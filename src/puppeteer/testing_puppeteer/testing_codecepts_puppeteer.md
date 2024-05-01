## Puppeteer

**Extends Helper**

Uses [Google Chrome's Puppeteer (opens new window)](https://github.com/GoogleChrome/puppeteer) library to run tests inside headless Chrome. Browser control is executed via DevTools Protocol (instead of Selenium). This helper works with a browser out of the box with no additional tools required to install.

Requires `puppeteer` or `puppeteer-core` package to be installed.

```bash
npm i puppeteer --save
```

or

```bash
npm i puppeteer-core --save
```

Using `puppeteer-core` package, will prevent the download of browser binaries and allow connecting to an existing browser installation or for connecting to a remote one.

> Experimental Firefox support [can be activated (opens new window)](https://codecept.io/helpers/Puppeteer-firefox).

## [#](https://codecept.io/helpers/Puppeteer/#configuration) Configuration

This helper should be configured in codecept.conf.js

Type: [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)

### [#](https://codecept.io/helpers/Puppeteer/#properties) Properties

-   `url` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** base url of website to be tested
-   `basicAuth` **[object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** (optional) the basic authentication to pass to base url. Example: {username: 'username', password: 'password'}
-   `show` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** show Google Chrome window for debug.
-   `restart` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** restart browser between tests.
-   `disableScreenshots` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** don't save screenshot on failure.
-   `fullPageScreenshots` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** make full page screenshots on failure.
-   `uniqueScreenshotNames` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** option to prevent screenshot override if you have scenarios with the same name in different suites.
-   `trace` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** record [tracing information (opens new window)](https://pptr.dev/api/puppeteer.tracing) with screenshots.
-   `keepTraceForPassedTests` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** save trace for passed tests.
-   `keepBrowserState` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** keep browser state between tests when `restart` is set to false.
-   `keepCookies` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** keep cookies between tests when `restart` is set to false.
-   `waitForAction` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** how long to wait after click, doubleClick or PressKey actions in ms. Default: 100.
-   `waitForNavigation` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** when to consider navigation succeeded. Possible options: `load`, `domcontentloaded`, `networkidle0`, `networkidle2`. See [Puppeteer API (opens new window)](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pagewaitfornavigationoptions). Array values are accepted as well.
-   `pressKeyDelay` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** delay between key presses in ms. Used when calling Puppeteers page.type(...) in fillField/appendField
-   `getPageTimeout` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** config option to set maximum navigation time in milliseconds. If the timeout is set to 0, then timeout will be disabled.
-   `waitForTimeout` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** default wait\* timeout in ms.
-   `windowSize` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** default window size. Set a dimension in format WIDTHxHEIGHT like `640x480`.
-   `userAgent` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** user-agent string.
-   `manualStart` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** do not start browser before a test, start it manually inside a helper with `this.helpers["Puppeteer"]._startBrowser()`.
-   `browser` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** can be changed to `firefox` when using [puppeteer-firefox (opens new window)](https://codecept.io/helpers/Puppeteer-firefox).
-   `chrome` **[object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** pass additional [Puppeteer run options (opens new window)](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#puppeteerlaunchoptions).
-   `highlightElement` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)?** highlight the interacting elements. Default: false. Note: only activate under verbose mode (--verbose).

#### [#](https://codecept.io/helpers/Puppeteer/#trace-recording-customization) Trace Recording Customization

Trace recording provides complete information on test execution and includes screenshots, and network requests logged during run. Traces will be saved to `output/trace`

-   `trace`: enables trace recording for failed tests; trace are saved into `output/trace` folder
-   `keepTraceForPassedTests`: - save trace for passed tests

#### [#](https://codecept.io/helpers/Puppeteer/#example-1-wait-for-0-network-connections) Example #1: Wait for 0 network connections.

```javascript
{
   helpers: {
     Puppeteer : {
       url: "http://localhost",
       restart: false,
       waitForNavigation: "networkidle0",
       waitForAction: 500
     }
   }
}
```

#### [#](https://codecept.io/helpers/Puppeteer/#example-2-wait-for-domcontentloaded-event-and-0-network-connections) Example #2: Wait for DOMContentLoaded event and 0 network connections

```javascript
{
   helpers: {
     Puppeteer : {
       url: "http://localhost",
       restart: false,
       waitForNavigation: [ "domcontentloaded", "networkidle0" ],
       waitForAction: 500
     }
   }
}
```

#### [#](https://codecept.io/helpers/Puppeteer/#example-3-debug-in-window-mode) Example #3: Debug in window mode

```javascript
{
   helpers: {
     Puppeteer : {
       url: "http://localhost",
       show: true
     }
   }
}
```

#### [#](https://codecept.io/helpers/Puppeteer/#example-4-connect-to-remote-browser-by-specifying-websocket-endpoint) Example #4: Connect to remote browser by specifying [websocket endpoint (opens new window)](https://chromedevtools.github.io/devtools-protocol/#how-do-i-access-the-browser-target)

```javascript
{
   helpers: {
     Puppeteer: {
       url: "http://localhost",
       chrome: {
         browserWSEndpoint: "ws://localhost:9222/devtools/browser/c5aa6160-b5bc-4d53-bb49-6ecb36cd2e0a"
       }
     }
   }
}
```

> Note: When connecting to remote browser `show` and specific `chrome` options (e.g. `headless` or `devtools`) are ignored.

#### [#](https://codecept.io/helpers/Puppeteer/#example-5-target-url-with-provided-basic-authentication) Example #5: Target URL with provided basic authentication

```javascript
{
   helpers: {
     Puppeteer : {
       url: 'http://localhost',
       basicAuth: {username: 'username', password: 'password'},
       show: true
     }
   }
}
```

#### [#](https://codecept.io/helpers/Puppeteer/#troubleshooting) Troubleshooting

Error Message: `No usable sandbox!`

When running Puppeteer on CI try to disable sandbox if you see that message

```javascript
helpers: {
 Puppeteer: {
    url: 'http://localhost',
    show: false,
    chrome: {
      args: ['--no-sandbox', '--disable-setuid-sandbox']
    }
  },
}
```

## [#](https://codecept.io/helpers/Puppeteer/#access-from-helpers) Access From Helpers

Receive Puppeteer client from a custom helper by accessing `browser` for the Browser object or `page` for the current Page object:

```javascript
const { browser } = this.helpers.Puppeteer;
await browser.pages(); // List of pages in the browser

const { page } = this.helpers.Puppeteer;
await page.url(); // Get the url of the current page
```

## [#](https://codecept.io/helpers/Puppeteer/#methods) Methods

### [#](https://codecept.io/helpers/Puppeteer/#parameters) Parameters

-   `config`

### [#](https://codecept.io/helpers/Puppeteer/#addpopuplistener) \_addPopupListener

Add the 'dialog' event listener to a page

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-2) Parameters

-   `page`

### [#](https://codecept.io/helpers/Puppeteer/#getpageurl) \_getPageUrl

Gets page URL including hash.

### [#](https://codecept.io/helpers/Puppeteer/#locate) \_locate

Get elements by different locator types, including strict locator Should be used in custom helpers:

```javascript
const elements = await this.helpers['Puppeteer']._locate({ name: 'password' });
```

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-3) Parameters

-   `locator`

### [#](https://codecept.io/helpers/Puppeteer/#locatecheckable) \_locateCheckable

Find a checkbox by providing human-readable text: NOTE: Assumes the checkable element exists

```javascript
this.helpers['Puppeteer']._locateCheckable('I agree with terms and conditions')
	.then; // ...
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-4) Parameters

-   `locator`
-   `providedContext`

### [#](https://codecept.io/helpers/Puppeteer/#locateclickable) \_locateClickable

Find a clickable element by providing human-readable text:

```javascript
this.helpers['Puppeteer']._locateClickable('Next page').then; // ...
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-5) Parameters

-   `locator`

### [#](https://codecept.io/helpers/Puppeteer/#locatefields) \_locateFields

Find field elements by providing human-readable text:

```javascript
this.helpers['Puppeteer']._locateFields('Your email').then; // ...
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-6) Parameters

-   `locator`

### [#](https://codecept.io/helpers/Puppeteer/#setpage) \_setPage

Set current page

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-7) Parameters

-   `page` **[object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** page to set

### [#](https://codecept.io/helpers/Puppeteer/#acceptpopup) acceptPopup

Accepts the active JavaScript native popup window, as created by window.alert|window.confirm|window.prompt. Don't confuse popups with modal windows, as created by [various libraries (opens new window)](http://jster.net/category/windows-modals-popups).

### [#](https://codecept.io/helpers/Puppeteer/#amacceptingpopups) amAcceptingPopups

Set the automatic popup response to Accept. This must be set before a popup is triggered.

```javascript
I.amAcceptingPopups();
I.click('#triggerPopup');
I.acceptPopup();
```

### [#](https://codecept.io/helpers/Puppeteer/#amcancellingpopups) amCancellingPopups

Set the automatic popup response to Cancel/Dismiss. This must be set before a popup is triggered.

```javascript
I.amCancellingPopups();
I.click('#triggerPopup');
I.cancelPopup();
```

### [#](https://codecept.io/helpers/Puppeteer/#amonpage) amOnPage

Opens a web page in a browser. Requires relative or absolute url. If url starts with `/`, opens a web page of a site defined in `url` config parameter.

```javascript
I.amOnPage('/'); // opens main page of website
I.amOnPage('https://github.com'); // opens github
I.amOnPage('/login'); // opens a login page
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-8) Parameters

-   `url` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** url path or global url.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#appendfield) appendField

Appends text to a input field or textarea. Field is located by name, label, CSS or XPath

```javascript
I.appendField('#myTextField', 'appended');
// typing secret
I.appendField('password', secret('123456'));
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-9) Parameters

-   `field` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by label|name|CSS|XPath|strict locator
-   `value` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** text value to append.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#attachfile) attachFile

> ⚠ There is an [issue with file upload in Puppeteer 2.1.0 & 2.1.1 (opens new window)](https://github.com/puppeteer/puppeteer/issues/5420), downgrade to 2.0.0 if you face it.

Attaches a file to element located by label, name, CSS or XPath Path to file is relative current codecept directory (where codecept.conf.ts or codecept.conf.js is located). File will be uploaded to remote system (if tests are running remotely).

```javascript
I.attachFile('Avatar', 'data/avatar.jpg');
I.attachFile('form input[name=avatar]', 'data/avatar.jpg');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-10) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** field located by label|name|CSS|XPath|strict locator.
-   `pathToFile` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** local file path relative to codecept.conf.ts or codecept.conf.js config file.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#blur) blur

Remove focus from a text input, button, etc. Calls [blur (opens new window)](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/focus) on the element.

Examples:

```javascript
I.blur('.text-area');
```

```javascript
//element `#product-tile` is focused
I.see('#add-to-cart-btn');
I.blur('#product-tile');
I.dontSee('#add-to-cart-btn');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-11) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** field located by label|name|CSS|XPath|strict locator.
-   `options` **any?** Playwright only: [Additional options (opens new window)](https://playwright.dev/docs/api/class-locator#locator-blur) for available options object as 2nd argument.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#cancelpopup) cancelPopup

Dismisses the active JavaScript popup, as created by window.alert|window.confirm|window.prompt.

### [#](https://codecept.io/helpers/Puppeteer/#checkoption) checkOption

Selects a checkbox or radio button. Element is located by label or name or CSS or XPath.

The second parameter is a context (CSS or XPath locator) to narrow the search.

```javascript
I.checkOption('#agree');
I.checkOption('I Agree to Terms and Conditions');
I.checkOption('agree', '//form');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-12) Parameters

-   `field` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** checkbox located by label | name | CSS | XPath | strict locator.
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)? | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** (optional, `null` by default) element located by CSS | XPath | strict locator.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#clearcookie) clearCookie

Clears a cookie by name, if none provided clears all cookies.

```javascript
I.clearCookie();
I.clearCookie('test'); // Playwright currently doesn't support clear a particular cookie name
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-13) Parameters

