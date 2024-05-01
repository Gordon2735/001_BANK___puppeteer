# [Reusing browser and page instance in Puppeteer?](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 12 months ago

Modified [12 months ago](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer?lastactivity '2023-05-05 17:01:35Z')

Viewed 1k times

This question shows research effort; it is useful and clear

0

This question does not show any research effort; it is unclear or not useful

Save this question.

[](https://stackoverflow.com/posts/76181003/timeline)

Show activity on this post.

For performance and resource reasons I try to reuse the same instance of a puppeteer browser and page. I have structured my code like this:

```javascript
async function createBrowser(id) {
    let bench = new Date().getTime();
    browser = await puppeteer.launch({
        headless: false,
        executablePath: browserPath
    });
    let pages = await browser.pages();
    let page = pages[0];
    let cookiesString = await fs.readFile(cookiePath);
    let cookies = JSON.parse(cookiesString);
    await page.setCookie(...cookies);
    console.log(
        '\x1b[1m',
        `[${new Date().toLocaleTimeString()}] Browser opened successfully in ${new Date().getTime() - bench}ms.`,
        '\x1b[0m'
    );
    worker(id, page);
}
```

And my worker/scraper logic:

```javascript
async function worker(id, page) {
    console.log(page);
    let bench = new Date().getTime();
    let url = 'https://www.mypagetoscrape.xyz';
    let response = await page.goto(url, {waitUntil: 'networkidle0',});
    // further logic goes here
```

Then I execute the code the first time everything works like a charm, however when I call worker function a second time some minutes later I cannot work with response anymore - even though console.log(page) still prints the full page object.

If I wanna get `response.status()` for example the error message is `TypeError: Cannot read properties of null (reading 'status')`

Can someone please explain what I am doing wrong and how to properly reuse the same browser and page instance? Closing browser & page and re-opening them again later (before doing the worker logic) delays everything for about 200-300 ms and causes more CPU & Ram load, so I really wanna avoid it.

Thanks a lot in advance!

-   [node.js](https://stackoverflow.com/questions/tagged/node.js "show questions tagged 'node.js'")
-   [puppeteer](https://stackoverflow.com/questions/tagged/puppeteer "show questions tagged 'puppeteer'")

[Share](https://stackoverflow.com/q/76181003/15588573 'Short permalink to this question')

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/76181003/edit 'Revise and improve this post')

Follow

Follow this question to receive notifications

asked May 5, 2023 at 10:00

[

![l4m0r's user avatar](https://www.gravatar.com/avatar/e2c67f8426d74a1d7b674b99e5baa3b6?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/12115105/l4m0r)

[l4m0r](https://stackoverflow.com/users/12115105/l4m0r)l4m0r

2399 bronze badges

3

-   1
    Reuse the browser instance, create new page for each worker and close the page at the end of `worker()`.
    – [Inder](https://stackoverflow.com/users/18954618/inder '1,811 reputation')
    [May 5, 2023 at 10:08](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer#comment134346156_76181003)
-   I thought about that but I really wanna use the same page again as well. Can't imagine that it isn't possible
    – [l4m0r](https://stackoverflow.com/users/12115105/l4m0r '23 reputation')
    [May 5, 2023 at 10:24](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer#comment134346329_76181003)
-   1
    In that case just return browser object from `createBrowser`, create new pages with it and reuse them.
    – [Vaviloff](https://stackoverflow.com/users/2715393/vaviloff '16,590 reputation')
    [May 5, 2023 at 10:29](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer#comment134346386_76181003)

[Add a comment](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.') | [](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer# 'Expand to show all comments on this post')

Report this ad

## 2 Answers 2

Sorted by: [Reset to default](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

0

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/76184229/timeline)

Show activity on this post.

I'm not sure I fully understand your use case and I'm not able to reproduce your error, so it's hard to make a precise recommendation.

In general, though, here's a simple manager for a singleton `browser`/`page` combo:

```javascript
const puppeteer = require('puppeteer'); // ^19.7.5

const pageManager = ((opts) => {
    const browser = puppeteer.launch(opts);
    let page;
    return {
        newPage: async () => {
            await page?.close();
            page = await (await browser).newPage();
            // any arbitrary fixed page initialization here, or add a callback
            return page;
        },
        page: () => page,
        close: async () => (await browser).close()
    };
})({ headless: true });

(async () => {
    const url = 'https://www.example.com';
    const page = await pageManager.newPage();
    await page.goto(url, { waitUntil: 'domcontentloaded' });
    const el = await page.$('::-p-text(Example)');
    console.log(await el.evaluate((el) => el.textContent));
})()
    .catch((err) => console.error(err))
    .finally(() => pageManager.close());
```

The important thing is to make sure to close the browser if an error occurs. Otherwise, your script can hang forever, eating up resources and creating zombie processes.

Here's another approach which is a bit more direct but doesn't offer a way to reboot the page:

```javascript
const browser = puppeteer.launch();
const page = browser.then(async (browser) => {
    const page = await browser.newPage();
    // any arbitrary fixed page initialization here, or add a callback
    return page;
});
const browserManager = {
    // the public interface
    page: () => page,
    close: async () => (await browser).close()
};

(async () => {
    const url = 'https://www.example.com';
    const page = await browserManager.page();
    await page.goto(url, { waitUntil: 'domcontentloaded' });
    const el = await page.$('::-p-text(Example)');
    console.log(await el.evaluate((el) => el.textContent));
})()
    .catch((err) => console.error(err))
    .finally(() => browserManager.close());
```

Hopefully it's clear that all of the management code can be tucked away in a module.

Other approaches are possible.

If you're using Express, keep in mind that creating and destroying pages should be fairly lightweight, and you can't really share this singleton page with different clients. If you _really_ don't want to create new pages, consider a page pool where route handlers can "rent" pages for the task, then return them to the pool. [puppeteer-cluster](https://github.com/thomasdondorf/puppeteer-cluster) may be a good option. But I'd avoid premature optimization, and I'm speculating heavily as to your actual use case.

Note that [`networkidle0` is very slow](https://serpapi.com/blog/puppeteer-antipatterns/#never-using-domcontentloaded), so if you're experiencing a need to optimize, I'd start by looking at your mainline Puppeteer work.

[Share](https://stackoverflow.com/a/76184229/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/76184229/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited May 5, 2023 at 17:01](https://stackoverflow.com/posts/76184229/revisions 'show all edits to this post')

answered May 5, 2023 at 16:25

[

![ggorlen's user avatar](https://www.gravatar.com/avatar/193965abcb7230d85c6264e55e2f0bda?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/6243352/ggorlen)

[ggorlen](https://stackoverflow.com/users/6243352/ggorlen)ggorlen

51.6k77 gold badges9292 silver badges132132 bronze badges

[Add a comment](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer# 'Expand to show all comments on this post')

This answer is useful

0

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/76182345/timeline)

Show activity on this post.

Per the Puppeteer [goto()](https://pptr.dev/api/puppeteer.page.goto) docs (as of latest version v20.1.1), the result you want to achieve is not possible to do without at least some workarounds.

> NOTE: page.goto either throws an error or returns a main resource response. The only exceptions are navigation to about:blank or navigation to the same URL with a different hash, which would succeed and return null.

However, this just means that the `await page.goto()` response would return `null`, not that the navigation itself wouldn't work.

You can simply accept the navigation as completed as soon as the `.goto()` call is resolved, and proceed to run your own logic afterwards.

If you really need to obtain the initial `response` object, you should use a different approach. There are a few suggestions in this Github issue: [https://github.com/puppeteer/puppeteer/issues/2479](https://github.com/puppeteer/puppeteer/issues/2479).

One that seems to be working is [this one](https://github.com/puppeteer/puppeteer/issues/2479#issuecomment-646839471), which disables the cache, sets default navigation timeout to 0, and accesses the response by obtaining it in the first `page.waitForResponse()` resolution.

```javascript
page.setCacheEnabled(false);
await page.setDefaultNavigationTimeout(0);
response = await page.goto(url, { waitUntil: 'networkidle0' });

if (response === null) {
    response = await page.waitForResponse(() => true);
}
```

[Share](https://stackoverflow.com/a/76182345/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/76182345/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered May 5, 2023 at 12:44

[

![tmilar's user avatar](https://www.gravatar.com/avatar/42dfcaa88fc7eef6d9ab7e3e9b02eca8?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/6279385/tmilar)

[tmilar](https://stackoverflow.com/users/6279385/tmilar)tmilar

1,8111515 silver badges2020 bronze badges

1

-   `await page.setDefaultNavigationTimeout(0);` along with `networkidle0` is risky--you could hang the script forever if the navigation never resolves. I'd suggest setting this to no more than, in an extreme case, 10 hours or something, so if you have a long-running script you'll eventually get some report that something's wrong, rather than a script that seems to be doing its job but isn't.
    – [ggorlen](https://stackoverflow.com/users/6243352/ggorlen '51,606 reputation')
    [May 5, 2023 at 15:22](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer#comment134350657_76182345)

[Add a comment](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/76181003/reusing-browser-and-page-instance-in-puppeteer# 'Expand to show all comments on this post')

## Your Answer
