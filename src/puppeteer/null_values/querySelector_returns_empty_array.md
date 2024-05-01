# [Query selector with puppeteer returns empty array](https://stackoverflow.com/questions/56619822/query-selector-with-puppeteer-returns-empty-array)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 4 years, 10 months ago

Modified [3 years, 7 months ago](https://stackoverflow.com/questions/56619822/query-selector-with-puppeteer-returns-empty-array?lastactivity "2020-09-23 15:20:37Z")

Viewed 2k times

This question shows research effort; it is useful and clear

2

This question does not show any research effort; it is unclear or not useful

 

Save this question.

[](https://stackoverflow.com/posts/56619822/timeline)

Show activity on this post.

I've got a short scraper written to pull some titles from a page using Puppeteer. While I can scrape individual elements, like a lone h2, trying to scrape and return an array of items hasn't been successful.

Mainly I've tried to make sure my query selector is even working, I can run `Array.from(document.querySelectorAll('div.landscape h3.title')).map(partner => partner.textContent)` in my Chrome dev tools and get the array I'm looking for, but running it in my script returns an empty array `[]`. As stated before, using just a lone querySelect('h2') seems to work fine.

```javascript
const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto('https://marketingplatform.google.com/about/partners/find-a-partner');

  const titlesArray = await page.evaluate(
    () => Array.from(document.querySelectorAll('div.landscape h3.title')).map(partner => partner.textContent)
  );


  console.log(titlesArray);


  await browser.close();
})();
```

No error messages seem to produce, just a console log of an empty array.

- [node.js](https://stackoverflow.com/questions/tagged/node.js "show questions tagged 'node.js'")
- [puppeteer](https://stackoverflow.com/questions/tagged/puppeteer "show questions tagged 'puppeteer'")

[Share](https://stackoverflow.com/q/56619822/15588573 "Short permalink to this question")

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ "The current license for this post: CC BY-SA 4.0")

[Edit](https://stackoverflow.com/posts/56619822/edit "Revise and improve this post")

Follow 

Follow this question to receive notifications

asked Jun 16, 2019 at 14:37

[

![Leroy's user avatar](https://graph.facebook.com/1711864272431419/picture?type=large)

](https://stackoverflow.com/users/6063528/leroy)

[Leroy](https://stackoverflow.com/users/6063528/leroy)Leroy

8188 bronze badges

0

[Add a comment](https://stackoverflow.com/questions/56619822/query-selector-with-puppeteer-returns-empty-array# "Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.") | [](https://stackoverflow.com/questions/56619822/query-selector-with-puppeteer-returns-empty-array# "Expand to show all comments on this post")

Report this ad

## 1 Answer 1

Sorted by: [Reset to default](https://stackoverflow.com/questions/56619822/query-selector-with-puppeteer-returns-empty-array?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

3

This answer is not useful

 

Save this answer.

[](https://stackoverflow.com/posts/56619881/timeline)

Show activity on this post.

When the page first loads, it shows a "Loading" text and redirects/loads data from there.

You have to wait for the element to be present in the DOM. Here is what the code might look,

```javascript
await page.goto('https://marketingplatform.google.com/about/partners/find-a-partner');
await page.waitForSelector('div.landscape h3.title'); // <-- add this line //updated from page.waitFor that is getting deprecated in 2020
```

[Share](https://stackoverflow.com/a/56619881/15588573 "Short permalink to this answer")

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ "The current license for this post: CC BY-SA 4.0")

[Edit](https://stackoverflow.com/posts/56619881/edit "Revise and improve this post")

Follow 

Follow this answer to receive notifications

[edited Sep 23, 2020 at 15:20](https://stackoverflow.com/posts/56619881/revisions "show all edits to this post")

[

![Leonardo Nobre Ghiggino's user avatar](https://lh3.googleusercontent.com/a-/AOh14GgUAHDPFjS1aGKFkHdHPCyqWnqMJmI7wRmN8ZzhcQ=k-s64)

](https://stackoverflow.com/users/13693557/leonardo-nobre-ghiggino)

[Leonardo Nobre Ghiggino](https://stackoverflow.com/users/13693557/leonardo-nobre-ghiggino)

8711 silver badge99 bronze badges

answered Jun 16, 2019 at 14:46

[

![Md. Abu Taher's user avatar](https://i.stack.imgur.com/YAtzE.jpg?s=64&g=1)

](https://stackoverflow.com/users/6161265/md-abu-taher)

[Md. Abu Taher](https://stackoverflow.com/users/6161265/md-abu-taher)Md. Abu Taher

18.3k55 gold badges5454 silver badges7676 bronze badges

1

- This was exactly it! Alternatively, I also used `await page.waitFor(2000);` to wait for the page to load after 2 seconds, before moving onto creating my array. Fantastic and thank you!
    
    – [Leroy](https://stackoverflow.com/users/6063528/leroy "81 reputation")
    
    [Jun 16, 2019 at 20:09](https://stackoverflow.com/questions/56619822/query-selector-with-puppeteer-returns-empty-array#comment99817455_56619881)
    

[Add a comment](https://stackoverflow.com/questions/56619822/query-selector-with-puppeteer-returns-empty-array# "Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.") | [](https://stackoverflow.com/questions/56619822/query-selector-with-puppeteer-returns-empty-array# "Expand to show all comments on this post")

  

## Your Answer