-   `name`
-   `cookie` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** (optional, `null` by default) cookie name

### [#](https://codecept.io/helpers/Puppeteer/#clearfield) clearField

Clears a `<textarea>` or text `<input>` element's value.

```javascript
I.clearField('Email');
I.clearField('user[email]');
I.clearField('#email');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-14) Parameters

-   `field`
-   `editable` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** field located by label|name|CSS|XPath|strict locator.

Returns **void** automatically synchronized promise through #recorder.

### [#](https://codecept.io/helpers/Puppeteer/#click) click

Perform a click on a link or a button, given by a locator. If a fuzzy locator is given, the page will be searched for a button, link, or image matching the locator string. For buttons, the "value" attribute, "name" attribute, and inner text are searched. For links, the link text is searched. For images, the "alt" attribute and inner text of any parent links are searched.

The second parameter is a context (CSS or XPath locator) to narrow the search.

```javascript
// simple link
I.click('Logout');
// button of form
I.click('Submit');
// CSS button
I.click('#form input[type=submit]');
// XPath
I.click('//form/*[@type=submit]');
// link in context
I.click('Logout', '#nav');
// using strict locator
I.click({ css: 'nav a.login' });
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-15) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** clickable link or button located by text, or any element located by CSS|XPath|strict locator.
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)? | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object) | null)** (optional, `null` by default) element to search in CSS|XPath|Strict locator.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#clicklink) clickLink

Performs a click on a link and waits for navigation before moving on.

