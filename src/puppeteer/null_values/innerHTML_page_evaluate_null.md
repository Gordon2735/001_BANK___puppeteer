<!-- Puppeteer innerHTML page evaluate functions returning null and undefined errors -->

<img src="../../../public/images/901___stackoverflow.webp" style="width: 280px; border-radius: 7px;" />

[stackoverflow](https://stackoverflow.com/)
<br />
<br />
<img src="https://s.gravatar.com/avatar/8919c21a69fc2528689eb1832c8ed37f?s=480&r=pg&d=https%3A%2F%2Fcdn.auth0.com%2Favatars%2Fwe.png" style="border-radius: 50%; float: left; margin-right: 10px; width: 75px;" />

#### Gordon Mullen

<br />
<br />
<br />

# [Puppeteer innerHTML page evaluate functions returning null and undefined errors](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 3 years, 11 months ago

Modified [3 years, 11 months ago](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors?lastactivity '2020-05-16 00:16:29Z')

Viewed 951 times

This question shows research effort; it is useful and clear

\-1

This question does not show any research effort; it is unclear or not useful

Save this question.

[](https://stackoverflow.com/posts/61802607/timeline)

Show activity on this post.

```typescript
await page.$eval(
	'.class1' + variable + ' img.class2',
	(el) => (el.ParentElement.innerHTML = 'text to substitute')
);
```

I also tried

```typescript

await page.evaluate((variable) '.class1' + variable + ' img.class2', el => el.ParentElement.innerHTML = 'text to substitute');
```

I know that all my if statements enclosing this function are correct, and in inspector, the .class1VARIABLE img.class2 selection's .ParentElement returns the appropriate element.

Yet, when I run first function I get error around finding ParentElement of undefined, and when I run second function I get error around finding ParentElement of null. What gives? Am I failing to pass the variable in correctly? Am I evaluating the wrong DOM? 'variable' is doing the right thing, incrementing in a for statement, and I've verified that it's correct with console.log debugging statements within the logic that gets me here. I even tried hardcoding the variable inside the function, like

```typescript
await page.evaluate(() '.class1VARIABLE img.class2', el => el.ParentElement.innerHTML = 'text to substitute');
```

which I can't even comprehend how it would fail, and it crashed with either the null or undefined error also.

Kinda at the end of my wits here.

P.S. I fit matters, the image's ParentElement is a td.

-   [node.js](https://stackoverflow.com/questions/tagged/node.js "show questions tagged 'node.js'")
-   [puppeteer](https://stackoverflow.com/questions/tagged/puppeteer "show questions tagged 'puppeteer'")

[Share](https://stackoverflow.com/q/61802607/15588573 'Short permalink to this question')

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/61802607/edit 'Revise and improve this post')

Follow

Follow this question to receive notifications

asked May 14, 2020 at 16:34

[

![Tom Mercer's user avatar](https://www.gravatar.com/avatar/71098be704eafbf98058ccb2d9a9f09e?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/5022349/tom-mercer)

[Tom Mercer](https://stackoverflow.com/users/5022349/tom-mercer)Tom Mercer

12355 bronze badges

9

-   It seems there are some errors in your examples:
-

```typescript

await page.evaluate((variable) '.class1' + variable + ' img.class2',
    el => el.ParentElement.innerHTML = 'text to substitute');
await page.evaluate(() '.class1VARIABLE img.class2',
    el => el.ParentElement.innerHTML = 'text to substitute'); // are syntactically wrong.
```

    – [vsemozhebuty](https://stackoverflow.com/users/2625560/vsemozhebuty '13,382 reputation')
    [May 14, 2020 at 17:52](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors#comment109318207_61802607)

-   ...ok... you gonna specify HOW?
    – [Tom Mercer](https://stackoverflow.com/users/5022349/tom-mercer '123 reputation')
    [May 14, 2020 at 17:55](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors#comment109318275_61802607)
-   Sorry, I cannot surely suppose, These fragments should throw syntax errors. At least something like this should be tried:

```typescript
-(await page.evaluate((selector) => {
	document.querySelector(selector).ParentElement.innerHTML =
		'text to substitute';
}, '.class1' + variable + ' img.class2'));
await page.evaluate((selector) => {
	document.querySelector(selector).ParentElement.innerHTML =
		'text to substitute';
}, '.class1VARIABLE img.class2');
```

    – [vsemozhebuty](https://stackoverflow.com/users/2625560/vsemozhebuty "13,382 reputation")

    [May 14, 2020 at 18:12](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors#comment109318843_61802607)

-   They don't throw syntax errors. I'll try your suggestions. The selector is '.class1VARIABLE img.class2', for example.
    – [Tom Mercer](https://stackoverflow.com/users/5022349/tom-mercer '123 reputation')
    [May 14, 2020 at 19:15](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors#comment109320876_61802607)
-   Maybe you quote them with some omissions or inaccurate editions? For me, they throw `SyntaxError: missing ) after argument list` or `SyntaxError: Unexpected token ')'`.
    – [vsemozhebuty](https://stackoverflow.com/users/2625560/vsemozhebuty '13,382 reputation')
    [May 14, 2020 at 19:28](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors#comment109321255_61802607)

[](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors# 'Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.') | [Show **4** more comments](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors# 'Expand to show all comments on this post')

Report this ad

## 1 Answer 1

Sorted by: [Reset to default](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

2

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/61808212/timeline)

Show activity on this post.

An example of how to change the innerHTML of an element with a .class selector:

```javascript
'use strict';

const html = `
  <!doctype html>
  <html>
    <head><meta charset='UTF-8'><title>Test</title></head>
    <body><p class='test'>Text.</p></body>
  </html>`;

const puppeteer = require('puppeteer');

(async function main() {
	try {
		const browser = await puppeteer.launch({ headless: false });
		const [page] = await browser.pages();

		await page.goto(`data:text/html,${html}`);

		const pSelector = '.test';
		const newHTML = '<i>New text.</i>';

		await page.evaluate(
			(selector, html) => {
				document.querySelector(selector).parentElement.innerHTML = html;
			},
			pSelector,
			newHTML
		);
	} catch (err) {
		console.error(err);
	}
})();
```

[Share](https://stackoverflow.com/a/61808212/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/61808212/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited May 16, 2020 at 0:16](https://stackoverflow.com/posts/61808212/revisions 'show all edits to this post')

answered May 14, 2020 at 22:03

[

![vsemozhebuty's user avatar](https://i.stack.imgur.com/lsWVJ.png?s=64&g=1)

](https://stackoverflow.com/users/2625560/vsemozhebuty)

[vsemozhebuty](https://stackoverflow.com/users/2625560/vsemozhebuty)vsemozhebuty

13.4k11 gold badge2727 silver badges2828 bronze badges

14

-   I'm confused. What is 'selector' doing in the function? Is it not declared? Some sort of placeholder? What is pSelector doing?
    – [Tom Mercer](https://stackoverflow.com/users/5022349/tom-mercer '123 reputation')
    [May 15, 2020 at 7:45](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors#comment109335594_61808212)
-   1
    `pSelector` is a variable that is defined in the Node.js scope (main script scope). Function argument of `page.evaluate()` is executed in the document (browser) scope and has no access to the main script scope (including `pSelector` variable). To transfer any variables of main script scope to document (browser) scope, we need to add them as second, third, etc. arguments in the `page.evaluate()` function and they will become parameters of the evaluated function (in this example — `selector` parameter). So `querySelector` and `selector` have the same value but are accessed from different scopes.
    – [vsemozhebuty](https://stackoverflow.com/users/2625560/vsemozhebuty '13,382 reputation')
    [May 15, 2020 at 15:02](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors#comment109349348_61808212)
-   You can just hardcode the selector value in the evaluated function if this suffices. But if I understand correctly, You need to call the same function in a loop with incremented counter, so you need to use this scope interaction: define the incrementing variable in the Node.js scope and transfer it to the function evaluated in the document scope.
    – [vsemozhebuty](https://stackoverflow.com/users/2625560/vsemozhebuty '13,382 reputation')
    [May 15, 2020 at 15:11](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors#comment109349648_61808212)
-   Ran that code, getting "Error: Evaluation failed: TypeError: Cannot set property 'innerHTML' of null" again. Maybe it's to do with the .ParentElement part. Where would you insert the parent-ness? pass in pSelector.ParentElement? define pSelector = '.test.ParentElement'? Remember, I have to get an img by class, and then change its parent, (a td), with .innerHTML.
    – [Tom Mercer](https://stackoverflow.com/users/5022349/tom-mercer '123 reputation')
    [May 15, 2020 at 16:37](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors#comment109352493_61808212)
-   aside, is there any reason for try{ ing the whole main function? Puppeteer already essentially does that. I try{ed the page.evaluate function in my code.
    – [Tom Mercer](https://stackoverflow.com/users/5022349/tom-mercer '123 reputation')
    [May 15, 2020 at 16:39](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors#comment109352560_61808212)

[](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [Show **9** more comments](https://stackoverflow.com/questions/61802607/puppeteer-innerhtml-page-evaluate-functions-returning-null-and-undefined-errors# 'Expand to show all comments on this post')
