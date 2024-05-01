javascript

# Puppeteer in Node.js: Common Mistakes to Avoid

![Greg Gorlen](/_next/image?url=%2Fimages%2Fauthors%2Fgreg-gorlen.jpg&w=3840&q=75)

[Greg Gorlen](https://blog.appsignal.com/authors/greg-gorlen.html) on Feb 7, 2023

![Puppeteer in Node.js: Common Mistakes to Avoid](/_next/image?url=%2Fimages%2Fblog%2F2023-02%2Fpuppeteer-pitfalls.png&w=3840&q=50)

\[data-rehype-pretty-code-fragment\] pre { content-visibility: auto; }

## This post is part of [Pitfalls of Puppeteer Series](https://blog.appsignal.com/series/pitfalls-of-puppeteer.html)

1. [1Puppeteer in Node.js: Common Mistakes to Avoid](https://blog.appsignal.com/2023/02/08/puppeteer-in-nodejs-common-mistakes-to-avoid.html)
2. [2Puppeteer in Node.js: More Antipatterns to Avoid](https://blog.appsignal.com/2023/06/14/puppeteer-in-nodejs-more-antipatterns-to-avoid.html)

[Puppeteer](https://github.com/puppeteer/puppeteer) is a powerful Node.js browser automation library for integration testing and web scraping. However, like any complex software, it comes with plenty of potential pitfalls.

In this article, I'll discuss a variety of common Puppeteer mistakes I've encountered in personal and consulting projects, as well as when monitoring the [Puppeteer tag on Stack Overflow](https://stackoverflow.com/questions/tagged/puppeteer). Once you're aware of these problematic patterns, you can write more robust scraping and testing code, while spending less time debugging and wading through arcane Puppeteer errors.

## Pre-requisites

The article was written using Node 18, Puppeteer 19.4.1, Chrome 108.0.5359.125, and Firefox 108.0.1.

We will assume you are familiar with ES6 JavaScript syntax, browser development tools, the browser DOM, and Node, and have previously written some Puppeteer scripts.

Now let's examine the pitfalls of Puppeteer.

## Common Pitfalls in Puppeteer for Node.js

### Attempting to Return Objects and DOM Elements from `evaluate` Callbacks

The following snippet should be a familiar pattern to those who've previously used Puppeteer:

javascript

```javascript
const puppeteer = require('puppeteer');

let browser;
(async () => {
	browser = await puppeteer.launch();
	const [page] = await browser.pages();
	const url = 'https://www.example.com';
	await page.goto(url, { waitUntil: 'domcontentloaded' });

	const element = await page.evaluate(() => {
		// executed in the browser
		return document.querySelector('h1');
	});
	console.log(element); // => always an empty object, {}
})()
	.catch((err) => console.error(err))
	.finally(() => browser?.close());
```

_**Note**: I'll skip the [IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE), import, and error-handling boilerplate in the remainder of this article._

The code above attempts to return a DOM element from the browser context back to Node for further processing (clicking it, typing into it, extracting its text content, etc.). However, the [`evaluate`](https://pptr.dev/api/puppeteer.page.evaluate/) call, which runs code in the browser context, resolves to an empty object in Node. DOM elements are complex structures with circular references and cannot be readily serialized and deserialized. These elements can't be decoupled from the browser environment in a meaningful way.

This behavior isn't specific to Puppeteer. Running `JSON.stringify(document.querySelector("h1"))` on a page with a header element should return `'{}'` on a Chromium-based browser. Firefox gives `'null'`, also indicating a serialization failure.

One solution is to use [`page.$("h1")`](https://pptr.dev/api/puppeteer.page._) (or the more general [`page.evaluateHandle`](https://pptr.dev/api/puppeteer.page.evaluatehandle)) to create a Puppeteer [`ElementHandle`](https://pptr.dev/api/puppeteer.elementhandle) that exposes an interface to the DOM element. Alternatively, you can use [`JSHandle`](https://pptr.dev/api/puppeteer.jshandle) which exposes an interface to the JS object. These interfaces enable you to run code in the browser context on the element, possibly to extract serializable data such as text content or element properties, or issue [trusted events](https://pptr.dev/faq/#q-whats-the-difference-between-a-trusted-and-untrusted-input-event). Be sure to dispose of these handles when you no longer need them to avoid memory leaks.

I've used `evaluate` here as it's the most general way to run code in the browser, but the same behavior applies to [`$eval`](https://pptr.dev/api/puppeteer.elementhandle._eval) and [`$$eval`](https://pptr.dev/api/puppeteer.elementhandle.__eval) as well. These methods are shorthands for the common case when `document.querySelector` or `document.querySelectorAll` is the first line in the `evaluate` callback.

## Trying to Access Variables from an `evaluate` Callback

At times, variables may appear to be in scope from an `evaluate` callback in Puppeteer when they aren't. The following example is a bit contrived because we could use `$eval`, but it nevertheless illustrates the pattern succinctly:

javascript

```javascript
const selector = 'h1';
const text = await page.evaluate(() => {
	return document.querySelector(selector).textContent;
});
```

Here, `selector` seems like it should be in scope of the `evaluate` callback, but it doesn't exist when the callback runs in the browser, throwing `Evaluation failed: ReferenceError: selector is not defined`. Yet again, serialization is the culprit: the browser is a completely separate process from Node that doesn't have your Node variables in scope.

Using the string version of `evaluate` makes the situation clearer:

javascript

```javascript
const selector = 'h1';
const text = await page.evaluate(`
 document.querySelector("${selector}").textContent
`);
console.log(text); // => Example Domain`
```

↓ Article continues below

![Left squiggle](/_next/image?url=%2Fimages%2Fcomponents%2Fbanner%2Fimg-left%402x.png&w=3840&q=75)

#### Is your app broken or slow? AppSignal lets you know.

[Monitoring by AppSignal →](https://www.appsignal.com/nodejs)

![Right squiggle](/_next/image?url=%2Fimages%2Fcomponents%2Fbanner%2Fimg-right%402x.png&w=3840&q=75)

However, building a string can lead to quoting problems. This motivates the more general approach — passing data to the browser by including extra arguments to `evaluate`:

```javascript
const selector = 'h1';
const text = await page.evaluate((selector) => {
	return document.querySelector(selector).textContent;
}, selector);
```

This parameter-passing pattern also applies to other important Puppeteer calls, such as [`page.waitForFunction`](https://pptr.dev/api/puppeteer.page.waitforfunction/). A subtle difference is that `waitForFunction`'s second argument is a configuration options object, followed by the variable parameter arguments:

javascript

```javascript
page.waitForFunction((arg1, arg2) => {...}, options, arg1, arg2);
```

[This Stack Overflow post](https://stackoverflow.com/questions/58870660/puppeteer-converting-circular-structure-to-json-are-you-passing-a-nested-jshand/68294113#68294113) offers tips on passing complex arguments to `evaluate` calls.

## Assuming Browser DevTools Is the Same as Node

Puppeteer programmers stuck on a bug often claim their selectors work in browser developer tools, but fail in Puppeteer. Unfortunately, there's no guarantee that code that works in browser developer tools will also work in Puppeteer. Here are some reasons why:

-   Developer tools exposes [iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) and [shadow root](https://developer.mozilla.org/en-US/docs/Web/API/ShadowRoot) subtrees. Puppeteer requires these trees to be explicitly expanded. It’s worth noting that Microsoft's Playwright library has locators that [expand the shadow DOM by default](https://playwright.dev/docs/locators#locate-in-shadow-dom).
-   By the time you get around to interacting with developer tools, the page has typically loaded its resources and executed its JS scripts. In Puppeteer, you can use `waitForSelector` calls to ensure JS-injected elements are available before interaction.
-   When working in an unautomated browser's developer tools, the website's server trusts you and delivers a full experience. In Node, Puppeteer scripts are often detected as bots, so they are blocked outright or served a restricted version of a page. Adding `console.log(await page.content())` is an easy way to verify that your HTML structure in Puppeteer is what you expect.

Recognizing developer tools and Node as distinct environments goes a long way to ensuring smooth translations from your developer tools exploration code to the final Puppeteer script.

## Assuming Puppeteer's Headless Mode Works the Same as Headful

Just as DevTools is distinct from Node, it's a mistake to assume that Puppeteer's headless mode works the same as headful mode. Websites have a much easier time detecting scripts as bots when in headless mode than in headful mode.

As with the above tip, `console.log(await page.content())` is a great way to ensure a document is what you expect. If a selector you see in the developer tools or in headful mode isn't in the headless log, there's a good chance you've been blocked.

## Not Using `Promise.all` When Triggering Navigation with a Click

Navigation is a common point of failure in Puppeteer scripts. The following code is unsafe:

javascript

```javascript
await page.click('#submit'); // trigger a navigation
await page.waitForNavigation();
```

In fact, this is a race condition. If the navigation resolves before [`waitForNavigation`](https://pptr.dev/api/puppeteer.page.waitfornavigation/) has the chance to run, the script may throw a timeout error. The correct pattern is:

javascript

```javascript
await Promise.all([
	page.waitForNavigation(),
	page.click('#submit') // trigger a navigation
]);
```

Or:

```javascript
const navigationPromise = page.waitForNavigation();
await page.click('#submit'); // trigger a navigation
await navigationPromise;
```

In these examples, the navigation wait promise is set before the navigation is triggered, ensuring that it will resolve as intended.

## Making Unnecessary Calls to `waitForNetworkIdle` or `waitForNavigation`

Another navigation-related mistake is making spurious calls to [`waitForNetworkIdle`](https://pptr.dev/api/puppeteer.page.waitfornetworkidle/) or `waitForNavigation`. For example:

javascript

```javascript
await page.goto('some url');
await page.waitForNavigation();
```

This is logical: we want to trigger a navigation with [`goto`](https://pptr.dev/api/puppeteer.page.goto/), then wait for that navigation to settle. But `goto` already waits for navigation, so the second `waitForNavigation` is waiting for a navigation that's already occurred, causing a timeout.

It's a similar story when waiting for an idle network state, either with a `waitForNetworkIdle` call or `page.goto(url, {waitUntil: "networkidle0"})`. In fact, waiting for an idle network can make the navigation time out if the automated page keeps enough long-running connections open.

`networkidle2` is usually safer since it tolerates two long-running connections. However, it is often used out of laziness or lack of awareness in place of the clear-cut `waitForSelector` and `waitForFunction` predicates.

## Using Infinite Timeouts

It's a mistake to set any timeout to 0 — for example, with [`page.setDefaultTimeout(0)`](https://pptr.dev/api/puppeteer.page.setdefaulttimeout/). Infinite timeouts introduce the potential for the script to block forever when encountering an unexpected state, without giving a clear error message. Under most circumstances, when a script hangs on a selector or navigation for more than a few minutes, it should log an error and either exit so its maintainer can fix the problem, or restart itself if it should keep attempting to do something.

Usually, when I come across infinite timeouts in Puppeteer scripts, it's an artifact of attempting to fix a deeper issue, like the script being detected as a bot and blocked. But the infinite timeout makes these errors harder to detect and resolve by stifling them and causing a silent hang.

## Forgetting to Await a Puppeteer Call

Almost all Puppeteer API calls are asynchronous. The reason for the asynchronous interface is that the browser runs in a separate process from Node. Puppeteer's methods send and receive data and wait for the browser process to respond, much like networking or file system operations. The Node process can use this time to perform CPU-bound work.

A common mistake is forgetting to `await` a promise returned by a Puppeteer call. This can lead to confusing and non-deterministic errors and race conditions.

For example, omitting `await` on a `page.goto` call may result in a `Protocol error (Page.navigate): Target closed` or `Execution context was destroyed, most likely because of a navigation`.

## Awaiting Synchronous Puppeteer Calls

One solution to the missing `await` problem described above is to `await` everything, but this can lead to confusion as well.

For example, I see the following pattern often:

```javascript
await page.on('request', (request) => {
	/* handle the request */
});
// do stuff after the request has been handled
```

Since `page.on` doesn't return a promise, it's easy to forget that `// do stuff after the request has been handled` runs before the request handler callback. The callback is in a different promise chain.

To solve this, use Puppeteer's `page.waitForRequest` (or `page.waitForResponse`) instead of `page.on`, which acts as a shorthand for manually [promisifying](https://javascript.info/promisify) the `page.on` callback.

## Creating Node.js Memory Leaks with `page.on` Listeners

Consider the following code:

```javascript
for (;;) {
	page.on('request', () => {});
	await setTimeout(10); // from "timers/promises"
}
```

This code reinstalls an event listener over and over again, slowly eating memory. The problem seems obvious in this minimal example, but I've seen it buried in the midst of moderately-complex, long-running jobs that eventually crash.

## Misunderstanding `page.exposeFunction`

[`page.exposeFunction`](https://pptr.dev/api/puppeteer.page.exposefunction/) enables your browser code to trigger Node code. As with `evaluate`, you can't pass DOM elements or other non-serializable structures as parameters, so a typical use case is passing serialized data like JSON or text for periodic processing. In the common case, you'll use `evaluate` to extract data rather than `exposeFunction`.

## Doing Too Much Work in Parallel

Another obvious pattern when seen in isolation is:

```javascript
const urlsToScrape = [
	/* large array */
];

const browser = await puppeteer.launch();
const results = await Promise.all(
	urlsToScrape.map(async (url) => {
		await page.goto(url, { waitUntil: 'domcontentloaded' });
		return page.$eval('h1', (element) => element.textContent);
	})
);
```

If `urlsToScrape` happens to be large enough, the memory and processor load from spawning dozens or hundreds of pages can bring a system down quickly. Consider [puppeteer-cluster](https://github.com/thomasdondorf/puppeteer-cluster).

## Wrapping Up

In this article, we've seen a variety of mistakes and gotchas that every Puppeteer programmer should be aware of.

I hope these tips will save you from making the same mistakes I've made over the years, so you can keep your tests and scripts running smoothly.

**P.S. If you liked this post, [subscribe to our JavaScript Sorcery list](https://blog.appsignal.com/javascript-sorcery) for a monthly deep dive into more magical JavaScript tips and tricks.**

**P.P.S. If you need an APM for your Node.js app, go and [check out the AppSignal APM for Node.js](https://www.appsignal.com/nodejs).**

## This post is part o