```javascript
I.clickLink('Logout', '#nav');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-16) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** clickable link or button located by text, or any element located by CSS|XPath|strict locator
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)? | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** (optional, `null` by default) element to search in CSS|XPath|Strict locator

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#closecurrenttab) closeCurrentTab

Close current tab and switches to previous.

```javascript
I.closeCurrentTab();
```

### [#](https://codecept.io/helpers/Puppeteer/#closeothertabs) closeOtherTabs

Close all tabs except for the current one.

```javascript
I.closeOtherTabs();
```

### [#](https://codecept.io/helpers/Puppeteer/#dontsee) dontSee

Opposite to `see`. Checks that a text is not present on a page. Use context parameter to narrow down the search.

```javascript
I.dontSee('Login'); // assume we are already logged in.
I.dontSee('Login', '.nav'); // no login inside .nav element
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-17) Parameters

-   `text` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** which is not present.
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))?** (optional) element located by CSS|XPath|strict locator in which to perfrom search.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#dontseecheckboxischecked) dontSeeCheckboxIsChecked

Verifies that the specified checkbox is not checked.

```javascript
I.dontSeeCheckboxIsChecked('#agree'); // located by ID
I.dontSeeCheckboxIsChecked('I agree to terms'); // located by label
I.dontSeeCheckboxIsChecked('agree'); // located by name
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-18) Parameters

-   `field` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by label|name|CSS|XPath|strict locator.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#dontseecookie) dontSeeCookie

Checks that cookie with given name does not exist.

```javascript
I.dontSeeCookie('auth'); // no auth cookie
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-19) Parameters

-   `name` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** cookie name.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#dontseecurrenturlequals) dontSeeCurrentUrlEquals

Checks that current url is not equal to provided one. If a relative url provided, a configured url will be prepended to it.

```javascript
I.dontSeeCurrentUrlEquals('/login'); // relative url are ok
I.dontSeeCurrentUrlEquals('http://mysite.com/login'); // absolute urls are also ok
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-20) Parameters

-   `url` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** value to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#dontseeelement) dontSeeElement

Opposite to `seeElement`. Checks that element is not visible (or in DOM)

```javascript
I.dontSeeElement('.modal'); // modal is not shown
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-21) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|Strict locator.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#dontseeelementindom) dontSeeElementInDOM

Opposite to `seeElementInDOM`. Checks that element is not on page.

```javascriptI.dontSeeElementInDOM('.nav'); // checks that element is not on page visible or not

```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-22) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|Strict locator.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#dontseeincurrenturl) dontSeeInCurrentUrl

Checks that current url does not contain a provided fragment.

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-23) Parameters

-   `url` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** value to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#dontseeinfield) dontSeeInField

Checks that value of input field or textarea doesn't equal to given value Opposite to `seeInField`.

```javascript
I.dontSeeInField('email', 'user@user.com'); // field by name
I.dontSeeInField({ css: 'form input.email' }, 'user@user.com'); // field by CSS
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-24) Parameters

-   `field` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by label|name|CSS|XPath|strict locator.
-   `value` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** value to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#dontseeinsource) dontSeeInSource

Checks that the current page does not contains the given string in its raw source code.

```javascript
I.dontSeeInSource('<!--'); // no comments in source
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-25) Parameters

-   `text`
-   `value` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#dontseeintitle) dontSeeInTitle

Checks that title does not contain text.

```javascript
I.dontSeeInTitle('Error');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-26) Parameters

-   `text` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** value to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#dontseetraffic) dontSeeTraffic

Verifies that a certain request is not part of network traffic.

Examples:

```javascript
I.dontSeeTraffic({
	name: 'Unexpected API Call',
	url: 'https://api.example.com'
});
I.dontSeeTraffic({
	name: 'Unexpected API Call of "user" endpoint',
	url: /api.example.com.*user/
});
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-27) Parameters

-   `opts` **[Object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** options when checking the traffic network.
    -   `opts.name` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** A name of that request. Can be any value. Only relevant to have a more meaningful error message in case of fail.
    -   `opts.url` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [RegExp (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/RegExp))** Expected URL of request in network traffic. Can be a string or a regular expression.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#doubleclick) doubleClick

Performs a double-click on an element matched by link|button|label|CSS or XPath. Context can be specified as second parameter to narrow search.

```javascript
I.doubleClick('Edit');
I.doubleClick('Edit', '.actions');
I.doubleClick({ css: 'button.accept' });
I.doubleClick('.btn.edit');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-28) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** clickable link or button located by text, or any element located by CSS|XPath|strict locator.
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)? | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** (optional, `null` by default) element to search in CSS|XPath|Strict locator.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#downloadfile) downloadFile

This method is **deprecated**.

Please use `handleDownloads()` instead.

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-29) Parameters

-   `locator`
-   `customName`

### [#](https://codecept.io/helpers/Puppeteer/#draganddrop) dragAndDrop

Drag an item to a destination element.

```javascript
I.dragAndDrop('#dragHandle', '#container');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-30) Parameters

-   `srcElement` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|strict locator.
-   `destElement` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|strict locator.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#dragslider) dragSlider

Drag the scrubber of a slider to a given position For fuzzy locators, fields are matched by label text, the "name" attribute, CSS, and XPath.

```javascript
I.dragSlider('#slider', 30);
I.dragSlider('#slider', -70);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-31) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by label|name|CSS|XPath|strict locator.
-   `offsetX` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** position to drag.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#executeasyncscript) executeAsyncScript

Asynchronous scripts can also be executed with `executeScript` if a function returns a Promise. Executes async script on page. Provided function should execute a passed callback (as first argument) to signal it is finished.

Example: In Vue.js to make components completely rendered we are waiting for [nextTick (opens new window)](https://vuejs.org/v2/api/#Vue-nextTick).

```javascript
I.executeAsyncScript(function (done) {
	Vue.nextTick(done); // waiting for next tick
});
```

By passing value to `done()` function you can return values. Additional arguments can be passed as well, while `done` function is always last parameter in arguments list.

```javascript
let val = await I.executeAsyncScript(function(url, done) {
  // in browser context
  $.ajax(url, { success: (data) => done(data); }
}, 'http://ajax.callback.url/');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-32) Parameters

-   `args` **...any** to be passed to function.
-   `fn` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [function (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function))** function to be executed in browser context.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<any>** script return value

### [#](https://codecept.io/helpers/Puppeteer/#executescript) executeScript

If a function returns a Promise, tt will wait for its resolution.

Executes sync script on a page. Pass arguments to function as additional parameters. Will return execution result to a test. In this case you should use async function and await to receive results.

Example with jQuery DatePicker:

```javascript
// change date of jQuery DatePicker
I.executeScript(function () {
	// now we are inside browser context
	$('date').datetimepicker('setDate', new Date());
});
```

Can return values. Don't forget to use `await` to get them.

```javascript
let date = await I.executeScript(function (el) {
	// only basic types can be returned
	return $(el).datetimepicker('getDate').toString();
}, '#date'); // passing jquery selector
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-33) Parameters

-   `args` **...any** to be passed to function.
-   `fn` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [function (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function))** function to be executed in browser context.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<any>** script return value

### [#](https://codecept.io/helpers/Puppeteer/#fillfield) fillField

Fills a text field or textarea, after clearing its value, with the given string. Field is located by name, label, CSS, or XPath.

```javascript
// by label
I.fillField('Email', 'hello@world.com');
// by name
I.fillField('password', secret('123456'));
// by CSS
I.fillField('form#login input[name=username]', 'John');
// or by strict locator
I.fillField({ css: 'form#login input[name=username]' }, 'John');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-34) Parameters

