# Page.waitForSelector() method

Wait for the `selector` to appear in page. If at the moment of calling the method the `selector` already exists, the method will return immediately. If the `selector` doesn't appear after the `timeout` milliseconds of waiting, the function will throw.

#### Signature:[​](https://pptr.dev/api/puppeteer.page.waitforselector#signature 'Direct link to Signature:')

```javascript
class Page {  waitForSelector<Selector extends string>(    selector: Selector,    options?: WaitForSelectorOptions  ): Promise<ElementHandle<NodeFor<Selector>> | null>;}
```

## Parameters[​](https://pptr.dev/api/puppeteer.page.waitforselector#parameters 'Direct link to Parameters')

A [selector](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors) of an element to wait for

[WaitForSelectorOptions](https://pptr.dev/api/puppeteer.waitforselectoroptions)

|

_(Optional)_ Optional waiting parameters

|

**Returns:**

Promise<[ElementHandle](https://pptr.dev/api/puppeteer.elementhandle)<[NodeFor](https://pptr.dev/api/puppeteer.nodefor)<Selector>> | null>

Promise which resolves when element specified by selector string is added to DOM. Resolves to `null` if waiting for hidden: `true` and selector is not found in DOM.

## Remarks[​](https://pptr.dev/api/puppeteer.page.waitforselector#remarks 'Direct link to Remarks')

The optional Parameter in Arguments `options` are:

-   `visible`: A boolean wait for element to be present in DOM and to be visible, i.e. to not have `display: none` or `visibility: hidden` CSS properties. Defaults to `false`.
-   `hidden`: Wait for element to not be found in the DOM or to be hidden, i.e. have `display: none` or `visibility: hidden` CSS properties. Defaults to `false`.
-   `timeout`: maximum time to wait for in milliseconds. Defaults to `30000` (30 seconds). Pass `0` to disable timeout. The default value can be changed by using the [Page.setDefaultTimeout()](https://pptr.dev/api/puppeteer.page.setdefaulttimeout) method.

## Example[​](https://pptr.dev/api/puppeteer.page.waitforselector#example 'Direct link to Example')

This method works across navigations:

```javascript
import puppeteer from 'puppeteer';
(async () => {
	const browser = await puppeteer.launch();
	const page = await browser.newPage();
	let currentURL;
	page.waitForSelector('img').then(() =>
		console.log('First URL with image: ' + currentURL)
	);
	for (currentURL of [
		'https://example.com',
		'https://google.com',
		'https://bbc.com'
	]) {
		await page.goto(currentURL);
	}
	await browser.close();
})();
```

[

Previous

](https://pptr.dev/api/puppeteer.page.waitforresponse)
