# [What is the difference between page.$$(selector) and page.$$eval(selector, function) in puppeteer?](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 2 years, 6 months ago

Modified [1 year, 4 months ago](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct?lastactivity "2022-12-03 04:39:19Z")

Viewed 2k times

This question shows research effort; it is useful and clear

1

This question does not show any research effort; it is unclear or not useful

 

Save this question.

[](https://stackoverflow.com/posts/69635543/timeline)

Show activity on this post.

I'm trying to load page elements into an array and retrieve the innerHTML from both and be able to click on them.

```javascript
var grabElements = await page.$$(selector);
await grabElements[0].click();
```

This allows me to grab my elements and click on them but it won't display innerHTML.

```javascript
var elNum = await page.$$eval(selector, (element) => {
    let n = []
    element.forEach(e => {
        n.push(e);
    })
    return n;  
});
await elNum[0].click();
```

This lets me get the innerHTML if I push the innerHTML to n. If I push just the element e and try to click or get its innerHTML outside of the var declaration, it doesn't work. The innerHTML comes as undefined and if I click, I get an error saying elnum\[index\].click() is not a function. What am I doing wrong?

- [javascript](https://stackoverflow.com/questions/tagged/javascript "show questions tagged 'javascript'")
- [puppeteer](https://stackoverflow.com/questions/tagged/puppeteer "show questions tagged 'puppeteer'")
- [webautomation](https://stackoverflow.com/questions/tagged/webautomation "show questions tagged 'webautomation'")

[Share](https://stackoverflow.com/q/69635543/15588573 "Short permalink to this question")

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ "The current license for this post: CC BY-SA 4.0")

[Edit](https://stackoverflow.com/posts/69635543/edit "Revise and improve this post")

Follow 

Follow this question to receive notifications

[edited Oct 20, 2021 at 15:12](https://stackoverflow.com/posts/69635543/revisions "show all edits to this post")

BrainLag

asked Oct 19, 2021 at 17:49

[

![BrainLag's user avatar](https://www.gravatar.com/avatar/f95b988689eda0717623c446bc17f1ed?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/14487611/brainlag)

[BrainLag](https://stackoverflow.com/users/14487611/brainlag)BrainLag

881010 bronze badges

12

- 1
    
    The difference is that `$$eval` returns whatever serializable the callback returns while `$$` returns the element handles. In other words, you could use `eval` to get `.innerHTML` and `$$` to get clickable handles. But you can also pull HTML from handles and click inside `eval`s with native functions, so it's pretty flexible. Could you show a simple HTML example, with the elements you want to click and the text you're hoping to get? Thanks.
    
    – [ggorlen](https://stackoverflow.com/users/6243352/ggorlen "51,419 reputation")
    
    [Oct 20, 2021 at 4:17](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct#comment123093192_69635543)
    
- An example of what I'm trying to get is: `<div class = "class">This is the innerHTML text I want. </div>`. On the page, it's text inside a clickable portion of the website. What i want to do is loop through the available options, then click on the ones that match an innerHTML I'm looking for.
    
    – [BrainLag](https://stackoverflow.com/users/14487611/brainlag "88 reputation")
    
    [Oct 20, 2021 at 15:10](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct#comment123108454_69635543)
    
- I've tried using grabElement\[0\].getProperty('innerHTML').jsonValue() but I keep getting back `.jsonValue() is not a function.`.
    
    – [BrainLag](https://stackoverflow.com/users/14487611/brainlag "88 reputation")
    
    [Oct 20, 2021 at 15:24](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct#comment123108838_69635543)
    
- If you want to click something by text, why not use [xpath](https://stackoverflow.com/a/58088028/6243352)? Do you have a link to the page? The specification still seems rather vague and pseudocodey for me to be able to write a runnable, complete answer.
    
    – [ggorlen](https://stackoverflow.com/users/6243352/ggorlen "51,419 reputation")
    
    [Oct 20, 2021 at 15:35](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct#comment123109089_69635543)
    
- 1
    
    @titoih Maybe ask a new question if you have a new question. What about `grabElements[0].click()` is confusing and/or not working exactly?
    
    – [ggorlen](https://stackoverflow.com/users/6243352/ggorlen "51,419 reputation")
    
    [Dec 2, 2022 at 19:35](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct#comment131781185_69635543)
    

[](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct# "Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.") | [Show **7** more comments](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct# "Expand to show all comments on this post")

Report this ad

## 1 Answer 1

Sorted by: [Reset to default](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

1

This answer is not useful

 

Save this answer.

[](https://stackoverflow.com/posts/74660819/timeline)

Show activity on this post.

The difference between `page.$$eval` (and other `evaluate`\-style methods, with the exception of `evaluateHandle`) and `page.$$` is that the `evaluate` family only works with serializable values. As you discovered, you [can't return elements from these methods](https://stackoverflow.com/questions/53032903/get-elements-from-page-evaluate-in-puppeteer) because they're not serialiable (they have circular references and would be useless in Node anyway).

On the other hand, `page.$$` returns Puppeteer ElementHandles that are references to DOM elements that can be manipulated from Puppeteer's API in Node rather than in the browser. This is useful for many reasons, one of which is that `ElementHandle.click()` issues a [totally different set of operations](https://serpapi.com/blog/puppeteer-antipatterns/#assuming-puppeteers-api-works-like-the-native-browser-api) than running the native `DOMElement.click()` in the browser.

From the [comments](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct#comment123108454_69635543):

> An example of what I'm trying to get is: `<div class = "class">This is the innerHTML text I want. </div>`. On the page, it's text inside a clickable portion of the website. What i want to do is loop through the available options, then click on the ones that match an `innerHTML` I'm looking for.

Here's a simple example you should be able to extrapolate to your actual use case:

```javascript
const puppeteer = require("puppeteer"); // ^19.1.0
const {setTimeout} = require("timers/promises");

const html = `
<div>
  <div class="class">This is the innerHTML text I want.</div>
  <div class="class">This is the innerHTML text I don't want.</div>
  <div class="class">This is the innerHTML text I want.</div>
</div>
<script>
document.querySelectorAll(".class").forEach(e => {
  e.addEventListener("click", () => e.textContent = "clicked");
});
</script>
`;

const target = "This is the innerHTML text I want.";

let browser;
(async () => {
  browser = await puppeteer.launch();
  const [page] = await browser.pages();
  await page.setContent(html);

  ///////////////////////////////////////////
  // approach 1 -- trusted Puppeteer click //
  ///////////////////////////////////////////
  const handles = await page.$$(".class");

  for (const handle of handles) {
    if (target === (await handle.evaluate(el => el.textContent))) {
      await handle.click();
    }
  }

  // show that it worked and reset
  console.log(await page.$eval("div", el => el.innerHTML));
  await page.setContent(html);

  //////////////////////////////////////////////
  // approach 2 -- untrusted native DOM click //
  //////////////////////////////////////////////
  await page.$$eval(".class", (els, target) => {
    els.forEach(el => {
      if (target === el.textContent) {
        el.click();
      }
    });
  }, target);

  // show that it worked and reset
  console.log(await page.$eval("div", el => el.innerHTML));
  await page.setContent(html);

  /////////////////////////////////////////////////////////////////
  // approach 3 -- selecting with XPath and using trusted clicks //
  /////////////////////////////////////////////////////////////////
  const xp = '//*[@class="class"][text()="This is the innerHTML text I want."]';

  for (const handle of await page.$x(xp)) {
    await handle.click();
  }

  // show that it worked and reset
  console.log(await page.$eval("div", el => el.innerHTML));
  await page.setContent(html);

  ///////////////////////////////////////////////////////////////////
  // approach 4 -- selecting with XPath and using untrusted clicks //
  ///////////////////////////////////////////////////////////////////
  await page.evaluate(xp => {
    // https://stackoverflow.com/a/68216786/6243352
    const $x = xp => {
      const snapshot = document.evaluate(
        xp, document, null,
        XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null
      );
      return [...Array(snapshot.snapshotLength)]
        .map((_, i) => snapshot.snapshotItem(i))
      ;
    };
    $x(xp).forEach(e => e.click());
  }, xp);

  // show that it worked
  console.log(await page.$eval("div", el => el.innerHTML));
})()
  .catch(err => console.error(err))
  .finally(() => browser?.close());
```

Output in all cases is:

```xml
<div class="class">clicked</div>
<div class="class">This is the innerHTML text I don't want.</div>
<div class="class">clicked</div>
```

Note that `===` might be too strict without calling `.trim()` on the `textContent` first. You may want an `.includes()` substring test instead, although the risk there is that it's too permissive. Or a regex may be the right tool. In short, use whatever makes sense for your use case rather than (necessarily) my `===` test.

With respect to the XPath approach, [this answer](https://stackoverflow.com/a/64626061/6243352) shows a few options for dealing with whitespace and substrings.

[Share](https://stackoverflow.com/a/74660819/15588573 "Short permalink to this answer")

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ "The current license for this post: CC BY-SA 4.0")

[Edit](https://stackoverflow.com/posts/74660819/edit "Revise and improve this post")

Follow 

Follow this answer to receive notifications

[edited Dec 3, 2022 at 4:39](https://stackoverflow.com/posts/74660819/revisions "show all edits to this post")

answered Dec 2, 2022 at 19:49

[

![ggorlen's user avatar](https://www.gravatar.com/avatar/193965abcb7230d85c6264e55e2f0bda?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/6243352/ggorlen)

[ggorlen](https://stackoverflow.com/users/6243352/ggorlen)ggorlen

51.4k77 gold badges9292 silver badges132132 bronze badges

[Add a comment](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct# "Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.") | [](https://stackoverflow.com/questions/69635543/what-is-the-difference-between-page-selector-and-page-evalselector-funct# "Expand to show all comments on this post")