-   `field` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by label|name|CSS|XPath|strict locator.
-   `value` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** text value to fill.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#flushnetworktraffics) flushNetworkTraffics

Resets all recorded network requests.

```javascript
I.flushNetworkTraffics();
```

### [#](https://codecept.io/helpers/Puppeteer/#flushwebsocketmessages) flushWebSocketMessages

Resets all recorded WS messages.

### [#](https://codecept.io/helpers/Puppeteer/#focus) focus

Calls [focus (opens new window)](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/focus) on the matching element.

Examples:

```javascript
I.dontSee('#add-to-cart-btn');
I.focus('#product-tile');
I.see('#add-to-cart-bnt');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-35) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** field located by label|name|CSS|XPath|strict locator.
-   `options` **any?** Playwright only: [Additional options (opens new window)](https://playwright.dev/docs/api/class-locator#locator-focus) for available options object as 2nd argument.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#forceclick) forceClick

Perform an emulated click on a link or a button, given by a locator. Unlike normal click instead of sending native event, emulates a click with JavaScript. This works on hidden, animated or inactive elements as well.

If a fuzzy locator is given, the page will be searched for a button, link, or image matching the locator string. For buttons, the "value" attribute, "name" attribute, and inner text are searched. For links, the link text is searched. For images, the "alt" attribute and inner text of any parent links are searched.

The second parameter is a context (CSS or XPath locator) to narrow the search.

```javascript
// simple link
I.forceClick('Logout');
// button of form
I.forceClick('Submit');
// CSS button
I.forceClick('#form input[type=submit]');
// XPath
I.forceClick('//form/*[@type=submit]');
// link in context
I.forceClick('Logout', '#nav');
// using strict locator
I.forceClick({ css: 'nav a.login' });
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-36) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** clickable link or button located by text, or any element located by CSS|XPath|strict locator.
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)? | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** (optional, `null` by default) element to search in CSS|XPath|Strict locator.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#grabattributefrom) grabAttributeFrom

Retrieves an attribute from an element located by CSS or XPath and returns it to test. Resumes test execution, so **should be used inside async with `await`** operator. If more than one element is found - attribute of first element is returned.

```javascript
let hint = await I.grabAttributeFrom('#tooltip', 'title');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-37) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `attr` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** attribute name.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>** attribute value

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#grabattributefromall) grabAttributeFromAll

Retrieves an array of attributes from elements located by CSS or XPath and returns it to test. Resumes test execution, so **should be used inside async with `await`** operator.

```javascript
let hints = await I.grabAttributeFromAll('.tooltip', 'title');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-38) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `attr` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** attribute name.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>>** attribute value

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#grabbrowserlogs) grabBrowserLogs

Get JS log from browser.

```javascript
let logs = await I.grabBrowserLogs();
console.log(JSON.stringify(logs));
```

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<any>>**

### [#](https://codecept.io/helpers/Puppeteer/#grabcookie) grabCookie

Gets a cookie object by name. If none provided gets all cookies. Resumes test execution, so **should be used inside async function with `await`** operator.

```javascript
let cookie = await I.grabCookie('auth');
assert(cookie.value, '123456');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-39) Parameters

-   `name` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** cookie name.

Returns **any** attribute valueReturns cookie in JSON format. If name not passed returns all cookies for this domain.

### [#](https://codecept.io/helpers/Puppeteer/#grabcsspropertyfrom) grabCssPropertyFrom

Grab CSS property for given locator Resumes test execution, so **should be used inside an async function with `await`** operator. If more than one element is found - value of first element is returned.

```javascript
const value = await I.grabCssPropertyFrom('h3', 'font-weight');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-40) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `cssProperty` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** CSS property name.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>** CSS value

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#grabcsspropertyfromall) grabCssPropertyFromAll

Grab array of CSS properties for given locator Resumes test execution, so **should be used inside an async function with `await`** operator.

```javascript
const values = await I.grabCssPropertyFromAll('h3', 'font-weight');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-41) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `cssProperty` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** CSS property name.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>>** CSS value

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#grabcurrenturl) grabCurrentUrl

Get current URL from browser. Resumes test execution, so should be used inside an async function.

```javascript
let url = await I.grabCurrentUrl();
console.log(`Current URL is [${url}]`);
```

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>** current URL

### [#](https://codecept.io/helpers/Puppeteer/#grabdatafromperformancetiming) grabDataFromPerformanceTiming

Grab the data from performance timing using Navigation Timing API. The returned data will contain following things in ms:

-   responseEnd,
-   domInteractive,
-   domContentLoadedEventEnd,
-   loadEventEnd Resumes test execution, so **should be used inside an async function with `await`** operator.

```javascript
await I.amOnPage('https://example.com');
let data = await I.grabDataFromPerformanceTiming();
//Returned data
{ // all results are in [ms]
  responseEnd: 23,
  domInteractive: 44,
  domContentLoadedEventEnd: 196,
  loadEventEnd: 241
}
```

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#grabelementboundingrect) grabElementBoundingRect

Grab the width, height, location of given locator. Provide `width` or `height`as second param to get your desired prop. Resumes test execution, so **should be used inside an async function with `await`** operator.

Returns an object with `x`, `y`, `width`, `height` keys.

```javascript
const value = await I.grabElementBoundingRect('h3');
// value is like { x: 226.5, y: 89, width: 527, height: 220 }
```

To get only one metric use second parameter:

```javascript
const width = await I.grabElementBoundingRect('h3', 'width');
// width == 527
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-42) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `prop`
-   `elementSize` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** x, y, width or height of the given element.

Returns **([Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<DOMRect> | [Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)\>)** Element bounding rectangle

### [#](https://codecept.io/helpers/Puppeteer/#grabhtmlfrom) grabHTMLFrom

Retrieves the innerHTML from an element located by CSS or XPath and returns it to test. Resumes test execution, so **should be used inside async function with `await`** operator. If more than one element is found - HTML of first element is returned.

```javascript
let postHTML = await I.grabHTMLFrom('#post');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-43) Parameters

-   `locator`
-   `element` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|strict locator.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>** HTML code for an element

### [#](https://codecept.io/helpers/Puppeteer/#grabhtmlfromall) grabHTMLFromAll

Retrieves all the innerHTML from elements located by CSS or XPath and returns it to test. Resumes test execution, so **should be used inside async function with `await`** operator.

```javascript
let postHTMLs = await I.grabHTMLFromAll('.post');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-44) Parameters

-   `locator`
-   `element` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|strict locator.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>>** HTML code for an element

### [#](https://codecept.io/helpers/Puppeteer/#grabnumberofopentabs) grabNumberOfOpenTabs

Grab number of open tabs. Resumes test execution, so **should be used inside async function with `await`** operator.

