<!-- Continue on Null Value of Result -->

<img src="../../../public/images/901___stackoverflow.webp" style="width: 280px; border-radius: 7px;" /> 

[stackoverflow](https://stackoverflow.com/)
<br />
<br />
<img src="https://s.gravatar.com/avatar/8919c21a69fc2528689eb1832c8ed37f?s=480&r=pg&d=https%3A%2F%2Fcdn.auth0.com%2Favatars%2Fwe.png" style="border-radius: 50%; float: left; margin-right: 10px; width: 75px;" />

#### Gordon Mullen

<br />
<br />
<br />

# [Continue on Null Value of Result (Nodejs, Puppeteer)](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 6 years, 5 months ago

Modified [1 year, 1 month ago](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer?lastactivity '2023-03-16 19:55:58Z')

Viewed 3k times

This question shows research effort; it is useful and clear

2

This question does not show any research effort; it is unclear or not useful

Save this question.

[](https://stackoverflow.com/posts/47332699/timeline)

Show activity on this post.

I'm just starting to play around with Puppeteer (Headless Chrome) and Nodejs. I'm scraping some test sites, and things work great when all the values are present, but if the value is missing I get an error like:

`Cannot read property 'src' of null` (so in the code below, the first two passes might have all values, but the third pass, there is no picture, so it just errors out).

Before I was using `if(!picture) continue;` but I think it's not working now because of the for loop.

Any help would be greatly appreciated, thanks!

```javascript
for (let i = 1; i <= 3; i++) {
//...Getting to correct page and scraping it three times
  const result = await page.evaluate(() => {
      let title = document.querySelector('h1').innerText;
      let article = document.querySelector('.c-entry-content').innerText;
      let picture = document.querySelector('.c-picture img').src;

      if (!document.querySelector('.c-picture img').src) {
        let picture = 'No Link';     }  //throws error

      let source = "The Verge";
      let categories = "Tech";

      if (!picture)
                continue;  //throws error

      return {
        title,
        article,
        picture,
        source,
        categories
      }
    });
}
```

-   [javascript](https://stackoverflow.com/questions/tagged/javascript "show questions tagged 'javascript'")
-   [node.js](https://stackoverflow.com/questions/tagged/node.js "show questions tagged 'node.js'")
-   [puppeteer](https://stackoverflow.com/questions/tagged/puppeteer "show questions tagged 'puppeteer'")

[Share](https://stackoverflow.com/q/47332699/15588573 'Short permalink to this question')

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/47332699/edit 'Revise and improve this post')

Follow

Follow this question to receive notifications

asked Nov 16, 2017 at 14:52

[

![Alteredorange's user avatar](https://www.gravatar.com/avatar/4d90666a45ffe73a4e5fbdd702832413?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/2936521/alteredorange)

[Alteredorange](https://stackoverflow.com/users/2936521/alteredorange)Alteredorange

59611 gold badge77 silver badges2424 bronze badges

1

-   _Unrelated_ If your variable doesn't change use of `const` instead of `let`
    – [Orelsanpls](https://stackoverflow.com/users/3337080/orelsanpls '23,102 reputation')
    [Nov 16, 2017 at 15:11](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer#comment81617196_47332699)

[Add a comment](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.') | [](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer# 'Expand to show all comments on this post')

Report this ad

## 2 Answers 2

Sorted by: [Reset to default](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

3

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/47333156/timeline)

Show activity on this post.

```javascript
let picture = document.querySelector('.c-picture img').src;

if (!document.querySelector('.c-picture img').src) {
	let picture = 'No Link';
} //throws error
```

If there is no picture, then `document.querySelector()` returns null, which does not have a `src` property. You need to check that your query found an element before trying to read the `src` property.

Moving the null-check to the top of the function has the added benefit of saving unnecessary calculations when you are just going to bail out anyway.

```javascript
async function scrape3() {
  // ...
  for (let i = 1; i <= 3; i++) {
  //...Getting to correct page and scraping it three times
    const result = await page.evaluate(() => {
        const pictureElement = document.querySelector('.c-picture img');

        if (!pictureElement) return null;

        const picture = pictureElement.src;
        const title = document.querySelector('h1').innerText;
        const article = document.querySelector('.c-entry-content').innerText;

        const source = "The Verge";
        const categories = "Tech";

        return {
          title,
          article,
          picture,
          source,
          categories
        }
    });

    if (!result) continue;

    // ... do stuff with result
  }
```

---

### Answering comment question: "Is there a way just to skip anything blank, and return the rest?"

Yes. You just need to check the existence of each element that could be missing before trying to read a property off of it. In this case we can omit the early return since you're always interested in all the results.

```javascript
async function scrape3() {
	// ...
	for (let i = 1; i <= 3; i++) {
		const result = await page.evaluate(() => {
			const img = document.querySelector('.c-picture img');
			const h1 = document.querySelector('h1');
			const content = document.querySelector('.c-entry-content');

			const picture = img ? img.src : '';
			const title = h1 ? h1.innerText : '';
			const article = content ? content.innerText : '';
			const source = 'The Verge';
			const categories = 'Tech';

			return {
				title,
				article,
				picture,
				source,
				categories
			};
		});
		// ...
	}
}
```

---

### Further thoughts

Since I'm still on this question, let me take this one step further, and refactor it a bit with some higher level techniques you might be interested in. Not sure if this is exactly what you are after, but it should give you some ideas about writing more maintainable code.

```javascript
// Generic reusable helper to return an object property
// if object exists and has property, else a default value
//
// This is a curried function accepting one argument at a
// time and capturing each parameter in a closure.
//
const maybeGetProp = default => key => object =>
  (object && object.hasOwnProperty(key)) ? object.key : default

// Pass in empty string as the default value
//
const getPropOrEmptyString = maybeGetProp('')

// Apply the second parameter, the property name, making 2
// slightly different functions which have a default value
// and a property name pre-loaded. Both functions only need
// an object passed in to return either the property if it
// exists or an empty string.
//
const maybeText = getPropOrEmptyString('innerText')
const maybeSrc = getPropOrEmptyString('src')

async function scrape3() {
  // ...

  // The _ parameter name is acknowledging that we expect a
  // an argument passed in but saying we plan to ignore it.
  //
  const evaluate = _ => page.evaluate(() => {

    // Attempt to retrieve the desired elements
    //
    const img = document.querySelector('.c-picture img');
    const h1 = document.querySelector('h1')
    const content = document.querySelector('.c-entry-content')

    // Return the results, with empty string in
    // place of any missing properties.
    //
    return {
      title: maybeText(h1),
      article: maybeText(article),
      picture: maybeSrc(img),
      source: 'The Verge',
      categories: 'Tech'
    }
  }))

  // Start with an empty array of length 3
  //
  const evaluations = Array(3).fill()

    // Then map over that array ignoring the undefined
    // input and return a promise for a page evaluation
    //
    .map(evaluate)

  // All 3 scrapes are occuring concurrently. We'll
  // wait for all of them to finish.
  //
  const results = await Promise.all(evaluations)

  // Now we have an array of results, so we can
  // continue using array methods to iterate over them
  // or otherwise manipulate or transform them
  //
  return results
    .filter(result => result.title && result.picture)
    .forEach(result => {
      //
      // Do something with each result
      //
    })
}
```

[Share](https://stackoverflow.com/a/47333156/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/47333156/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Mar 16, 2023 at 19:55](https://stackoverflow.com/posts/47333156/revisions 'show all edits to this post')

answered Nov 16, 2017 at 15:14

[

![skylize's user avatar](https://www.gravatar.com/avatar/3918459025ff30659427cdd826567d7f?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/7776106/skylize)

[skylize](https://stackoverflow.com/users/7776106/skylize)skylize

1,41111 gold badge1010 silver badges2121 bronze badges

5

-   Thanks for the reply! implemented, but I get `SyntaxError: Illegal continue statement: no surrounding iteration statement`
    – [Alteredorange](https://stackoverflow.com/users/2936521/alteredorange '596 reputation')
    [Nov 16, 2017 at 15:17](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer#comment81617497_47333156)
-   Oh yes. That makes sense. I almost never use `for` loops anymore (favoring pure higher order functions and utilizing array methods like `map` instead), so I forget about some of the idiosyncrasies of a raw loop. Here the problem is the `continue` is inside a function that runs asynchronously, so basically the loop is not in the call stack when trying to `continue`. I've updated the example to pull `continue` out into the loop's root block. We still bail out early from the function, but use `return null` instead of `continue`.
    – [skylize](https://stackoverflow.com/users/7776106/skylize '1,411 reputation')
    [Nov 16, 2017 at 15:50](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer#comment81618934_47333156)
-   Awesome, I'm going to try this after lunch! Quick question, so if there is no src, does it not return anything? Is there a way just to skip anything blank, and return the rest? Thanks a million for the help!
    – [Alteredorange](https://stackoverflow.com/users/2936521/alteredorange '596 reputation')
    [Nov 16, 2017 at 18:56](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer#comment81626176_47333156)
-   Yeah, that example bails early and just returns `null` which is used to trigger `continue` since your original code seemed to be trying to bail out if missing `src`. I've added a replacement example that just returns empty strings for missing props, and another example with some more advanced ideas for you.
    – [skylize](https://stackoverflow.com/users/7776106/skylize '1,411 reputation')
    [Nov 18, 2017 at 2:17](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer#comment81676575_47333156)
-   I try to adapt your solution to my script where I have a Array.from structure in the page.evaluate. Like:`Array.from(document.querySelectorAll('article.section-wrap section'), value => ({ nom: value.querySelector('h1.title').innerText.trim(), ...` Is there a way to get a specific string for null values, I tried several ways without success. Maybe some ternary operator syntax maybe possible but i'm puzzled.
    – [Plouf](https://stackoverflow.com/users/2949510/plouf '397 reputation')
    [Jun 2, 2019 at 18:35](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer#comment99431463_47333156)

[Add a comment](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer# 'Expand to show all comments on this post')

This answer is useful

0

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/68587947/timeline)

Show activity on this post.

Try-catch worked for me:

```javascript
try {
	if ((await page.$eval('element')) !== null) {
		const name = await page.$eval('element');
	}
} catch (error) {
	name = '';
}
```

[Share](https://stackoverflow.com/a/68587947/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/68587947/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Jul 31, 2021 at 12:52](https://stackoverflow.com/posts/68587947/revisions 'show all edits to this post')

[

![Zoe is on strike's user avatar](https://i.stack.imgur.com/zgIdn.png?s=64&g=1)

](https://stackoverflow.com/users/6296561/zoe-is-on-strike)

[Zoe is on strike](https://stackoverflow.com/users/6296561/zoe-is-on-strike)♦

27.9k2222 gold badges125125 silver badges152152 bronze badges

answered Jul 30, 2021 at 8:40

[

![Giorgi Tediashvili's user avatar](https://lh3.googleusercontent.com/a/AATXAJzVXzg0K1bEdBpU2auQAhR3pOODT8e0qM8Ohnqb=k-s64)

](https://stackoverflow.com/users/16559925/giorgi-tediashvili)

[Giorgi Tediashvili](https://stackoverflow.com/users/16559925/giorgi-tediashvili)Giorgi Tediashvili

1

1

-   hello, you missed a `'` mark at `page.$eval('element)`
    – [I_love_vegetables](https://stackoverflow.com/users/15366635/i-love-vegetables '1,581 reputation')
    [Jul 30, 2021 at 8:44](https://stackoverflow.com/questions/47332699/continue-on-null-value-of-result-nodejs-puppeteer#comment121213601_68587947)
