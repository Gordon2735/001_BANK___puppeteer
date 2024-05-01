# checking if browser is still open and working #3149

Closed

[Hretic](https://github.com/Hretic) opened this issue Aug 28, 2018 · 8 comments

Closed

# [checking if browser is still open and working](https://github.com/puppeteer/puppeteer/issues/3149#top) #3149

[Hretic](https://github.com/Hretic) opened this issue Aug 28, 2018 · 8 comments

## Comments

[![@Hretic](https://avatars.githubusercontent.com/u/2313132?s=80&v=4)](https://github.com/Hretic)

Sorry, something went wrong.

Quote reply

###

**[Hretic](https://github.com/Hretic)** commented [Aug 28, 2018](https://github.com/puppeteer/puppeteer/issues/3149#issue-354715507)

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">
                    im trying to open multiple tabs in a single browser instance
                    , after they're done i close the tabs and then re-opening
                    those tabs every x seconds ... but i want to keep the
                    browser itself open so i dont have to login in each tab on
                    every loop
                </p>
                <p dir="auto">
                    so the browser remains open , tabs open and close
                </p>
                <p dir="auto">
                    here is my simplified code , pleas ignore syntax erros
                </p>
                <div
                    class="snippet-clipboard-content notranslate position-relative overflow-auto"
                >
                    <pre class="notranslate"></pre>
                </div>
            </td>
        </tr>
    </tbody>
</table>
```

```typescript
var  global_browser = false ;
async function init_puppeteer( settings ) {

    if(global_browser === false )
        global_browser = await puppeteer.launch({headless: false  , args:['--no-sandbox']});

    for(var i = 0  ; i &lt; settings.length ; i++ )
    {
        var setting = settings[i];
    	open_tab($setting);
    }

}

async function open_tab( setting ){
const page = await global_browser.newPage();
// do stuff
page.close();
}

setInterval(function (){
init_puppeteer(settings)
}, 50000 );
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="var global_browser = false ;
async function init_puppeteer( settings ) {

    if(global_browser === false )
        global_browser = await puppeteer.launch({headless: false  , args:['--no-sandbox']});

    for(var i = 0  ; i &lt; settings.length ; i++ )
    {
        var setting = settings[i];
    	open_tab($setting);
    }

}

async function open_tab( setting ){
const page = await global_browser.newPage();
// do stuff
page.close();
}

setInterval(function (){
init_puppeteer(settings)
}, 50000 );
```

```html
<>"tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">here is the problem , sometimes browser crashes or it get closed for whatever reason but the <code class="notranslate">global_browser</code> remains an object /instance of puppeteer ... of curse it wont work when i try open a tab with that instance , and i get something like</p><div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code class="notranslate">(node:5720) UnhandledPromiseRejectionWarning: Error: WebSocket is not open: readyState 3 (CLOSED)
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="(node:5720) UnhandledPromiseRejectionWarning: Error: WebSocket is not open: readyState 3 (CLOSED)" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">here is my question , how can i check and make sure i have a working/open instance of puppeteer in <code class="notranslate">global_browser</code> ? so i can create a new instance and replace it if the previous one is closed</p></td></tr><tr class="d-block pl-3 pr-3 pb-3 js-comment-body-error" hidden=""><td class="d-block"><div class="flash flash-warn" role="alert"><p class="mb-1"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-info"><path d="M0 8a8 8 0 1 1 16 0A8 8 0 0 1 0 8Zm8-6.5a6.5 6.5 0 1 0 0 13 6.5 6.5 0 0 0 0-13ZM6.5 7.75A.75.75 0 0 1 7.25 7h1a.75.75 0 0 1 .75.75v2.75h.25a.75.75 0 0 1 0 1.5h-2a.75.75 0 0 1 0-1.5h.25v-2h-.25a.75.75 0 0 1-.75-.75ZM8 6a1 1 0 1 1 0-2 1 1 0 0 1 0 2Z"></path></svg>The text was updated successfully, but these errors were encountered:</p><ol class="mb-0 pl-4 ml-4"></ol></div></td></tr></tbody></table>
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

All reactions

[![@ris58h](https://avatars.githubusercontent.com/u/511242?s=80&u=b8c8b011da01167ded4fad6ecd30aa15163ab974&v=4)](https://github.com/ris58h)

Sorry, something went wrong.

Quote reply

###

**[ris58h](https://github.com/ris58h)** commented [Aug 28, 2018](https://github.com/puppeteer/puppeteer/issues/3149#issuecomment-416710852) •

edited

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">
                    Why just not to handle that error? Even if there is/was such
                    method to check the browser's state, the browser can crash
                    right after this check.
                </p>
            </td>
        </tr>
    </tbody>
</table>
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

All reactions

Sorry, something went wrong.

[![@Hretic](https://avatars.githubusercontent.com/u/2313132?s=80&v=4)](https://github.com/Hretic)

Sorry, something went wrong.

Quote reply

Author

###

**[Hretic](https://github.com/Hretic)** commented [Aug 30, 2018](https://github.com/puppeteer/puppeteer/issues/3149#issuecomment-417228788) •

edited

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">
                    the whole process repeats in a setInterval loop so if it
                    crashes right after check i'll re-open it in the next loop
                    (if i can figure out how to check the browser) ..... but its
                    also a good idea to check for that specific error , that
                    would be my plan B ..... the thing is crashes might result
                    on different error(s) ... i got this error by closing the
                    browser myself so i think its more reliable to check the
                    state of browser
                </p>
            </td>
        </tr>
    </tbody>
</table>
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

All reactions

Sorry, something went wrong.

[![@ShragaUser](https://avatars.githubusercontent.com/u/18091546?s=80&u=c1fd57ea7c6fc7439a1496f924db63918eeaf356&v=4)](https://github.com/ShragaUser)

Sorry, something went wrong.

Quote reply

###

**[ShragaUser](https://github.com/ShragaUser)** commented [Aug 31, 2018](https://github.com/puppeteer/puppeteer/issues/3149#issuecomment-417777156)

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">
                    Hi!<br />we can check to see if browser is open and running
                    by accessing the browsers ChildProcess instance and see if
                    the process itself is running on the computer via the
                    exposed pid.
                </p>
                <p dir="auto">
                    also we could add logic to chrome process 'close' event to
                    emit an event or update Browser's new property such as
                    "ísOpen".
                </p>
                <p dir="auto">
                    <a
                        class="user-mention notranslate"
                        data-hovercard-type="user"
                        data-hovercard-url="/users/Hretic/hovercard"
                        data-octo-click="hovercard-link-click"
                        data-octo-dimensions="link_type:self"
                        href="https://github.com/Hretic"
                        >@Hretic</a
                    >
                    - for now as a workaround you can add an event listener on
                    the local browser instance _process to let you know you need
                    to "restart" the browser in your code.
                </p>
                <p dir="auto">any thoughts?</p>
            </td>
        </tr>
    </tbody>
</table>
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

All reactions

Sorry, something went wrong.

[![@ShragaUser](https://avatars.githubusercontent.com/u/18091546?s=80&u=c1fd57ea7c6fc7439a1496f924db63918eeaf356&v=4)](https://github.com/ShragaUser)

Sorry, something went wrong.

Quote reply

###

**[ShragaUser](https://github.com/ShragaUser)** commented [Aug 31, 2018](https://github.com/puppeteer/puppeteer/issues/3149#issuecomment-417783565)

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">
                    <a
                        class="user-mention notranslate"
                        data-hovercard-type="user"
                        data-hovercard-url="/users/Hretic/hovercard"
                        data-octo-click="hovercard-link-click"
                        data-octo-dimensions="link_type:self"
                        href="https://github.com/Hretic"
                        >@Hretic</a
                    >
                    - something of the sorts:<br /><code class="notranslate"
                        >global_browser._process.once('close',()=&gt;{
                        global_browser.isClose = true; });</code
                    ><br />and then elsewhere in your code ( openTab function
                    maybe ) put in:<br /><code class="notranslate"
                        >if(browser.isClose){ global_browser = await
                        puppeteer.launch({headless: false ,
                        args:['--no-sandbox']}); }</code
                    >
                </p>
            </td>
        </tr>
    </tbody>
</table>
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 2 saqib-ahmed and bluesealjs reacted with thumbs up emoji

All reactions

-   👍 2 reactions

Sorry, something went wrong.

This was referenced Sep 1, 2018

[Feature: see if chrome process is currently open #3171](https://github.com/puppeteer/puppeteer/pull/3171)

Closed

[feat(browser): see if chrome process is currently open #3172](https://github.com/puppeteer/puppeteer/pull/3172)

Closed

[![@Hretic](https://avatars.githubusercontent.com/u/2313132?s=80&v=4)](https://github.com/Hretic)

Sorry, something went wrong.

Quote reply

Author

###

**[Hretic](https://github.com/Hretic)** commented [Sep 2, 2018](https://github.com/puppeteer/puppeteer/issues/3149#issuecomment-417920517) •

edited

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">thanx , i used event listener and its working</p>
            </td>
        </tr>
    </tbody>
</table>
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 2 aslushnikov and davidevallicella reacted with thumbs up emoji

All reactions

-   👍 2 reactions

Sorry, something went wrong.

[![@aslushnikov](https://avatars.githubusercontent.com/u/746130?s=80&u=bc83ba749f90def9710c03f1502595f1c3af49a9&v=4)](https://github.com/aslushnikov)

Sorry, something went wrong.

Quote reply

Contributor

###

**[aslushnikov](https://github.com/aslushnikov)** commented [Sep 4, 2018](https://github.com/puppeteer/puppeteer/issues/3149#issuecomment-418483101)

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">
                    note: you can access browser process with
                    <a
                        href="https://pptr.dev/#?product=Puppeteer&amp;version=v1.7.0&amp;show=api-browserprocess"
                        rel="nofollow"
                        ><code class="notranslate">browser.process()</code></a
                    >.
                </p>
            </td>
        </tr>
    </tbody>
</table>
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

All reactions

Sorry, something went wrong.

[![@aslushnikov](https://avatars.githubusercontent.com/u/746130?s=40&u=bc83ba749f90def9710c03f1502595f1c3af49a9&v=4)](https://github.com/aslushnikov) [aslushnikov](https://github.com/aslushnikov) closed this as [completed](https://github.com/puppeteer/puppeteer/issues?q=is%3Aissue+is%3Aclosed+archived%3Afalse+reason%3Acompleted) [Sep 4, 2018](https://github.com/puppeteer/puppeteer/issues/3149#event-1826105228)

[![@saqib-ahmed](https://avatars.githubusercontent.com/u/16355181?s=80&u=7cb0634464e836d4ef3256fcf81df85fd16346a6&v=4)](https://github.com/saqib-ahmed)

Sorry, something went wrong.

Quote reply

###

**[saqib-ahmed](https://github.com/saqib-ahmed)** commented [Feb 18, 2020](https://github.com/puppeteer/puppeteer/issues/3149#issuecomment-587395906) •

edited

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">
                    <a
                        class="user-mention notranslate"
                        data-hovercard-type="user"
                        data-hovercard-url="/users/Hretic/hovercard"
                        data-octo-click="hovercard-link-click"
                        data-octo-dimensions="link_type:self"
                        href="https://github.com/Hretic"
                        >@Hretic</a
                    >
                    Can you please share the fixed/updated code? I have a
                    similar use case as you had and I didn't quite get where to
                    register that event emitter.
                </p>
                <p dir="auto">
                    Also, when do you call
                    <code class="notranslate">browser.close()</code>, if ever?
                </p>
            </td>
        </tr>
    </tbody>
</table>
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

All reactions

Sorry, something went wrong.

[![@phanminhtai](https://avatars.githubusercontent.com/u/53898609?s=80&u=4bc429202aab2671038dff840d6616fdbd27d970&v=4)](https://github.com/phanminhtai)

Sorry, something went wrong.

Quote reply

###

**[phanminhtai](https://github.com/phanminhtai)** commented [Sep 4, 2020](https://github.com/puppeteer/puppeteer/issues/3149#issuecomment-687039121)

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <blockquote>
                    <p dir="auto">
                        <a
                            class="user-mention notranslate"
                            data-hovercard-type="user"
                            data-hovercard-url="/users/Hretic/hovercard"
                            data-octo-click="hovercard-link-click"
                            data-octo-dimensions="link_type:self"
                            href="https://github.com/Hretic"
                            >@Hretic</a
                        >
                        Can you please share the fixed/updated code? I have a
                        similar use case as you had and I didn't quite get where
                        to register that event emitter.
                    </p>
                    <p dir="auto">
                        Also, when do you call
                        <code class="notranslate">browser.close()</code>, if
                        ever?
                    </p>
                </blockquote>
                <p dir="auto">
                    Here bro:
                    <a
                        href="https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working"
                        rel="nofollow"
                        >https://stackoverflow.com/questions/52045600/puppeteer-how-check-if-browser-is-still-open-and-working</a
                    >
                </p>
            </td>
        </tr>
    </tbody>
</table>
```

-   👍 - 👎 - 😄 - 🎉 - 😕 - ❤️ - 🚀 - 👀 All reactions Sorry, something went
    wrong.
    [![@Gordon2735](https://avatars.githubusercontent.com/u/81874061?s=80&v=4)](https://github.com/Gordon2735)

#### Add a comment

```

```

```

```