```javascript
let tabs = await I.grabNumberOfOpenTabs();
```

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)\>** number of open tabs

### [#](https://codecept.io/helpers/Puppeteer/#grabnumberofvisibleelements) grabNumberOfVisibleElements

Grab number of visible elements by locator. Resumes test execution, so **should be used inside async function with `await`** operator.

```javascript
let numOfElements = await I.grabNumberOfVisibleElements('p');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-45) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|strict locator.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)\>** number of visible elements

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#grabpagescrollposition) grabPageScrollPosition

Retrieves a page scroll position and returns it to test. Resumes test execution, so **should be used inside an async function with `await`** operator.

```javascript
let { x, y } = await I.grabPageScrollPosition();
```

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<PageScrollPosition>** scroll position

### [#](https://codecept.io/helpers/Puppeteer/#grabpopuptext) grabPopupText

Grab the text within the popup. If no popup is visible then it will return null

```javascript
await I.grabPopupText();
```

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | null)>**

### [#](https://codecept.io/helpers/Puppeteer/#grabrecordednetworktraffics) grabRecordedNetworkTraffics

Grab the recording network traffics

```javascript
const traffics = await I.grabRecordedNetworkTraffics();
expect(traffics[0].url).to.equal('https://reqres.in/api/comments/1');
expect(traffics[0].response.status).to.equal(200);
expect(traffics[0].response.body).to.contain({ name: 'this was mocked' });
```

Returns **[Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)** recorded network traffics

### [#](https://codecept.io/helpers/Puppeteer/#grabsource) grabSource

Retrieves page source and returns it to test. Resumes test execution, so **should be used inside async function with `await`** operator.

```javascript
let pageSource = await I.grabSource();
```

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>** source code

### [#](https://codecept.io/helpers/Puppeteer/#grabtextfrom) grabTextFrom

Retrieves a text from an element located by CSS or XPath and returns it to test. Resumes test execution, so **should be used inside async with `await`** operator.

```javascript
let pin = await I.grabTextFrom('#pin');
```

If multiple elements found returns first element.

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-46) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>** attribute value

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#grabtextfromall) grabTextFromAll

Retrieves all texts from an element located by CSS or XPath and returns it to test. Resumes test execution, so **should be used inside async with `await`** operator.

```javascript
let pins = await I.grabTextFromAll('#pin li');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-47) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>>** attribute value

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#grabtitle) grabTitle

Retrieves a page title and returns it to test. Resumes test execution, so **should be used inside async with `await`** operator.

```javascript
let title = await I.grabTitle();
```

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>** title

### [#](https://codecept.io/helpers/Puppeteer/#grabvaluefrom) grabValueFrom

Retrieves a value from a form element located by CSS or XPath and returns it to test. Resumes test execution, so **should be used inside async function with `await`** operator. If more than one element is found - value of first element is returned.

```javascript
let email = await I.grabValueFrom('input[name=email]');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-48) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** field located by label|name|CSS|XPath|strict locator.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>** attribute value

### [#](https://codecept.io/helpers/Puppeteer/#grabvaluefromall) grabValueFromAll

Retrieves an array of value from a form located by CSS or XPath and returns it to test. Resumes test execution, so **should be used inside async function with `await`** operator.

```javascript
let inputs = await I.grabValueFromAll('//form/input');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-49) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** field located by label|name|CSS|XPath|strict locator.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<[Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>>** attribute value

### [#](https://codecept.io/helpers/Puppeteer/#grabwebelements) grabWebElements

Grab WebElements for given locator Resumes test execution, so **should be used inside an async function with `await`** operator.

```javascript
const webElements = await I.grabWebElements('#button');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-50) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.

Returns **[Promise (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)<any>** WebElement of being used Web helper

### [#](https://codecept.io/helpers/Puppeteer/#grabwebsocketmessages) grabWebSocketMessages

Grab the recording WS messages

Returns **([Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<any> | [undefined (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/undefined))**

### [#](https://codecept.io/helpers/Puppeteer/#handledownloads) handleDownloads

Sets a directory to where save files. Allows to test file downloads. Should be used with [FileSystem helper (opens new window)](https://codecept.io/helpers/FileSystem) to check that file were downloaded correctly.

By default, files are saved to `output/downloads`. This directory is cleaned on every `handleDownloads` call, to ensure no old files are kept.

```javascript
I.handleDownloads();
I.click('Download Avatar');
I.amInPath('output/downloads');
I.seeFile('avatar.jpg');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-51) Parameters

-   `downloadPath` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** change this parameter to set another directory for saving

### [#](https://codecept.io/helpers/Puppeteer/#mockroute) mockRoute

