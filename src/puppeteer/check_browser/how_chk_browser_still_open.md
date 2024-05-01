# [puppeteer : how check if browser is still open and working](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 5 years, 8 months ago

Modified [3 years, 11 months ago](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working?lastactivity '2020-06-03 02:26:18Z')

Viewed 38k times

This question shows research effort; it is useful and clear

21

This question does not show any research effort; it is unclear or not useful

Save this question.

[](https://stackoverflow.com/posts/52045600/timeline)

Show activity on this post.

im trying to open multiple tabs in a single browser instance , after they're done i close the tabs and then re-opening those tabs every x seconds ... but i want to keep the browser itself open so i dont have to login in each tab on every loop

so the browser remains open , tabs open and close

here is my simplified code , pleas ignore syntax erros

```javascript
var global_browser = false;
async function init_puppeteer(settings) {
    if (global_browser === false)
        global_browser = await puppeteer.launch({
            headless: false,
            args: ['--no-sandbox']
        });

    for (var i = 0; i < settings.length; i++) {
        var setting = settings[i];
        open_tab($setting);
    }
}

async function open_tab(setting) {
    const page = await global_browser.newPage();
    // do stuff
    page.close();
}

setInterval(function () {
    init_puppeteer(settings);
}, 50000);
```

here is the problem , sometimes browser crashes or it get closed for whatever reason but the `global_browser` remains an object /instance of puppeteer ... of curse it wont work when i try open a tab with that instance , and i get something like

```javascript
(node:5720) UnhandledPromiseRejectionWarning: Error: WebSocket is not open: readyState 3 (CLOSED)
```

here is my question , how can i check and make sure i have a working/open instance of puppeteer in `global_browser` ? so i can create a new instance and replace it if the previous one is closed

-   [javascript](https://stackoverflow.com/questions/tagged/javascript "show questions tagged 'javascript'")
-   [puppeteer](https://stackoverflow.com/questions/tagged/puppeteer "show questions tagged 'puppeteer'")

[Share](https://stackoverflow.com/q/52045600/15588573 'Short permalink to this question')

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/52045600/edit 'Revise and improve this post')

Follow

Follow this question to receive notifications

[edited Aug 27, 2018 at 19:15](https://stackoverflow.com/posts/52045600/revisions 'show all edits to this post')

hretic

asked Aug 27, 2018 at 19:09

[

![hretic's user avatar](https://www.gravatar.com/avatar/0d0c55f94426eb3d52568d5540aab6cf?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/5796284/hretic)

[hretic](https://stackoverflow.com/users/5796284/hretic)hretic

1,15999 gold badges4141 silver badges8383 bronze badges

3

-   You are calling `page.close();` in your `open_tab()` function. I think that's why it closes the browser.
    – [Neeraj Wadhwa](https://stackoverflow.com/users/6842291/neeraj-wadhwa '705 reputation')
    [Aug 30, 2018 at 8:03](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working#comment91133876_52045600)
-   4
    He is asking how to tell if it is closed or not. Not why it closes.
    – [Md. Abu Taher](https://stackoverflow.com/users/6161265/md-abu-taher '18,353 reputation')
    [Aug 30, 2018 at 10:56](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working#comment91140572_52045600)
-   [Related GH issue #3149](https://github.com/puppeteer/puppeteer/issues/3149)
    – [ggorlen](https://stackoverflow.com/users/6243352/ggorlen '51,606 reputation')
    [May 14, 2023 at 4:23](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working#comment134456758_52045600)

[Add a comment](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working# 'Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.') | [](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working# 'Expand to show all comments on this post')

Report this ad

## 3 Answers 3

Sorted by: [Reset to default](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

45

This answer is not useful

Save this answer.

+100

This answer has been awarded bounties worth 100 reputation by hretic

[](https://stackoverflow.com/posts/52105376/timeline)

Show activity on this post.

### Use `browser.on('disconnected')`.

You can use [`browser.on('disconnected')`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#event-disconnected) to listen for when the browser is closed or crashed, or if the [`browser.disconnect()`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#browserdisconnect) method was called.

Then, you can automatically relaunch the browser, and continue with your program.

The following class will launch the browser, and automatically relaunch the browser whenever the `'disconnected'` event is fired:

```javascript
class BrowserHandler {
    constructor() {
        const launch_browser = async () => {
            this.browser = false;
            this.browser = await puppeteer.launch();
            this.browser.on('disconnected', launch_browser);
        };

        (async () => {
            await launch_browser();
        })();
    }
}
```

**`BrowserHandler.browser` will return `false` when disconnected.**

Additionally, the following function will give you the ability to force your program to wait for the browser to finish launching before continuing any further:

```javascript
const wait_for_browser = (browser_handler) =>
    new Promise((resolve, reject) => {
        const browser_check = setInterval(() => {
            if (browser_handler.browser !== false) {
                clearInterval(browser_check);
                resolve(true);
            }
        }, 100);
    });
```

---

**Complete Example:**

```javascript
'use strict';

const puppeteer = require('puppeteer');

/**
 * Class: BrowserHandler
 *     Relaunch Browser when Closed
 *     Return false when Browser is Disconnected
 */

class BrowserHandler {
    constructor() {
        const launch_browser = async () => {
            this.browser = false;
            this.browser = await puppeteer.launch();
            this.browser.on('disconnected', launch_browser);
        };

        (async () => {
            await launch_browser();
        })();
    }
}

/**
 * Function: wait_for_browser
 *     Wait for Browser to Finish Launching
 */

const wait_for_browser = (browser_handler) =>
    new Promise((resolve, reject) => {
        const browser_check = setInterval(() => {
            if (browser_handler.browser !== false) {
                clearInterval(browser_check);
                resolve(true);
            }
        }, 100);
    });

// Main Program

(async () => {
    // Open Browser

    const browser_handler = new BrowserHandler();

    await wait_for_browser(browser_handler);

    // Open New Page

    let page = await browser_handler.browser.newPage();

    await page.goto('https://www.example.com/');

    // Disconnect and Automatically Reconnect Browser

    browser_handler.browser.disconnect();

    if (browser_handler.browser === false) {
        console.log('The browser has been disconnected.');

        await wait_for_browser(browser_handler);
    }

    console.log('The browser has been reconnected.');

    // Close and Automatically Reopen Browser

    await browser_handler.browser.close();

    if (browser_handler.browser === false) {
        console.log('The browser has been closed.');

        await wait_for_browser(browser_handler);
    }

    console.log('The browser has been reopened.');

    // Force Close Puppeteer

    process.exit();
})();
```

**Result:**

> The browser has been disconnected.
>
> The browser has been reconnected.
>
> The browser has been closed.
>
> The browser has been reopened.

[Share](https://stackoverflow.com/a/52105376/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/52105376/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Jun 20, 2020 at 9:12](https://stackoverflow.com/posts/52105376/revisions 'show all edits to this post')

[

![Community's user avatar](https://www.gravatar.com/avatar/a007be5a61f6aa8f3e85ae2fc18dd66e?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/-1/community)

[Community](https://stackoverflow.com/users/-1/community)Bot

111 silver badge

answered Aug 30, 2018 at 21:08

[

![Grant Miller's user avatar](https://i.stack.imgur.com/a6JjK.jpg?s=64&g=1)

](https://stackoverflow.com/users/4283581/grant-miller)

[Grant Miller](https://stackoverflow.com/users/4283581/grant-miller)Grant Miller

28.4k1616 gold badges151151 silver badges167167 bronze badges

2

-   As for this moment, for me, this solution not working, Only restart the application works.
    – [Or Assayag](https://stackoverflow.com/users/4442606/or-assayag '6,030 reputation')
    [Nov 29, 2020 at 9:17](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working#comment115017352_52105376)
-   Grant, can you explain how to extend this so it also reopens the "page" when the page closed? So, if the page closes, it reopens. If the browser closes, it reopens the browser AND the page.
    – [regan](https://stackoverflow.com/users/225114/regan '405 reputation')
    [Jul 24, 2021 at 15:27](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working#comment121079742_52105376)

[Add a comment](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working# 'Expand to show all comments on this post')

This answer is useful

8

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/62164233/timeline)

Show activity on this post.

If you just close all tabs (or browser window) but browser process is still there (but no any window).

`disconnected` event will not be triggered.

Then you can check whether all tabs are closed by:

```javascript
if ((await browser.pages()).length === 0) {
    // no tabs opening, do stuff
}
```

[Share](https://stackoverflow.com/a/62164233/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/62164233/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Jun 3, 2020 at 2:26

[

![Anyany Pan's user avatar](https://lh5.googleusercontent.com/-ZCto7-MKXIQ/AAAAAAAAAAI/AAAAAAAAACs/QqrmRclY7mo/photo.jpg?sz=64)

](https://stackoverflow.com/users/4683349/anyany-pan)

[Anyany Pan](https://stackoverflow.com/users/4683349/anyany-pan)Anyany Pan

67977 silver badges99 bronze badges

0

[Add a comment](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working# 'Expand to show all comments on this post')

This answer is useful

2

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/52095290/timeline)

Show activity on this post.

You can make a very simple function to know if the browser process was killed.

```javascript
async function wasBrowserKilled(browser) {
    const procInfo = await browser.process();
    return !!procInfo.signalCode; // null if browser is still running
}
```

We can use this here,

```javascript
const browserKilled = await wasBrowserKilled(global_browser);
if(global_browser === false || browserKilled)
```

It will check if the browser was killed, otherwise it will replace it.

This is just one way out of many provided by the API.

This is the code I used to test this out, see how the output changes if I comment out the `browser.close()` section.

```javascript
const puppeteer = require('puppeteer');

puppeteer.launch().then(async (browser) => {
    const page = await browser.newPage();
    // comment out to keep browser open
    await browser.close();
    console.log({ browserKilled: await wasBrowserKilled(browser) });
});

async function wasBrowserKilled(browser) {
    const procInfo = await browser.process();
    return !!procInfo.signalCode;
}
```

Log here,

```javascript
➜  puppeteer-xvfb git:(direct-script) ✗ node temp/interval_tab.js
{ browserKilled: true }
➜  puppeteer-xvfb git:(direct-script) ✗ node temp/interval_tab.js
{ browserKilled: false }
_
```

This is different than the event. I made this snippet specially to check the process for this specific question where you check and run it if you want.

Note that this will only produce result if the browser is crashed/closed somehow.

[Share](https://stackoverflow.com/a/52095290/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/52095290/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Aug 31, 2018 at 12:24](https://stackoverflow.com/posts/52095290/revisions 'show all edits to this post')

answered Aug 30, 2018 at 10:54

[

![Md. Abu Taher's user avatar](https://i.stack.imgur.com/YAtzE.jpg?s=64&g=1)

](https://stackoverflow.com/users/6161265/md-abu-taher)

[Md. Abu Taher](https://stackoverflow.com/users/6161265/md-abu-taher)Md. Abu Taher

18.4k55 gold badges5454 silver badges7676 bronze badges

2

-   1
    thanx but `procInfo.signalCode` is null both for open and closed browser
    – [hretic](https://stackoverflow.com/users/5796284/hretic '1,159 reputation')
    [Aug 30, 2018 at 15:33](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working#comment91152170_52095290)
-   1
    My end showed SIGKILL for signalCode :/ Show me how you are closing the browser/check when it crashes.
    – [Md. Abu Taher](https://stackoverflow.com/users/6161265/md-abu-taher '18,353 reputation')
    [Aug 30, 2018 at 18:07](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working#comment91156899_52095290)

[Add a comment](https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.')
