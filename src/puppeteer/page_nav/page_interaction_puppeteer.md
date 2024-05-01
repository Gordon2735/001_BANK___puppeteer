# Page interactions

Puppeteer allows you interact with the pages in various ways.

## Locators[​](https://pptr.dev/guides/page-interactions#locators 'Direct link to Locators')

Locators is a new, experimental API that combines the functionalities of waiting and actions. With additional precondition checks, it enables automatic retries for failed actions, resulting in more reliable and less flaky automation scripts.

note

Locators API is experimental and we will not follow semver for breaking changes in the Locators API.

### Use cases[​](https://pptr.dev/guides/page-interactions#use-cases 'Direct link to Use cases')

#### Waiting for an element[​](https://pptr.dev/guides/page-interactions#waiting-for-an-element 'Direct link to Waiting for an element')

```typescript
await page.locator('button').wait();
```

The following preconditions are automatically checked:

-   Waits for the element to become [visible](https://pptr.dev/api/puppeteer.elementhandle.isvisible/) or hidden.

#### Waiting for a function[​](https://pptr.dev/guides/page-interactions#waiting-for-a-function 'Direct link to Waiting for a function')

```typescript
await page
	.locator(() => {
		let resolve!: (node: HTMLCanvasElement) => void;
		const promise = new Promise((res) => {
			return (resolve = res);
		});
		const observer = new MutationObserver((records) => {
			for (const record of records) {
				if (record.target instanceof HTMLCanvasElement) {
					resolve(record.target);
				}
			}
		});
		observer.observe(document);
		return promise;
	})
	.wait();
```

#### Clicking an element[​](https://pptr.dev/guides/page-interactions#clicking-an-element 'Direct link to Clicking an element')

```typescript
await page.locator('button').click();
```

The following preconditions are automatically checked:

-   Ensures the element is in the viewport.
-   Waits for the element to become [visible](https://pptr.dev/api/puppeteer.elementhandle.isvisible/) or hidden.
-   Waits for the element to become enabled.
-   Waits for the element to have a stable bounding box over two consecutive animation frames.

#### Clicking an element matching a criteria[​](https://pptr.dev/guides/page-interactions#clicking-an-element-matching-a-criteria 'Direct link to Clicking an element matching a criteria')

```typescript
await page
	.locator('button')
	.filter((button) => !button.disabled)
	.click();
```

The following preconditions are automatically checked:

-   Ensures the element is in the viewport.
-   Waits for the element to become [visible](https://pptr.dev/api/puppeteer.elementhandle.isvisible/) or hidden.
-   Waits for the element to become enabled.
-   Waits for the element to have a stable bounding box over two consecutive animation frames.

#### Filling out an input[​](https://pptr.dev/guides/page-interactions#filling-out-an-input 'Direct link to Filling out an input')

```typescript
await page.locator('input').fill('value');
```

Automatically detects the input type and choose an appropriate way to fill it out with the provided value.

The following preconditions are automatically checked:

-   Ensures the element is in the viewport.
-   Waits for the element to become [visible](https://pptr.dev/api/puppeteer.elementhandle.isvisible/) or hidden.
-   Waits for the element to become enabled.
-   Waits for the element to have a stable bounding box over two consecutive animation frames.

#### Retrieving an element property[​](https://pptr.dev/guides/page-interactions#retrieving-an-element-property 'Direct link to Retrieving an element property')

```typescript
const enabled = await page
	.locator('button')
	.map((button) => !button.disabled)
	.wait();
```

#### Hover over an element[​](https://pptr.dev/guides/page-interactions#hover-over-an-element 'Direct link to Hover over an element')

```typescript
await page.locator('div').hover();
```

The following preconditions are automatically checked:

-   Ensures the element is in the viewport.
-   Waits for the element to become [visible](https://pptr.dev/api/puppeteer.elementhandle.isvisible/) or hidden.
-   Waits for the element to have a stable bounding box over two consecutive animation frames.

#### Scroll an element[​](https://pptr.dev/guides/page-interactions#scroll-an-element 'Direct link to Scroll an element')

```typescript
await page.locator('div').scroll({ scrollLeft: 10, scrollTop: 20 });
```

The following preconditions are automatically checked:

-   Ensures the element is in the viewport.
-   Waits for the element to become [visible](https://pptr.dev/api/puppeteer.elementhandle.isvisible/) or hidden.
-   Waits for the element to have a stable bounding box over two consecutive animation frames.

### Configuring locators[​](https://pptr.dev/guides/page-interactions#configuring-locators 'Direct link to Configuring locators')

Locators can be configured to tune configure the preconditions and other other options:

```typescript
await page
	.locator('button')
	.setEnsureElementIsInTheViewport(false)
	.setTimeout(0)
	.setVisibility(null)
	.setWaitForEnabled(false)
	.setWaitForStableBoundingBox(false)
	.click();
```

### Getting locator events[​](https://pptr.dev/guides/page-interactions#getting-locator-events 'Direct link to Getting locator events')

Currently, locators support a single event that notifies you when the locator is about to perform the action:

```typescript
let willClick = false;
await page
	.locator('button')
	.on(LocatorEvent.Action, () => {
		willClick = true;
	})
	.click();
```

This event can be used for logging/debugging or other purposes. The event might fire multiple times if the locator retries the action.

## Query Selectors[​](https://pptr.dev/guides/page-interactions#query-selectors 'Direct link to Query Selectors')

Queries are the primary mechanism for interacting with the DOM on your site. For example, a typical workflow goes like:

```typescript
// Import puppeteer
import puppeteer from 'puppeteer';
(async () => {
	// Launch the browser
	const browser = await puppeteer.launch(); // Create a page
	const page = await browser.newPage(); // Go to your site
	await page.goto('YOUR_SITE'); // Query for an element handle.
	const element = await page.waitForSelector('div > .class-name'); // Do something with element...
	await element.click(); // Just an example.
	// Dispose of handle
	await element.dispose(); // Close browser.
	await browser.close();
})();
```

### `P` Selectors[​](https://pptr.dev/guides/page-interactions#p-selectors 'Direct link to p-selectors')

Puppeteer uses a superset of the CSS selector syntax for querying. We call this syntax _P selectors_ and it's supercharged with extra capabilities such as deep combinators and text selection.

caution

Although P selectors look like real CSS selectors (we intentionally designed it this way), they should not be used for actually CSS styling. They are designed only for Puppeteer.

note

P selectors only work on the first "depth" of selectors; for example, `:is(div >>> a)` will not work.

#### `>>>` and `>>>>` combinators[​](https://pptr.dev/guides/page-interactions#-and--combinators 'Direct link to -and--combinators')

The `>>>` and `>>>>` are called _deep descendent_ and _deep_ combinators respectively. Both combinators have the effect of going into shadow hosts with `>>>` going into every shadow host under a node and `>>>>` going into the immediate one (if the node is a shadow host; otherwise, it's a no-op).

note

A common question is when should `>>>>` be chosen over `>>>` considering the flexibility of `>>>`. A similar question can be asked about `>` and a space; choose `>` if you do not need to query all elements under a given node and a space otherwise. This answer extends to `>>>>` (`>`) and `>>>` (space) naturally.

##### Example[​](https://pptr.dev/guides/page-interactions#example 'Direct link to Example')

Suppose we have the markup

```html
<custom-element>
	<template shadowrootmode="open"> <slot></slot> </template>
	<custom-element>
		<template shadowrootmode="open"> <slot></slot> </template>
		<custom-element>
			<template shadowrootmode="open"> <slot></slot> </template>
			<h2>Light content</h2>
		</custom-element>
	</custom-element></custom-element
>
```

> Note: `<template shadowrootmode="open">` is not supported on Firefox. You can read more about it [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template#attributes).

Then `custom-element >>> h2` will return `h2`, but `custom-element >>>> h2` will return nothing since the inner `h2` is in a deeper shadow root.

#### `P`\-elements[​](https://pptr.dev/guides/page-interactions#p-elements 'Direct link to p-elements')

`P` elements are [pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements) with a `-p` vendor prefix. It allows you to enhance your selectors with Puppeteer-specific query engines such as XPath, text queries, and ARIA.

##### Text selectors (`-p-text`)[​](https://pptr.dev/guides/page-interactions#text-selectors--p-text 'Direct link to text-selectors--p-text')

Text selectors will select "minimal" elements containing the given text, even within (open) shadow roots. Here, "minimum" means the deepest elements that contain a given text, but not their parents (which technically will also contain the given text).

###### Example[​](https://pptr.dev/guides/page-interactions#example-1 'Direct link to Example')

```typescript
const element = await page.waitForSelector('div ::-p-text(My name is Jun)'); // You can also use escapes.
const element = await page.waitForSelector(
	':scope >>> ::-p-text(My name is Jun \\(pronounced like "June"\\))'
); // or quotes
const element = await page.waitForSelector(
	'div >>>> ::-p-text("My name is Jun (pronounced like \\"June\\")"):hover'
);
```

##### XPath selectors (`-p-xpath`)[​](https://pptr.dev/guides/page-interactions#xpath-selectors--p-xpath 'Direct link to xpath-selectors--p-xpath')

XPath selectors will use the browser's native [`Document.evaluate`](https://developer.mozilla.org/en-US/docs/Web/API/Document/evaluate) to query for elements.

###### Example[​](https://pptr.dev/guides/page-interactions#example-2 'Direct link to Example')

```typescript
const element = await page.waitForSelector('::-p-xpath(h2)');
```

##### ARIA selectors (`-p-aria`)[​](https://pptr.dev/guides/page-interactions#aria-selectors--p-aria 'Direct link to aria-selectors--p-aria')

ARIA selectors can be used to find elements with a given ARIA label. These labels are computed using Chrome's internal representation.

###### Example[​](https://pptr.dev/guides/page-interactions#example-3 'Direct link to Example')

```typescript
const node = await page.waitForSelector('::-p-aria(Submit)');
const node = await page.waitForSelector(
	'::-p-aria([name="Click me"][role="button"])'
);
```

#### Custom selectors[​](https://pptr.dev/guides/page-interactions#custom-selectors 'Direct link to Custom selectors')

Puppeteer provides users the ability to add their own query selectors to Puppeteer using [Puppeteer.registerCustomQueryHandler](https://pptr.dev/api/puppeteer.registercustomqueryhandler). This is useful for creating custom selectors based on framework objects or other vendor-specific objects.

##### Custom Selectors[​](https://pptr.dev/guides/page-interactions#custom-selectors-1 'Direct link to Custom Selectors')

You can register a custom query handler that allows you to create custom selectors. For example, define a query handler for `getById` selectors:

```typescript
Puppeteer.registerCustomQueryHandler('getById', {
	queryOne: (elementOrDocument, selector) => {
		return elementOrDocument.querySelector(
			`[id="${CSS.escape(selector)}"]`
		);
	}, // Note: for demonstation perpose only `id` should be page unique
	queryAll: (elementOrDocument, selector) => {
		return elementOrDocument.querySelectorAll(
			`[id="${CSS.escape(selector)}"]`
		);
	}
});
```

You can now use it as following:

```typescript
const node = await page.waitForSelector('::-p-getById(elementId)'); // OR used in conjunction with other selectorsconst moreSpecific
Node = await page.waitForSelector('.side-bar ::-p-getById(elementId)');
```

##### Custom framework components selector[​](https://pptr.dev/guides/page-interactions#custom-framework-components-selector 'Direct link to Custom framework components selector')

caution

Be careful when relying on internal APIs of libraries or frameworks. They can change at any time.

Find Vue components by name by using Vue internals for querying:

```typescript
Puppeteer.registerCustomQueryHandler('vue', {
	queryOne: (element, name) => {
		const walker = document.createTreeWalker(
			element,
			NodeFilter.SHOW_ELEMENT
		);
		do {
			const currentNode = walker.currentNode;
			if (
				currentNode.__vnode?.ctx?.type?.name.toLowerCase() ===
				name.toLocaleLowerCase()
			) {
				return currentNode;
			}
		} while (walker.nextNode());
		return null;
	}
});
```

Query the Vue component as following:

```typescript
const element = await page.$('::-p-vue(MyComponent)');
```

##### Web Components[​](https://pptr.dev/guides/page-interactions#web-components 'Direct link to Web Components')

Web Components create their own tag so you can query them by the tag name:

```typescript
const element = await page.$('my-web-component');
```

Extend `HTMLElementTagNameMap` to define types for custom tags. This allows Puppeteer to infer the return type for the ElementHandle:

```typescript
declare global {
	interface HTMLElementTagNameMap {
		'my-web-component': MyWebComponent;
	}
}
```

## Query Selectors (legacy)[​](https://pptr.dev/guides/page-interactions#query-selectors-legacy 'Direct link to Query Selectors (legacy)')

caution

While we maintin prefixed selectors, the recommended way is to use the selector syntax documented above.

Queries are the primary mechanism for interacting with the DOM on your site. For example, a typical workflow goes like:

```typescript
// Import puppeteer
import puppeteer from 'puppeteer';
(async () => {
	// Launch the browser
	const browser = await puppeteer.launch();
	// Create a page
	const page = await browser.newPage();
	// Go to your site
	await page.goto('YOUR_SITE');
	// Query for an element handle.
	const element = await page.waitForSelector('div > .class-name');
	// Do something with element...
	await element.click(); // Just an example.
	// Dispose of handle
	await element.dispose();
	// Close browser.
	await browser.close();
})();
```

### CSS[​](https://pptr.dev/guides/page-interactions#css 'Direct link to CSS')

CSS selectors follow the CSS spec of the browser being automated. We provide some basic type deduction for CSS selectors (such as `HTMLInputElement` for `input`), but any selector that contains no type information (such as `.class-name`) will need to be coerced manually using TypeScript's `as` coercion mechanism.

#### Example[​](https://pptr.dev/guides/page-interactions#example-4 'Direct link to Example')

```typescript
// Automatic
const element = await page.waitForSelector('div > input'); // Manual
const element = (await page.waitForSelector(
	'div > .class-name-for-input'
)) as HTMLInputElement;
```

### Built-in selectors[​](https://pptr.dev/guides/page-interactions#built-in-selectors 'Direct link to Built-in selectors')

Built-in selectors are Puppeteer's own class of selectors for doing things CSS cannot. Every built-in selector starts with a prefix `.../` to assist Puppeteer in distinguishing between CSS selectors and a built-in.

#### Text selectors (`text/`)[​](https://pptr.dev/guides/page-interactions#text-selectors-text 'Direct link to text-selectors-text')

Text selectors will select "minimal" elements containing the given text, even within (open) shadow roots. Here, "minimum" means the deepest elements that contain a given text, but not their parents (which technically will also contain the given text).

##### Example[​](https://pptr.dev/guides/page-interactions#example-5 'Direct link to Example')

```typescript
// Note we usually need type coercion since the type cannot be deduced, but for text selectors, `instanceof` checks may be better for runtime validation.
const element = await page.waitForSelector('text/My name is Jun');
```

#### XPath selectors (`xpath/`)[​](https://pptr.dev/guides/page-interactions#xpath-selectors-xpath 'Direct link to xpath-selectors-xpath')

XPath selectors will use the browser's native [`Document.evaluate`](https://developer.mozilla.org/en-US/docs/Web/API/Document/evaluate) to query for elements.

##### Example[​](https://pptr.dev/guides/page-interactions#example-6 'Direct link to Example')

```typescript
const node = await page.waitForSelector('aria/Button name');
```

#### Pierce selectors (`pierce/`)[​](https://pptr.dev/guides/page-interactions#pierce-selectors-pierce 'Direct link to pierce-selectors-pierce')

Pierce selectors will run the `querySelector*` API on the document and all shadow roots to find an element.

danger

Selectors will **not** _partially_ pierce through shadow roots. See the examples below.

##### Example[​](https://pptr.dev/guides/page-interactions#example-8 'Direct link to Example')

Suppose the HTML is

```html
<div>
	<custom-element> <div></div> </custom-element>
</div>
```

Then

```typescript
// This will be two elements because of the outer and inner div.
expect((await page.$$('pierce/div')).length).toBe(2);
// Partial piercing doesn't work.
expect((await page.$$('pierce/div div')).length).toBe(0);
```

### Custom selectors[​](https://pptr.dev/guides/page-interactions#custom-selectors-2 'Direct link to Custom selectors')

Puppeteer provides users the ability to add their own query selectors to Puppeteer using [Puppeteer.registerCustomQueryHandler](https://pptr.dev/api/puppeteer.registercustomqueryhandler). This is useful for creating custom selectors based on framework objects or other vendor-specific objects.

[

Previous

](https://pptr.dev/guides/browser-management)