Mocks network request using [`Request Interception` (opens new window)](https://pptr.dev/next/guides/request-interception)

```javascript
I.mockRoute(/(.png$)|(.jpg$)/, (route) => route.abort());
```

This method allows intercepting and mocking requests & responses. [Learn more about it (opens new window)](https://pptr.dev/next/guides/request-interception)

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-52) Parameters

-   `url` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [RegExp (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/RegExp))?** URL, regex or pattern for to match URL
-   `handler` **[function (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)?** a function to process request

### [#](https://codecept.io/helpers/Puppeteer/#movecursorto) moveCursorTo

Moves cursor to element matched by locator. Extra shift can be set with offsetX and offsetY options.

```javascript
I.moveCursorTo('.tooltip');
I.moveCursorTo('#submit', 5, 5);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-53) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|strict locator.
-   `offsetX` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `0` by default) X-axis offset.
-   `offsetY` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `0` by default) Y-axis offset.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#opennewtab) openNewTab

Open new tab and switch to it

```javascript
I.openNewTab();
```

### [#](https://codecept.io/helpers/Puppeteer/#presskey) pressKey

_Note:_ Shortcuts like `'Meta'` + `'A'` do not work on macOS ([GoogleChrome/puppeteer#1313 (opens new window)](https://github.com/GoogleChrome/puppeteer/issues/1313)).

Presses a key in the browser (on a focused element).

_Hint:_ For populating text field or textarea, it is recommended to use [`fillField`](https://codecept.io/helpers/Puppeteer/#fillfield).

```javascript
I.pressKey('Backspace');
```

To press a key in combination with modifier keys, pass the sequence as an array. All modifier keys (`'Alt'`, `'Control'`, `'Meta'`, `'Shift'`) will be released afterwards.

```javascript
I.pressKey(['Control', 'Z']);
```

For specifying operation modifier key based on operating system it is suggested to use `'CommandOrControl'`. This will press `'Command'` (also known as `'Meta'`) on macOS machines and `'Control'` on non-macOS machines.

```javascript
I.pressKey(['CommandOrControl', 'Z']);
```

Some of the supported key names are:

-   `'AltLeft'` or `'Alt'`
-   `'AltRight'`
-   `'ArrowDown'`
-   `'ArrowLeft'`
-   `'ArrowRight'`
-   `'ArrowUp'`
-   `'Backspace'`
-   `'Clear'`
-   `'ControlLeft'` or `'Control'`
-   `'ControlRight'`
-   `'Command'`
-   `'CommandOrControl'`
-   `'Delete'`
-   `'End'`
-   `'Enter'`
-   `'Escape'`
-   `'F1'` to `'F12'`
-   `'Home'`
-   `'Insert'`
-   `'MetaLeft'` or `'Meta'`
-   `'MetaRight'`
-   `'Numpad0'` to `'Numpad9'`
-   `'NumpadAdd'`
-   `'NumpadDecimal'`
-   `'NumpadDivide'`
-   `'NumpadMultiply'`
-   `'NumpadSubtract'`
-   `'PageDown'`
-   `'PageUp'`
-   `'Pause'`
-   `'Return'`
-   `'ShiftLeft'` or `'Shift'`
-   `'ShiftRight'`
-   `'Space'`
-   `'Tab'`

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-54) Parameters

-   `key` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>)** key or array of keys to press.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#presskeydown) pressKeyDown

Presses a key in the browser and leaves it in a down state.

To make combinations with modifier key and user operation (e.g. `'Control'` + [`click`](https://codecept.io/helpers/Puppeteer/#click)).

```javascript
I.pressKeyDown('Control');
I.click('#element');
I.pressKeyUp('Control');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-55) Parameters

-   `key` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** name of key to press down.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#presskeyup) pressKeyUp

Releases a key in the browser which was previously set to a down state.

To make combinations with modifier key and user operation (e.g. `'Control'` + [`click`](https://codecept.io/helpers/Puppeteer/#click)).

```javascript
I.pressKeyDown('Control');
I.click('#element');
I.pressKeyUp('Control');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-56) Parameters

-   `key` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** name of key to release.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#refreshpage) refreshPage

Reload the current page.

```javascript
I.refreshPage();
```

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#resizewindow) resizeWindow

Unlike other drivers Puppeteer changes the size of a viewport, not the window! Puppeteer does not control the window of a browser, so it can't adjust its real size. It also can't maximize a window.

Resize the current window to provided width and height. First parameter can be set to `maximize`.

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-57) Parameters

-   `width` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** width in pixels or `maximize`.
-   `height` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** height in pixels.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#rightclick) rightClick

Performs right click on a clickable element matched by semantic locator, CSS or XPath.

```javascript
// right click element with id el
I.rightClick('#el');
// right click link or button with text "Click me"
I.rightClick('Click me');
// right click button with text "Click me" inside .context
I.rightClick('Click me', '.context');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-58) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** clickable element located by CSS|XPath|strict locator.
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)? | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** (optional, `null` by default) element located by CSS|XPath|strict locator.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#saveelementscreenshot) saveElementScreenshot

Saves screenshot of the specified locator to ouput folder (set in codecept.conf.ts or codecept.conf.js). Filename is relative to output folder.

```javascript
I.saveElementScreenshot(`#submit`, 'debug.png');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-59) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `fileName` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** file name to save.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#savescreenshot) saveScreenshot

Saves a screenshot to ouput folder (set in codecept.conf.ts or codecept.conf.js). Filename is relative to output folder. Optionally resize the window to the full available page `scrollHeight` and `scrollWidth` to capture the entire page by passing `true` in as the second argument.

```javascript
I.saveScreenshot('debug.png');
I.saveScreenshot('debug.png', true); //resizes to available scrollHeight and scrollWidth before taking screenshot
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-60) Parameters

-   `fileName` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** file name to save.
-   `fullPage` **[boolean (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** (optional, `false` by default) flag to enable fullscreen screenshot mode.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#scrollpagetobottom) scrollPageToBottom

Scroll page to the bottom.

```javascript
I.scrollPageToBottom();
```

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#scrollpagetotop) scrollPageToTop

Scroll page to the top.

```javascript
I.scrollPageToTop();
```

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#scrollto) scrollTo

Scrolls to element matched by locator. Extra shift can be set with offsetX and offsetY options.

```javascript
I.scrollTo('footer');
I.scrollTo('#submit', 5, 5);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-61) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|strict locator.
-   `offsetX` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `0` by default) X-axis offset.
-   `offsetY` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `0` by default) Y-axis offset.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#see) see

Checks that a page contains a visible text. Use context parameter to narrow down the search.

```javascript
I.see('Welcome'); // text welcome on a page
I.see('Welcome', '.content'); // text inside .content div
I.see('Register', { css: 'form.register' }); // use strict locator
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-62) Parameters

-   `text` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** expected on page.
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)? | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** (optional, `null` by default) element located by CSS|Xpath|strict locator in which to search for text.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#seeattributesonelements) seeAttributesOnElements

Checks that all elements with given locator have given attributes.

```javascript
I.seeAttributesOnElements('//form', { method: 'post' });
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-63) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|strict locator.
-   `attributes` **[object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** attributes and their values to check.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#seecheckboxischecked) seeCheckboxIsChecked

Verifies that the specified checkbox is checked.

```javascript
I.seeCheckboxIsChecked('Agree');
I.seeCheckboxIsChecked('#agree'); // I suppose user agreed to terms
I.seeCheckboxIsChecked({ css: '#signup_form input[type=checkbox]' });
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-64) Parameters

-   `field` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by label|name|CSS|XPath|strict locator.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seecookie) seeCookie

Checks that cookie with given name exists.

```javascript
I.seeCookie('Auth');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-65) Parameters

-   `name` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** cookie name.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seecsspropertiesonelements) seeCssPropertiesOnElements

Checks that all elements with given locator have given CSS properties.

```javascript
I.seeCssPropertiesOnElements('h3', { 'font-weight': 'bold' });
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-66) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|strict locator.
-   `cssProperties` **[object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** object with CSS properties and their values to check.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#seecurrenturlequals) seeCurrentUrlEquals

Checks that current url is equal to provided one. If a relative url provided, a configured url will be prepended to it. So both examples will work:

```javascript
I.seeCurrentUrlEquals('/register');
I.seeCurrentUrlEquals('http://my.site.com/register');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-67) Parameters

-   `url` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** value to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seeelement) seeElement

Checks that a given Element is visible Element is located by CSS or XPath.

```javascript
I.seeElement('#modal');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-68) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by CSS|XPath|strict locator.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#seeelementindom) seeElementInDOM

Checks that a given Element is present in the DOM Element is located by CSS or XPath.

```javascript
I.seeElementInDOM('#modal');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-69) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seeincurrenturl) seeInCurrentUrl

Checks that current url contains a provided fragment.

```javascript
I.seeInCurrentUrl('/register'); // we are on registration page
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-70) Parameters

-   `url` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a fragment to check

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seeinfield) seeInField

Checks that the given input field or textarea equals to given value. For fuzzy locators, fields are matched by label text, the "name" attribute, CSS, and XPath.

```javascript
I.seeInField('Username', 'davert');
I.seeInField({ css: 'form textarea' }, 'Type your comment here');
I.seeInField('form input[type=hidden]', 'hidden_value');
I.seeInField('#searchform input', 'Search');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-71) Parameters

