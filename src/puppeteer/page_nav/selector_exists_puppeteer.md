# [How can I check if selector exists in Puppeteer?](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 4 years, 5 months ago

Modified [3 months ago](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer?lastactivity '2024-01-23 17:28:01Z')

Viewed 63k times

This question shows research effort; it is useful and clear

33

This question does not show any research effort; it is unclear or not useful

Save this question.

[](https://stackoverflow.com/posts/58675083/timeline)

Show activity on this post.

In Puppeteer, how can I check if, for example, `#idProductType` exists and if not, set `producttype` to `""`? I tried many many things but it doesn't work.

```javascript
const urls = [myurls, ...]
const productsList = [];
for (let i = 0; i < urls.length; i++) {
    const url = urls[i];
    await Promise.all([
        page.goto(url),
        page.waitForNavigation({ waitUntil: 'networkidle0' }),
    ]);

    let products = await page.evaluate(() => {

  //here i want to test if #idProductType exists do :
        let producttype = document.querySelector('#idProductType').innerText;
  //else
        let producttype = "";
  //and same thing for other selectors

        let productsubtype = document.querySelector('#idProductSubType').innerText;
        let product = document.querySelector('#idProduct').innerText;
        let description = document.querySelector('td.js-orderModelVer').innerText;
        let reference = document.querySelector('td.text-nowrap').innerText;
        let prixpub = document.querySelector('td.text-nowrap.text-right.js-pricecol-msrp').innerText;
        let dispo = document.querySelector('td.text-nowrap.text-center.js-pricecol-availability').innerText;
        let retire = document.querySelector('td.js-retired-filler-cell').innerText;

        let results = [];
        results.push({
            producttype: producttype,
            productsubtype: productsubtype,
            product: product,
            description: description,
            reference: reference,
            prixpub: prixpub,
            dispo: dispo,
            retire: retire
        })
        return results
    })
    productsList.push(products);
}
```

-   [javascript](https://stackoverflow.com/questions/tagged/javascript "show questions tagged 'javascript'")
-   [node.js](https://stackoverflow.com/questions/tagged/node.js "show questions tagged 'node.js'")
-   [puppeteer](https://stackoverflow.com/questions/tagged/puppeteer "show questions tagged 'puppeteer'")

[Share](https://stackoverflow.com/q/58675083/15588573 'Short permalink to this question')

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/58675083/edit 'Revise and improve this post')

Follow

Follow this question to receive notifications

[edited Aug 6, 2022 at 1:22](https://stackoverflow.com/posts/58675083/revisions 'show all edits to this post')

[

![ggorlen's user avatar](https://www.gravatar.com/avatar/193965abcb7230d85c6264e55e2f0bda?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/6243352/ggorlen)

[ggorlen](https://stackoverflow.com/users/6243352/ggorlen)

51.4k77 gold badges9292 silver badges132132 bronze badges

asked Nov 2, 2019 at 20:36

[

![Cyri1's user avatar](https://www.gravatar.com/avatar/2976e3c6fd7308c04d09932c2ada762f?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/11733392/cyri1)

[Cyri1](https://stackoverflow.com/users/11733392/cyri1)Cyri1

40911 gold badge44 silver badges99 bronze badges

1

-   As an aside, there's no need to `waitForNavigation` alongside `goto`. `goto` already lets you specify `{waitUntil: "networkidle0"}` in its options parameter.
    – [ggorlen](https://stackoverflow.com/users/6243352/ggorlen '51,419 reputation')
    [Sep 15, 2023 at 15:29](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer#comment135942151_58675083)

[Add a comment](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.') | [](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Expand to show all comments on this post')

Report this ad

## 8 Answers 8

Sorted by: [Reset to default](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

17

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/63305002/timeline)

Show activity on this post.

You can use [page.$(selector)](https://pptr.dev/#?product=Puppeteer&version=v5.2.1&show=api-pageselector) which is similar to [document.querySelector(selector)](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)

```javascript
let producttype = (await page.$('#idProductType')) || '';
```

[Share](https://stackoverflow.com/a/63305002/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/63305002/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Aug 7, 2020 at 15:38

[

![Mohammad Faisal's user avatar](https://lh3.googleusercontent.com/-rnANl0i9X0g/AAAAAAAAAAI/AAAAAAAAABk/T_ETnB_Rato/photo.jpg?sz=64)

](https://stackoverflow.com/users/9993322/mohammad-faisal)

[Mohammad Faisal](https://stackoverflow.com/users/9993322/mohammad-faisal)Mohammad Faisal

2,27411 gold badge1717 silver badges2727 bronze badges

[Add a comment](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Expand to show all comments on this post')

This answer is useful

16

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/62256839/timeline)

Show activity on this post.

return innerText or empty string if not found:

```javascript
let productType = await page.evaluate(() => {
	let el = document.querySelector('.foo');
	return el ? el.innerText : '';
});
```

[Share](https://stackoverflow.com/a/62256839/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/62256839/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Jun 8, 2020 at 7:14

[

![pguardiario's user avatar](https://www.gravatar.com/avatar/917fcb4327159076f752c0c3c3fddfbb?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/966023/pguardiario)

[pguardiario](https://stackoverflow.com/users/966023/pguardiario)pguardiario

54.4k2020 gold badges122122 silver badges166166 bronze badges

[Add a comment](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Expand to show all comments on this post')

This answer is useful

13

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/67645733/timeline)

Show activity on this post.

Puppeteer throws an error when could not find a matched element.

So to confirm the existence,

```javascript
try {
	await page.$(selector);
	// Does exist
} catch {
	// Does not
}
```

Or to make whether it exists a flag

```javascript
const exists = await page.$eval(selector, () => true).catch(() => false);
```

[Share](https://stackoverflow.com/a/67645733/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/67645733/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited May 26, 2021 at 12:55](https://stackoverflow.com/posts/67645733/revisions 'show all edits to this post')

answered May 22, 2021 at 3:06

[

![SHION TONATIUH FUJIE's user avatar](https://lh4.googleusercontent.com/-EyQJfDHnktQ/AAAAAAAAAAI/AAAAAAAAARQ/JJ1mtNAtNt0/photo.jpg?sz=64)

](https://stackoverflow.com/users/9164525/shion-tonatiuh-fujie)

[SHION TONATIUH FUJIE](https://stackoverflow.com/users/9164525/shion-tonatiuh-fujie)SHION TONATIUH FUJIE

14711 silver badge33 bronze badges

1

-   8
    Not quite true. `page.$(selector)` resolves to `null` if no element matches `selector`. I usually use `const exists = !! await page.$(selector);`
    – [impeto](https://stackoverflow.com/users/1532684/impeto '350 reputation')
    [Aug 1, 2021 at 7:32](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer#comment121249662_67645733)

[Add a comment](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Expand to show all comments on this post')

This answer is useful

8

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/62245383/timeline)

Show activity on this post.

Another aproach that may be more suitable for such usecases:

```javascript
let producttype;

if ((await page.$('#idProductType')) !== null) {
	// do things with its content
	producttype = await page.evaluate(
		(el) => el.innerText,
		await page.$('#idProductType')
	);
} else {
	// do something else
	producttype = '';
}
```

[Share](https://stackoverflow.com/a/62245383/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/62245383/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Jun 7, 2020 at 12:33

[

![theDavidBarton's user avatar](https://i.stack.imgur.com/RhbKC.png?s=64&g=1)

](https://stackoverflow.com/users/12412595/thedavidbarton)

[theDavidBarton](https://stackoverflow.com/users/12412595/thedavidbarton)theDavidBarton

8,30444 gold badges2727 silver badges5353 bronze badges

[Add a comment](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Expand to show all comments on this post')

This answer is useful

7

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/58675227/timeline)

Show activity on this post.

`querySelector()` returns `null` value if there are not available element in DOM with specific selector

So you could write simple helper function:

```javascript
const getInnerTextForSelector = (selector) => {
	const element = document.querySelector(selector);
	if (element) return element.innerText;
	return '';
};
```

and run for example for `#idProductType` selector:

```javascript
const producttype = getInnerTextForSelector('#idProductType');
```

Or you could write helper which will operate on puppeteer Page and ElementHandle's:

```javascript
const getElementForSelector = async (page, selector) => {
	return (await element.$(selector)) || undefined;
};

export const getInnerText = async (page, selector) => {
	const elementForSelector = await getElementForSelector(page, selector);
	try {
		if (elementForSelector)
			return (
				(await elementForSelector.evaluate((element) => {
					return element.innerText;
				})) || ''
			);
	} catch {
		return '';
	}
};
```

and then run for example for `#idProductType` selector:

```javascript
const producttype = await getInnerText(page, '#idProductType');
```

[Share](https://stackoverflow.com/a/58675227/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/58675227/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Nov 2, 2019 at 20:56

[

![Fiszcz's user avatar](https://graph.facebook.com/1703657002998790/picture?type=large)

](https://stackoverflow.com/users/8850253/fiszcz)

[Fiszcz](https://stackoverflow.com/users/8850253/fiszcz)Fiszcz

10111 silver badge88 bronze badges

[Add a comment](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Expand to show all comments on this post')

This answer is useful

3

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/69046955/timeline)

Show activity on this post.

If the element is generated by Javascript it's a good idea to use a timeout:

```javascript
let producttype;
try {
	await page.waitForSelector('#idProductType', { timeout: 1000 });
	producttype = document.querySelector('#idProductType').innerText;
} catch (error) {
	producttype = '';
}
```

[Share](https://stackoverflow.com/a/69046955/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/69046955/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Sep 3, 2021 at 14:57

[

![embe's user avatar](https://www.gravatar.com/avatar/758a74a096f04f11d243413ad0a421fa?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/1746269/embe)

[embe](https://stackoverflow.com/users/1746269/embe)embe

1,08422 gold badges1111 silver badges2525 bronze badges

[Add a comment](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Expand to show all comments on this post')

This answer is useful

3

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/69732490/timeline)

Show activity on this post.

Here is the method I use to do this

Here is the way I do it

```javascript
if (page.$(selector) !== null) {
	// selector was found in the page
} else {
	// selector not found
}
```

for reference, you may check [this discussion](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-339020744)

also [here](https://gist.github.com/lh7dev/aa82c8ad2ecd04fdad5d54bcc78fda0c#file-extract-yp-details-page-js) you can see it in action

[Share](https://stackoverflow.com/a/69732490/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/69732490/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Oct 27, 2021 at 3:51](https://stackoverflow.com/posts/69732490/revisions 'show all edits to this post')

answered Oct 27, 2021 at 3:40

[

![LH7's user avatar](https://i.stack.imgur.com/CxuEv.jpg?s=64&g=1)

](https://stackoverflow.com/users/4701248/lh7)

[LH7](https://stackoverflow.com/users/4701248/lh7)LH7

1,40522 gold badges1313 silver badges1616 bronze badges

[Add a comment](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Expand to show all comments on this post')

This answer is useful

1

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/58675331/timeline)

Show activity on this post.

I think i find a way to do it, i don't know if it is the best solution :

```javascript
            var producttype = "";
            try {
                var producttype = document.querySelector('#idProductType').innerText;
            } catch (err) {
                console.log("The element didn't appear.")
```

[Share](https://stackoverflow.com/a/58675331/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/58675331/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Nov 2, 2019 at 21:09

[

![Cyri1's user avatar](https://www.gravatar.com/avatar/2976e3c6fd7308c04d09932c2ada762f?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/11733392/cyri1)

[Cyri1](https://stackoverflow.com/users/11733392/cyri1)Cyri1

40911 gold badge44 silver badges99 bronze badges

[Add a comment](https://stackoverflow.com/questions/58675083/how-can-i-check-if-selector-exists-in-puppeteer# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.')
