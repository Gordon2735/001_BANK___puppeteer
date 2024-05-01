<!-- Puppeteer querySelector returns null -->

<img src="../../../public/images/901___stackoverflow.webp" style="width: 280px; border-radius: 7px;" /> 

[stackoverflow](https://stackoverflow.com/)
<br />
<br />
<img src="https://s.gravatar.com/avatar/8919c21a69fc2528689eb1832c8ed37f?s=480&r=pg&d=https%3A%2F%2Fcdn.auth0.com%2Favatars%2Fwe.png" style="border-radius: 50%; float: left; margin-right: 10px; width: 75px;" />

#### Gordon Mullen

<br />
<br />
<br />


#   Puppeteer querySelector returns null
Asked 5 years, 10 months ago
Modified 5 years, 9 months ago
Viewed 44k times
11

I am trying to scrap some data with puppeteer but for some sites querySelector returns null and I have no idea what is wrong. I found some answers about this issue in stackoverflow but none of them worked. Here is the code with an example link that does not work.

```typescript
const puppeteer = require('puppeteer');

(async () => {
    const browser = await puppeteer.launch();
    const page = await browser.newPage();

    await page.goto('https://www.macys.com/shop/product/the-north-face-mens- 
    logo-half-dome-t-shirt?ID=2085687&CategoryID=30423&cm_kws=2085687');

    const textContent = await page.evaluate(() => {
    return document.querySelector('.price');
});

console.log(textContent); 

browser.close();
})();
```

node.jsweb-scrapingjquery-selectorspuppeteer
Share
Edit
Follow
asked Jun 3, 2018 at 6:53
Aram Sheroyan's user avatar
Aram Sheroyan
58811 gold badge66 silver badges1717 bronze badges
Add a comment

Report this ad
2 Answers
Sorted by:

Highest score (default)
31

Probably the elements are loaded asynchronously via javascript and are still not in the DOM when you're calling .evaluate().

Try to wait for the selector with puppeteer .waitForSelector function

```typescript
const puppeteer = require('puppeteer');

(async () => {
    const browser = await puppeteer.launch();
    const page = await browser.newPage();

await page.goto('https://www.macys.com/shop/product/the-north-face-mens- 
logo-half-dome-t-shirt?ID=2085687&CategoryID=30423&cm_kws=2085687');

await page.waitForSelector('.price');

const textContent = await page.evaluate(() => {
   return document.querySelector('.price');
});

console.log(textContent); 

browser.close();
})();
```


Share
Edit
Follow
edited Jul 9, 2018 at 8:24
answered Jun 4, 2018 at 8:13
Pjotr Raskolnikov's user avatar
Pjotr Raskolnikov
1,64822 gold badges1616 silver badges2727 bronze badges
Thanks for the response! I thought the problem was that the page wasn't fully loading, but after taking a snapshot of the page, it turned out that my request was getting blocked by a bot detection system. I'll post the solution. – 
Aram Sheroyan
 Jun 6, 2018 at 0:58
Where is document defined? It seems like it shouldn't exist in this context. – 
Dem Pilafian
 Jun 14, 2023 at 20:53
Add a comment
8

After taking a snapshot of the page, it turned out that my request gets blocked by a bot detection system. Here is the solution. We just need to pass some more data so it wont be detected as a bot. If it still not working, you can check out this tutorial.

```typescript
const puppeteer = require('puppeteer');

// This is where we'll put the code to get around the tests.
const preparePageForTests = async (page) => {

// Pass the User-Agent Test.
const userAgent = 'Mozilla/5.0 (X11; Linux x86_64)' +
  'AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.39 Safari/537.36';
await page.setUserAgent(userAgent);
}


(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await preparePageForTests(page);

 // await page.setRequestInterception(true);
 await page.goto('websiteURL');

 const textContent = await page.evaluate(() => {
   return {document.querySelector('yourCSSselector').textContent,
 }
 });
  console.log(textContent);

  browser.close();
  ```
  
Share
Edit
Follow
answered Jun 6, 2018 at 1:06
Aram Sheroyan's user avatar
Aram Sheroyan
58811 gold badge66 silver badges1717 bronze badges
This gave me the idea to take a screenshot, which revealed to me that i was actually working in the wrong tab – 
Michael Davidson
 May 25, 2020 at 19:01
1
Thank you. I faced the same problem. Just to clarify how to make a screenshot with puppeteer for future readers, I did this: await page.screenshot({ path: "./screenshot.jpg", type: "jpeg", fullPage: true }); Which saves a screenshot in the root folder of your project after running the script. – 
fjplaurr
 Sep 12, 2020 at 10:33
Add a comment