-   `field` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** located by label|name|CSS|XPath|strict locator.
-   `value` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** value to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seeinpopup) seeInPopup

Checks that the active JavaScript popup, as created by `window.alert|window.confirm|window.prompt`, contains the given string.

```javascript
I.seeInPopup('Popup text');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-72) Parameters

-   `text` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** value to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seeinsource) seeInSource

Checks that the current page contains the given string in its raw source code.

```javascript
I.seeInSource('<h1>Green eggs &amp; ham</h1>');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-73) Parameters

-   `text` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** value to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seeintitle) seeInTitle

Checks that title contains text.

```javascript
I.seeInTitle('Home Page');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-74) Parameters

-   `text` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** text value to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seenumberofelements) seeNumberOfElements

Asserts that an element appears a given number of times in the DOM. Element is located by label or name or CSS or XPath.

```javascript
I.seeNumberOfElements('#submitBtn', 1);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-75) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `num` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** number of elements.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#seenumberofvisibleelements) seeNumberOfVisibleElements

Asserts that an element is visible a given number of times. Element is located by CSS or XPath.

```javascript
I.seeNumberOfVisibleElements('.buttons', 3);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-76) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `num` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** number of elements.

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#seetextequals) seeTextEquals

Checks that text is equal to provided one.

```javascript
I.seeTextEquals('text', 'h1');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-77) Parameters

-   `text` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** element value to check.
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))?** element located by CSS|XPath|strict locator.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seetitleequals) seeTitleEquals

Checks that title is equal to provided one.

```javascript
I.seeTitleEquals('Test title.');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-78) Parameters

-   `text` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** value to check.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#seetraffic) seeTraffic

Verifies that a certain request is part of network traffic.

```javascript
// checking the request url contains certain query strings
I.amOnPage('https://openai.com/blog/chatgpt');
I.startRecordingTraffic();
await I.seeTraffic({
	name: 'sentry event',
	url: 'https://images.openai.com/blob/cf717bdb-0c8c-428a-b82b-3c3add87a600',
	parameters: {
		width: '1919',
		height: '1138'
	}
});
```

```javascript
// checking the request url contains certain post data
I.amOnPage('https://openai.com/blog/chatgpt');
I.startRecordingTraffic();
await I.seeTraffic({
	name: 'event',
	url: 'https://cloudflareinsights.com/cdn-cgi/rum',
	requestPostData: {
		st: 2
	}
});
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-79) Parameters

-   `opts` **[Object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** options when checking the traffic network.
    -   `opts.name` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** A name of that request. Can be any value. Only relevant to have a more meaningful error message in case of fail.
    -   `opts.url` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Expected URL of request in network traffic
    -   `opts.parameters` **[Object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** Expected parameters of that request in network traffic
    -   `opts.requestPostData` **[Object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)?** Expected that request contains post data in network traffic
    -   `opts.timeout` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** Timeout to wait for request in seconds. Default is 10 seconds.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#selectoption) selectOption

Selects an option in a drop-down select. Field is searched by label | name | CSS | XPath. Option is selected by visible text or by value.

```javascript
I.selectOption('Choose Plan', 'Monthly'); // select by label
I.selectOption('subscription', 'Monthly'); // match option by text
I.selectOption('subscription', '0'); // or by value
I.selectOption('//form/select[@name=account]', 'Premium');
I.selectOption('form select[name=account]', 'Premium');
I.selectOption({ css: 'form select[name=account]' }, 'Premium');
```

Provide an array for the second argument to select multiple options.

```javascript
I.selectOption('Which OS do you use?', ['Android', 'iOS']);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-80) Parameters

-   `select` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** field located by label|name|CSS|XPath|strict locator.
-   `option` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<any>)** visible text or value of option.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#setcookie) setCookie

Sets cookie(s).

Can be a single cookie object or an array of cookies:

```javascript
I.setCookie({ name: 'auth', value: true });

// as array
I.setCookie([
	{ name: 'auth', value: true },
	{ name: 'agree', value: true }
]);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-81) Parameters

-   `cookie` **(Cookie | [Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<Cookie>)** a cookie object or array of cookie objects.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#setpuppeteerrequestheaders) setPuppeteerRequestHeaders

Set headers for all next requests

```javascript
I.setPuppeteerRequestHeaders({
	'X-Sent-By': 'CodeceptJS'
});
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-82) Parameters

-   `customHeaders` **[object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** headers to set

### [#](https://codecept.io/helpers/Puppeteer/#startrecordingtraffic) startRecordingTraffic

Starts recording the network traffics. This also resets recorded network requests.

```javascript
I.startRecordingTraffic();
```

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#startrecordingwebsocketmessages) startRecordingWebSocketMessages

Starts recording of websocket messages. This also resets recorded websocket messages.

```javascript
await I.startRecordingWebSocketMessages();
```

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#stopmockingroute) stopMockingRoute

Stops network mocking created by `mockRoute`.

```javascript
I.stopMockingRoute(/(.png$)|(.jpg$)/);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-83) Parameters

-   `url` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [RegExp (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/RegExp))?** URL, regex or pattern for to match URL

### [#](https://codecept.io/helpers/Puppeteer/#stoprecordingtraffic) stopRecordingTraffic

Stops recording of network traffic. Recorded traffic is not flashed.

```javascript
I.stopRecordingTraffic();
```

### [#](https://codecept.io/helpers/Puppeteer/#stoprecordingwebsocketmessages) stopRecordingWebSocketMessages

Stops recording WS messages. Recorded WS messages is not flashed.

```javascript
await I.stopRecordingWebSocketMessages();
```

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#switchto) switchTo

Switches frame or in case of null locator reverts to parent.

```javascript
I.switchTo('iframe'); // switch to first iframe
I.switchTo(); // switch back to main page
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-84) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)? | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** (optional, `null` by default) element located by CSS|XPath|strict locator.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#switchtonexttab) switchToNextTab

Switch focus to a particular tab by its number. It waits tabs loading and then switch tab

```javascript
I.switchToNextTab();
I.switchToNextTab(2);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-85) Parameters

-   `num` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)**

### [#](https://codecept.io/helpers/Puppeteer/#switchtoprevioustab) switchToPreviousTab

Switch focus to a particular tab by its number. It waits tabs loading and then switch tab

```javascript
I.switchToPreviousTab();
I.switchToPreviousTab(2);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-86) Parameters

-   `num` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)**

### [#](https://codecept.io/helpers/Puppeteer/#type) type

Types out the given text into an active field. To slow down typing use a second parameter, to set interval between key presses. _Note:_ Should be used when [`fillField`](https://codecept.io/helpers/Puppeteer/#fillfield) is not an option.

```javascript
// passing in a string
I.type('Type this out.');

// typing values with a 100ms interval
I.type('4141555311111111', 100);

// passing in an array
I.type(['T', 'E', 'X', 'T']);

// passing a secret
I.type(secret('123456'));
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-87) Parameters

