# [puppeteer: how to wait until an element is visible?](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 6 years, 7 months ago

Modified [1 month ago](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible?lastactivity '2024-02-27 21:53:24Z')

Viewed 193k times

This question shows research effort; it is useful and clear

94

This question does not show any research effort; it is unclear or not useful

Save this question.

[](https://stackoverflow.com/posts/46135853/timeline)

Show activity on this post.

I would like to know if I can tell puppeteer to wait until an element is displayed.

```javascript
const inputValidate = await page.$('input[value=validate]');
await inputValidate.click();

// I want to do something like that
waitElemenentVisble('.btnNext ');

const btnNext = await page.$('.btnNext');
await btnNext.click();
```

Is there any way I can accomplish this?

-   [javascript](https://stackoverflow.com/questions/tagged/javascript "show questions tagged 'javascript'")
-   [node.js](https://stackoverflow.com/questions/tagged/node.js "show questions tagged 'node.js'")
-   [google-chrome-devtools](https://stackoverflow.com/questions/tagged/google-chrome-devtools "show questions tagged 'google-chrome-devtools'")
-   [puppeteer](https://stackoverflow.com/questions/tagged/puppeteer "show questions tagged 'puppeteer'")

[Share](https://stackoverflow.com/q/46135853/15588573 'Short permalink to this question')

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/46135853/edit 'Revise and improve this post')

Follow

Follow this question to receive notifications

[edited Aug 29, 2020 at 21:23](https://stackoverflow.com/posts/46135853/revisions 'show all edits to this post')

[

![theDavidBarton's user avatar](https://i.stack.imgur.com/RhbKC.png?s=64&g=1)

](https://stackoverflow.com/users/12412595/thedavidbarton)

[theDavidBarton](https://stackoverflow.com/users/12412595/thedavidbarton)

8,30444 gold badges2727 silver badges5353 bronze badges

asked Sep 9, 2017 at 23:01

[

![Pipo's user avatar](https://graph.facebook.com/911728185527055/picture?type=large)

](https://stackoverflow.com/users/4542111/pipo)

[Pipo](https://stackoverflow.com/users/4542111/pipo)Pipo

5,37777 gold badges3535 silver badges6767 bronze badges

1

-   1
    Note about modals, just in case (I know this wasn't asked, but I feel a common enough pitfall): element visibility with modals that fade in/out is tricky. An element can be visible, but not yet clickable due to modal opacity etc. You can either disable transitions for test, or just register shown/hidden hooks, write a boolean variable on window, and wait for the right value in tests around modal interactions. Saves lots of flakes.
    – [ron](https://stackoverflow.com/users/180258/ron '9,364 reputation')
    [Oct 24, 2020 at 20:27](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment114081601_46135853)

[Add a comment](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.') | [](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Expand to show all comments on this post')

Report this ad

## 8 Answers 8

Sorted by: [Reset to default](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

120

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/46135989/timeline)

Show activity on this post.

I think you can use `page.waitForSelector(selector[, options])` function for that purpose.

```javascript
const puppeteer = require('puppeteer');

puppeteer.launch().then(async (browser) => {
	const browser = await puppeteer.launch({
		executablePath:
			'C:\\Program Files\\Google\\Chrome\\Application\\chrome.exe',
		headless: false
	});
	const page = await browser.newPage();
	await page.setUserAgent(options.agent);
	await page.goto('https://www.url.net', {
		timeout: 60000,
		waitUntil: 'domcontentloaded'
	});

	page.waitForSelector('#myId').then(() => console.log('got it'));
	browser.close();
});
```

To check the options available, please see the [github link.](https://github.com/puppeteer/puppeteer/blob/main/docs/api/puppeteer.elementhandle.waitforselector.md)

[Share](https://stackoverflow.com/a/46135989/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/46135989/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Feb 27 at 21:53](https://stackoverflow.com/posts/46135989/revisions 'show all edits to this post')

answered Sep 9, 2017 at 23:25

[

![C.Unbay's user avatar](https://i.stack.imgur.com/LDe4I.jpg?s=64&g=1)

](https://stackoverflow.com/users/6876149/c-unbay)

[C.Unbay](https://stackoverflow.com/users/6876149/c-unbay)C.Unbay

2,78522 gold badges1717 silver badges3232 bronze badges

9

-   2
    `waitForXPath()` ?
    – [Gilles Quénot](https://stackoverflow.com/users/465183/gilles-qu%c3%a9not '180,803 reputation')
    [May 16, 2018 at 10:03](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment87751909_46135989)
-   1
    @joy, you could just use `page.waitFor` which is very versatile
    – [JamieJag](https://stackoverflow.com/users/312716/jamiejag '1,550 reputation')
    [Jun 6, 2018 at 12:27](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment88449221_46135989)
-   19
    how is this a good answer? the code snippet doesn't even go a web page!
    – [shafeen](https://stackoverflow.com/users/1249278/shafeen '2,449 reputation')
    [Jul 1, 2018 at 18:01](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment89236297_46135989)
-   4
    @shafeen I proposed an edit for the snippet to work, but it still hasn't been accepted yet :/ I however think the snippet is still relevant, as it demonstrates how `page.waitForSelector` can be used
    – [Nino Filiu](https://stackoverflow.com/users/8186898/nino-filiu '17,672 reputation')
    [Dec 20, 2018 at 14:23](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment94588062_46135989)
-   1
    Example code not tested and missing url
    – [Gabe](https://stackoverflow.com/users/5315239/gabe '1,173 reputation')
    [Dec 28, 2021 at 17:04](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment124640232_46135989)

[](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [Show **4** more comments](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Expand to show all comments on this post')

This answer is useful

88

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/55212494/timeline)

Show activity on this post.

If you want to ensure the element is actually visible, you have to use

```javascript
await page.waitForSelector('#myId', { visible: true });
```

Otherwise you are just looking for the element in the DOM and not checking for visibility.

[Share](https://stackoverflow.com/a/55212494/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/55212494/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Sep 16, 2022 at 14:36](https://stackoverflow.com/posts/55212494/revisions 'show all edits to this post')

[

![Cepheus's user avatar](https://www.gravatar.com/avatar/f837408e776d259cca73ad33eeb9f782?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/1485347/cepheus)

[Cepheus](https://stackoverflow.com/users/1485347/cepheus)

4,65266 gold badges3333 silver badges4545 bronze badges

answered Mar 17, 2019 at 22:16

[

![finn's user avatar](https://www.gravatar.com/avatar/daa8867ef849b3c26fb8773a4bcd1775?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/1462065/finn)

[finn](https://stackoverflow.com/users/1462065/finn)finn

1,26899 silver badges1010 bronze badges

2

-   5
    In my case I needed the opposite which is `page.waitForSelector('#myId', {hidden: true})` to wait until a loader was hidden before continuing
    – [Chris Magnuson](https://stackoverflow.com/users/101679/chris-magnuson '5,859 reputation')
    [May 16, 2019 at 17:36](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment98974323_55212494)
-   This does not work if the element has height/width 0. Check this answer for that [stackoverflow.com/a/54103671/528468](https://stackoverflow.com/a/54103671/528468)
    – [Aalex Gabi](https://stackoverflow.com/users/528468/aalex-gabi '1,665 reputation')
    [Nov 11, 2021 at 16:00](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment123618101_55212494)

[Add a comment](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Expand to show all comments on this post')

This answer is useful

53

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/54103671/timeline)

Show activity on this post.

> **Note, All the answers submitted until today are incorrect**

Because it answer for an element if **Exist or Located** `but NOT` **Visible or Displayed**

The right answer is to check an element size or visibility using [`page.waitFor()`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pagewaitforselectororfunctionortimeout-options-args) or [`page.waitForFunction()`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pagewaitforfunctionpagefunction-options-args), see explaination below.

```javascript
// wait until present on the DOM
// await page.waitForSelector( css_selector );
// wait until "display"-ed
await page.waitForFunction(
	"document.querySelector('.btnNext') && document.querySelector('.btnNext').clientHeight != 0"
);
// or wait until "visibility" not hidden
await page.waitForFunction(
	"document.querySelector('.btnNext') && document.querySelector('.btnNext').style.visibility != 'hidden'"
);

const btnNext = await page.$('.btnNext');
await btnNext.click();
```

## Explanation

The element that Exist on the DOM of page not always Visible if has CSS property `display:none` or `visibility:hidden` that why using `page.waitForSelector(selector)` is not good idea, let see the different in the snippet below.

Show code snippet

```javascript
function isExist(selector) {
	let el = document.querySelector(selector);
	let exist = el.length != 0 ? 'Exist!' : 'Not Exist!';
	console.log(selector + ' is ' + exist);
}

function isVisible(selector) {
	let el = document.querySelector(selector).clientHeight;
	let visible = el != 0 ? 'Visible, ' + el : 'Not Visible, ' + el;
	console.log(selector + ' is ' + visible + 'px');
}

isExist('#idA');
isVisible('#idA');
console.log('=============================');
isExist('#idB');
isVisible('#idB');
```

```css
.bd {
	border: solid 2px blue;
}
```

```xml
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<div class="bd">
  <div id="idA" style="display:none">#idA, hidden element</div>
</div>
<br>
<div class="bd">
  <div id="idB">#idB, visible element</div>
</div>
```

Run code snippetHide results

Expand snippet

on the snippet above the function `isExist()` is simulate

```javascript
page.waitForSelector('#myId');
```

and we can see while running `isExist()` for both element `#idA` an `#idB` is return exist.

But when running `isVisible()` the `#idA` is not visible or dislayed.

And here other objects to check if an element is displayed or using CSS property `display`.

```javascript
scrollWidth;
scrollHeight;
offsetTop;
offsetWidth;
offsetHeight;
offsetLeft;
clientWidth;
clientHeight;
```

for style `visibility` check with not `hidden`.

note: I'm not good in Javascript or English, feel free to improve this answer.

[Share](https://stackoverflow.com/a/54103671/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/54103671/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited May 19, 2020 at 9:34](https://stackoverflow.com/posts/54103671/revisions 'show all edits to this post')

[

![0fnt's user avatar](https://www.gravatar.com/avatar/406e1885d98ceda53c6b7caa886ad7c3?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/247077/0fnt)

[0fnt](https://stackoverflow.com/users/247077/0fnt)

8,4711010 gold badges4747 silver badges6464 bronze badges

answered Jan 9, 2019 at 5:21

[

![ewwink's user avatar](https://www.gravatar.com/avatar/9ef09f4a6e7e0803825d17212d2dba67?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/458214/ewwink)

[ewwink](https://stackoverflow.com/users/458214/ewwink)ewwink

18.9k22 gold badges4545 silver badges5555 bronze badges

3

-   3
    Absolutely right! However there is actually an option in puppeteer for this. See my answer.
    – [finn](https://stackoverflow.com/users/1462065/finn '1,268 reputation')
    [Mar 17, 2019 at 22:17](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment97160825_54103671)
-   1
    @finn, unless the next page has the exact same selectors, which does does not allow you to differentiate between the current and next page. `waitForFunction` allows you to do this.
    – [caram](https://stackoverflow.com/users/2893408/caram '1,622 reputation')
    [Jan 15, 2021 at 14:00](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment116228005_54103671)
-   waitFor() is gone as of version 15 according to the release notes.
    – [Stan Smith](https://stackoverflow.com/users/2611739/stan-smith '906 reputation')
    [Aug 23, 2022 at 0:34](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment129713876_54103671)

[Add a comment](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Expand to show all comments on this post')

This answer is useful

18

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/52123869/timeline)

Show activity on this post.

You can use [`page.waitFor()`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pagewaitforselectororfunctionortimeout-options-args), [`page.waitForSelector()`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pagewaitforselectorselector-options), or [`page.waitForXPath()`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pagewaitforxpathxpath-options) to wait for an element on a [page](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#class-page):

```javascript
// Selectors

const css_selector = '.btnNext';
const xpath_selector =
	'//*[contains(concat(" ", normalize-space(@class), " "), " btnNext ")]';

// Wait for CSS Selector

await page.waitFor(css_selector);
await page.waitForSelector(css_selector);

// Wait for XPath Selector

await page.waitFor(xpath_selector);
await page.waitForXPath(xpath_selector);
```

> **Note:** In reference to a [frame](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#class-frame), you can also use [`frame.waitFor()`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#framewaitforselectororfunctionortimeout-options-args), [`frame.waitForSelector()`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#framewaitforselectorselector-options), or [`frame.waitForXPath()`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#framewaitforxpathxpath-options).

[Share](https://stackoverflow.com/a/52123869/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/52123869/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Mar 4, 2020 at 6:17](https://stackoverflow.com/posts/52123869/revisions 'show all edits to this post')

answered Sep 1, 2018 at 0:09

[

![Grant Miller's user avatar](https://i.stack.imgur.com/a6JjK.jpg?s=64&g=1)

](https://stackoverflow.com/users/4283581/grant-miller)

[Grant Miller](https://stackoverflow.com/users/4283581/grant-miller)Grant Miller

28.4k1616 gold badges151151 silver badges167167 bronze badges

2

-   1
    Isn't it redundant to await for page.waitFor?
    – [FabricioG](https://stackoverflow.com/users/2690257/fabriciog '3,199 reputation')
    [Mar 3, 2020 at 18:24](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment107053646_52123869)
-   3
    Yes it is, and now it's also deprecated.
    – [Moshisho](https://stackoverflow.com/users/2470092/moshisho '2,871 reputation')
    [Nov 10, 2020 at 8:36](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible#comment114510941_52123869)

[Add a comment](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Expand to show all comments on this post')

This answer is useful

13

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/51611029/timeline)

Show activity on this post.

Updated answer with some optimizations:

```javascript
const puppeteer = require('puppeteer');

(async () => {
	const browser = await puppeteer.launch({ headless: true });
	const page = await browser.newPage();

	await page.goto('https://www.somedomain.com', {
		waitUntil: 'networkidle2'
	});
	await page.click('input[value=validate]');
	await page.waitForSelector('#myId');
	await page.click('.btnNext');
	console.log('got it');

	browser.close();
})();
```

[Share](https://stackoverflow.com/a/51611029/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/51611029/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Jul 31, 2018 at 10:17

[

![andyrandy's user avatar](https://i.stack.imgur.com/YKQis.png?s=64&g=1)

](https://stackoverflow.com/users/757508/andyrandy)

[andyrandy](https://stackoverflow.com/users/757508/andyrandy)andyrandy

73.6k99 gold badges113113 silver badges132132 bronze badges

[Add a comment](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Expand to show all comments on this post')

This answer is useful

7

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/58604555/timeline)

Show activity on this post.

While I agree with @ewwink answer. Puppeteer's API checks for not hidden by default, so when you do:

```javascript
await page.waitForSelector('#id', { visible: true });
```

You get not hidden and visible by CSS. To ensure rendering you can do as @ewwink's `waitForFunction`. However to completely answer your question, here's a snippet using puppeteer's API:

```javascript
async waitElemenentVisble(selector) {
  function waitVisible(selector) {
    function hasVisibleBoundingBox(element) {
      const rect = element.getBoundingClientRect()
      return !!(rect.top || rect.bottom || rect.width || rect.height)
    }
    const elements = [document.querySelectorAll(selector)].filter(hasVisibleBoundingBox)
    return elements[0]
  }
  await page.waitForFunction(waitVisible, {visible: true}, selector)
  const jsHandle = await page.evaluateHandle(waitVisible, selector)
  return jsHandle.asElement()
}
```

After writing some methods like this myself, I found [expect-puppeteer](https://github.com/smooth-code/jest-puppeteer/tree/master/packages/expect-puppeteer) which does this and more better (see [toMatchElement](https://github.com/smooth-code/jest-puppeteer/tree/master/packages/expect-puppeteer#toMatchElement)).

[Share](https://stackoverflow.com/a/58604555/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/58604555/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Oct 29, 2019 at 9:27

[

![Moshisho's user avatar](https://www.gravatar.com/avatar/0636779beb52178d154f350f92e0a394?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/2470092/moshisho)

[Moshisho](https://stackoverflow.com/users/2470092/moshisho)Moshisho

2,87111 gold badge2323 silver badges4141 bronze badges

[Add a comment](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Expand to show all comments on this post')

This answer is useful

3

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/67850199/timeline)

Show activity on this post.

```javascript
async function waitForVisible (selector){
    //const selector = '.foo';
  return  await page.waitForFunction(
      (selector) => document.querySelector(selector) && document.querySelector(selector).clientHeight != 0",
      {},
      selector
    );
}
```

---

Above function makes it generic, so that you can use it anywhere.

---

But, if you are using pptr there is another faster and easier solution:

[https://pptr.dev/#?product=Puppeteer&version=v10.0.0&show=api-pagewaitforfunctionpagefunction-options-args](https://pptr.dev/#?product=Puppeteer&version=v10.0.0&show=api-pagewaitforfunctionpagefunction-options-args)

---

```javascript
page.waitForSelector('#myId', { visible: true });
```

[Share](https://stackoverflow.com/a/67850199/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/67850199/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Jun 5, 2021 at 13:44

[

![Frank Guo's user avatar](https://i.stack.imgur.com/nxYs7.jpg?s=64&g=1)

](https://stackoverflow.com/users/2123187/frank-guo)

[Frank Guo](https://stackoverflow.com/users/2123187/frank-guo)Frank Guo

68788 silver badges88 bronze badges

[Add a comment](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/46135853/puppeteer-how-to-wait-until-an-element-is-visible# 'Expand to show all comments on this post')

This answer is useful

2

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/70994408/timeline)

Show activity on this post.

Just tested this by scraping a fitness website. @ewwink, @0fnt, and @caram have provided the most complete answer.

Just because a DOM element is visible doesn't mean that it's content has been fully populated.

Today, I ran:

```javascript
await page.waitForSelector('table#some-table', { visible: true });
const data = await page.$eval('table#some-table', (el) => el.outerHTML);
console.log(data);
```

And incorrectly received the following, because the table DOM hadn't been populated fully by runtime. You can see that the outerHTML is empty.

`user@env:$ <table id="some-table"></table>`

Adding a pause of 1 second fixed this, as might be expected:

```javascript
function sleep(ms) {
	return new Promise((resolve) => setTimeout(resolve, ms));
}

await page.waitForSelector('table#some-table', { visible: true });
await sleep(1000);
const data = await page.$eval('table#some-table', (el) => el.outerHTML);
console.log(data);
```

`user@env:$ <table id="some-table"><tr><td>Data</td></tr></table>`

But so did @ewwink's answer, more elegantly (no artificial timeouts):

```javascript
await page.waitForSelector('table#some-table', { visible: true });
await page.waitForFunction(
	"document.querySelector('table#sched-records').clientHeight != 0"
);
const data = await page.$eval('table#some-table', (el) => el.outerHTML);
console.log(data);
```

`user@env:$ <table id="some-table"><tr><td>Data</td></tr></table>`

[Share](https://stackoverflow.com/a/70994408/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/70994408/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Feb 5, 2022 at 0:53](https://stackoverflow.com/posts/70994408/revisions 'show all edits to this post')

answered Feb 5, 20
