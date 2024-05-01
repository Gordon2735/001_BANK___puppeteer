<!-- Puppeteer's query selector returns null, although it exists -->

<img src="../../../public/images/901___stackoverflow.webp" style="width: 280px; border-radius: 7px;" /> 

[stackoverflow](https://stackoverflow.com/)
<br />
<br />
<img src="https://s.gravatar.com/avatar/8919c21a69fc2528689eb1832c8ed37f?s=480&r=pg&d=https%3A%2F%2Fcdn.auth0.com%2Favatars%2Fwe.png" style="border-radius: 50%; float: left; margin-right: 10px; width: 75px;" />

#### Gordon Mullen

<br />
<br />
<br />


# [Puppeteer's query selector returns null, although it exists](https://stackoverflow.com/questions/72418221/puppeteers-query-selector-returns-null-although-it-exists)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 1 year, 11 months ago

Modified [1 year, 11 months ago](https://stackoverflow.com/questions/72418221/puppeteers-query-selector-returns-null-although-it-exists?lastactivity "2022-05-28 18:16:46Z")

Viewed 301 times

This question shows research effort; it is useful and clear

1

This question does not show any research effort; it is unclear or not useful

 

Save this question.

[](https://stackoverflow.com/posts/72418221/timeline)

Show activity on this post.

Ran into a problem that `querySelector()` returns `null` for an element that exists on the page. I looked up stackover flow for some answers, I tried:

```javascript
waitForSelector() & page.setUserAgent(UserAgent)
```

When I manually run the script `document.querySelector('span.s-item__price')` in the chrome console, it returned what I was expecting, but not when I tried with puppeteer.

```javascript
const puppeteer = require('puppeteer');

async function openBrowser(url, callback) {
const browser = await puppeteer.launch({
    headless: true,
    defaultViewport: {
        width: 1920,
        height: 1080
    }
});
const page = await browser.newPage();
await page.goto(`${url}`);
await callback(page);
await browser.close();
}


openBrowser('https://www.ebay.com/sch/i.html?_from=R40&_trksid=p2380057.m570.l1313&_nkw=men+watch&_sacat=0', async (page) => {

const products = await page.evaluate(() => {

    let resultArray = [];
    const productsArray = [...document.querySelectorAll('li.s-item.s-item__pl-on-bottom')];

    for (let i = 1; i < productsArray.length; i++) {
        resultArray.push({
            id: i,
            title: productsArray[i].querySelector('h3.s-item__title').textContent,
            img: productsArray[i].querySelector('img.s-item__image-img').src,
            price: productsArray[i].querySelector('span.s-item__price').textContent,
            // seller: productsArray[i].querySelector('.s-item__seller-info-text').textContent THIS ONE FAILS, TOP ONES WORK FINE.
        });
    }

    return resultArray;

});

console.log(products);

});
```

Run code snippetHide results

Expand snippet

- [javascript](https://stackoverflow.com/questions/tagged/javascript "show questions tagged 'javascript'")
- [node.js](https://stackoverflow.com/questions/tagged/node.js "show questions tagged 'node.js'")
- [puppeteer](https://stackoverflow.com/questions/tagged/puppeteer "show questions tagged 'puppeteer'")

[Share](https://stackoverflow.com/q/72418221/15588573 "Short permalink to this question")

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ "The current license for this post: CC BY-SA 4.0")

Edit

Follow 

Follow this question to receive notifications

asked May 28, 2022 at 18:16

[

![spectre's user avatar](https://www.gravatar.com/avatar/2f4af626255def74da4096635facd69b?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/19221809/spectre)

[spectre](https://stackoverflow.com/users/19221809/spectre)spectre

1111 bronze badge

3

- I'm not clear what the expected output is. Is the problem with the seller info text or the price? Arrays run from 0, so I assume you intended to skip the first element by starting at 1.
    
    – [ggorlen](https://stackoverflow.com/users/6243352/ggorlen "51,368 reputation")
    
    [May 28, 2022 at 19:03](https://stackoverflow.com/questions/72418221/puppeteers-query-selector-returns-null-although-it-exists#comment127932680_72418221)
    
- 1
    
    @ggorlen Yes, skip was needed for the first element. The output should be a list of simple scrape data from the ebay platform, but the last property of the object - seller, it fails with an error msg: TypeError: Cannot read properties of null (reading 'textContent'), but when run manually in the console of the browser -it is fine. I assume that this .s-item\_\_seller-info-text is dynamically rendered on the page, but not sure how to get it.
    
    – [spectre](https://stackoverflow.com/users/19221809/spectre "11 reputation")
    
    [May 28, 2022 at 19:21](https://stackoverflow.com/questions/72418221/puppeteers-query-selector-returns-null-although-it-exists#comment127932894_72418221)
    
- Gotcha--thanks. I see why you're skipping the first element, it appears to be a placeholder. After a bunch of runs, I see the seller sometimes, but it doesn't appear to be consistently rendered in this view.
    
    – [ggorlen](https://stackoverflow.com/users/6243352/ggorlen "51,368 reputation")
    
    [May 28, 2022 at 20:09](https://stackoverflow.com/questions/72418221/puppeteers-query-selector-returns-null-although-it-exists#comment127933427_72418221)
    

[Add a comment](https://stackoverflow.com/questions/72418221/puppeteers-query-selector-returns-null-although-it-exists# "Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.") | [](https://stackoverflow.com/questions/72418221/puppeteers-query-selector-returns-null-although-it-exists# "Expand to show all comments on this post")