-   `keys`
-   `delay` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** (optional) delay in ms between key presses
-   `key` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)\>)** or array of keys to type.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#uncheckoption) uncheckOption

Unselects a checkbox or radio button. Element is located by label or name or CSS or XPath.

The second parameter is a context (CSS or XPath locator) to narrow the search.

```javascript
I.uncheckOption('#agree');
I.uncheckOption('I Agree to Terms and Conditions');
I.uncheckOption('agree', '//form');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-88) Parameters

-   `field` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** checkbox located by label | name | CSS | XPath | strict locator.
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)? | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** (optional, `null` by default) element located by CSS | XPath | strict locator.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#usepuppeteerto) usePuppeteerTo

Use Puppeteer API inside a test.

First argument is a description of an action. Second argument is async function that gets this helper as parameter.

{ [`page` (opens new window)](https://github.com/puppeteer/puppeteer/blob/master/docs/api.md#class-page), [`browser` (opens new window)](https://github.com/puppeteer/puppeteer/blob/master/docs/api.md#class-browser) } from Puppeteer API are available.

```javascript
I.usePuppeteerTo('emulate offline mode', async ({ page }) {
  await page.setOfflineMode(true);
});
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-89) Parameters

-   `description` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** used to show in logs.
-   `fn` **[function (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** async function that is executed with Puppeteer as argument

### [#](https://codecept.io/helpers/Puppeteer/#wait) wait

Pauses execution for a number of seconds.

```javascript
I.wait(2); // wait 2 secs
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-90) Parameters

-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** number of second to wait.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitforclickable) waitForClickable

Waits for element to be clickable (by default waits for 1sec). Element can be located by CSS or XPath.

```javascript
I.waitForClickable('.btn.continue');
I.waitForClickable('.btn.continue', 5); // wait for 5 secs
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-91) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `waitTimeout`
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitforcookie) waitForCookie

Waits for the specified cookie in the cookies.

```javascript
I.waitForCookie('token');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-92) Parameters

-   `name` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** expected cookie name.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `3` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitfordetached) waitForDetached

Waits for an element to become not attached to the DOM on a page (by default waits for 1sec). Element can be located by CSS or XPath.

```javascript
I.waitForDetached('#popup');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-93) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitforelement) waitForElement

Waits for element to be present on page (by default waits for 1sec). Element can be located by CSS or XPath.

```javascript
I.waitForElement('.btn.continue');
I.waitForElement('.btn.continue', 5); // wait for 5 secs
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-94) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#waitforenabled) waitForEnabled

Waits for element to become enabled (by default waits for 1sec). Element can be located by CSS or XPath.

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-95) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional) time in seconds to wait, 1 by default.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitforfunction) waitForFunction

Waits for a function to return true (waits for 1 sec by default). Running in browser context.

```javascript
I.waitForFunction(fn[, [args[, timeout]])
```

```javascript
I.waitForFunction(() => window.requests == 0);
I.waitForFunction(() => window.requests == 0, 5); // waits for 5 sec
I.waitForFunction((count) => window.requests == count, [3], 5); // pass args and wait for 5 sec
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-96) Parameters

-   `fn` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [function (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function))** to be executed in browser context.
-   `argsOrSec` **([Array (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)<any> | [number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number))?** (optional, `1` by default) arguments for function or seconds.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitforinvisible) waitForInvisible

Waits for an element to be removed or become invisible on a page (by default waits for 1sec). Element can be located by CSS or XPath.

```javascript
I.waitForInvisible('#popup');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-97) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitfornavigation) waitForNavigation

Waits for navigation to finish. By default, takes configured `waitForNavigation` option.

See [Puppeteer's reference (opens new window)](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pagewaitfornavigationoptions)

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-98) Parameters

-   `opts` **any**

### [#](https://codecept.io/helpers/Puppeteer/#waitfornumberoftabs) waitForNumberOfTabs

Waits for number of tabs.

```javascript
I.waitForNumberOfTabs(2);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-99) Parameters

-   `expectedTabs` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** expecting the number of tabs.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** number of secs to wait.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitforrequest) waitForRequest

Waits for a network request.

```javascriptI.waitForRequest('http://example.com/resource');
I.waitForRequest(request => request.url() === 'http://example.com' && request.method() === 'GET');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-100) Parameters

-   `urlOrPredicate` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [function (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function))**
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** seconds to wait

### [#](https://codecept.io/helpers/Puppeteer/#waitforresponse) waitForResponse

Waits for a network response.

```javascript
I.waitForResponse('http://example.com/resource');
I.waitForResponse(
	(response) =>
		response.url() === 'http://example.com' &&
		response.request().method() === 'GET'
);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-101) Parameters

-   `urlOrPredicate` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [function (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function))**
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** number of seconds to wait

### [#](https://codecept.io/helpers/Puppeteer/#waitfortext) waitForText

Waits for a text to appear (by default waits for 1sec). Element can be located by CSS or XPath. Narrow down search results by providing context.

```javascript
I.waitForText('Thank you, form has been submitted');
I.waitForText('Thank you, form has been submitted', 5, '#modal');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-102) Parameters

-   `text` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** to wait for.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `1` by default) time in seconds to wait
-   `context` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))?** (optional) element located by CSS|XPath|strict locator.

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitforvalue) waitForValue

Waits for the specified value to be in value attribute.

```javascript
I.waitForValue('//input', 'GoodValue');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-103) Parameters

-   `field` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** input field.
-   `value` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** expected value.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitforvisible) waitForVisible

Waits for an element to become visible on a page (by default waits for 1sec). Element can be located by CSS or XPath.

```javascript
I.waitForVisible('#popup');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-104) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#waitinurl) waitInUrl

Waiting for the part of the URL to match the expected. Useful for SPA to understand that page was changed.

```javascript
I.waitInUrl('/info', 2);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-105) Parameters

-   `urlPart` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** value to check.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waitnumberofvisibleelements) waitNumberOfVisibleElements

Waits for a specified number of elements on the page.

```javascript
I.waitNumberOfVisibleElements('a', 3);
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-106) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `num` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** number of elements.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

This action supports [React locators (opens new window)](https://codecept.io/react#locators)

### [#](https://codecept.io/helpers/Puppeteer/#waittohide) waitToHide

Waits for an element to hide (by default waits for 1sec). Element can be located by CSS or XPath.

```javascript
I.waitToHide('#popup');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-107) Parameters

-   `locator` **([string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String) | [object (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object))** element located by CSS|XPath|strict locator.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder

### [#](https://codecept.io/helpers/Puppeteer/#waiturlequals) waitUrlEquals

Waits for the entire URL to match the expected

```javascript
I.waitUrlEquals('/info', 2);
I.waitUrlEquals('http://127.0.0.1:8000/info');
```

#### [#](https://codecept.io/helpers/Puppeteer/#parameters-108) Parameters

-   `urlPart` **[string (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** value to check.
-   `sec` **[number (opens new window)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** (optional, `1` by default) time in seconds to wait

Returns **void** automatically synchronized promise through #recorder
