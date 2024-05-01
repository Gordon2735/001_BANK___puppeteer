# Error "undefined" launching browser process when using `node:18-buster` Docker image and installing dependencies listed on website #10285

Closed

2 tasks

[mattwelke](https://github.com/mattwelke) opened this issue May 31, 2023 · 7 comments

Closed

2 tasks

# [\[Bug\]: Error "undefined" launching browser process when using `node:18-buster` Docker image and installing dependencies listed on website](https://github.com/puppeteer/puppeteer/issues/10285#top) #10285

[mattwelke](https://github.com/mattwelke) opened this issue May 31, 2023 · 7 comments

Labels

[bug](https://github.com/puppeteer/puppeteer/labels/bug) [needs-feedback](https://github.com/puppeteer/puppeteer/labels/needs-feedback) [not-reproducible](https://github.com/puppeteer/puppeteer/labels/not-reproducible)

## Comments

[![@mattwelke](https://avatars.githubusercontent.com/u/7719209?s=80&u=80f02a799323b1472b389b836d95957c93a6d856&v=4)](https://github.com/mattwelke)

Sorry, something went wrong.

Quote reply

Contributor

###

**[mattwelke](https://github.com/mattwelke)** commented [May 31, 2023](https://github.com/puppeteer/puppeteer/issues/10285#issue-1734980139) •

edited

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><h3 dir="auto">Bug expectation</h3><p dir="auto"><strong>Summary:</strong></p><p dir="auto">I expected Node.js to be able to execute a script that uses Puppeteer to read an element from a website, with the script being based on the example from the website:</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-c">// Import puppeteer</span>
<span class="pl-k">import</span> <span class="pl-s1">puppeteer</span> <span class="pl-k">from</span> <span class="pl-s">'puppeteer'</span><span class="pl-kos">;</span>

<span class="pl-kos">(</span><span class="pl-k">async</span> <span class="pl-kos">(</span><span class="pl-kos">)</span> <span class="pl-c1">=&gt;</span> <span class="pl-kos">{</span>
<span class="pl-c">// Launch the browser</span>
<span class="pl-k">const</span> <span class="pl-s1">browser</span> <span class="pl-c1">=</span> <span class="pl-k">await</span> <span class="pl-s1">puppeteer</span><span class="pl-kos">.</span><span class="pl-en">launch</span><span class="pl-kos">(</span><span class="pl-kos">{</span>
<span class="pl-c1">headless</span>: <span class="pl-s">'new'</span><span class="pl-kos">,</span>
<span class="pl-kos">}</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

    <span class="pl-c">// Create a page</span>
    <span class="pl-k">const</span> <span class="pl-s1">page</span> <span class="pl-c1">=</span> <span class="pl-k">await</span> <span class="pl-s1">browser</span><span class="pl-kos">.</span><span class="pl-en">newPage</span><span class="pl-kos">(</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

    <span class="pl-c">// Go to your site</span>
    <span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">goto</span><span class="pl-kos">(</span><span class="pl-s">'https://pptr.dev/guides/query-selectors'</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

    <span class="pl-c">// Query for an element handle.</span>
    <span class="pl-k">const</span> <span class="pl-s1">inner_html</span> <span class="pl-c1">=</span> <span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">$eval</span><span class="pl-kos">(</span><span class="pl-s">'h1'</span><span class="pl-kos">,</span> <span class="pl-s1">element</span> <span class="pl-c1">=&gt;</span> <span class="pl-s1">element</span><span class="pl-kos">.</span><span class="pl-c1">innerHTML</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

    <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">`Inner HTML: <span class="pl-s1"><span class="pl-kos">${</span><span class="pl-s1">inner_html</span><span class="pl-kos">}</span></span>`</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

    <span class="pl-c">// Close browser.</span>
    <span class="pl-k">await</span> <span class="pl-s1">browser</span><span class="pl-kos">.</span><span class="pl-en">close</span><span class="pl-kos">(</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

<span class="pl-kos">}</span><span class="pl-kos">)</span><span class="pl-kos">(</span><span class="pl-kos">)</span><span class="pl-kos">;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="// Import puppeteer
import puppeteer from 'puppeteer';

```javascript
(async () = {
// Launch the browser
const browser = await puppeteer.launch({
headless: 'new',
});

    // Create a page
    const page = await browser.newPage();

    // Go to your site
    await page.goto('https://pptr.dev/guides/query-selectors');

    // Query for an element handle.
    const inner_html = await page.$eval('h1', element =&gt; element.innerHTML);

    console.log(`Inner HTML: ${inner_html}`);

    // Close browser.
    await browser.close();

})();
```

````css
" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">Instead, Node.js encountered an error launching the browser process:</p><div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code class="notranslate">
```


file:///usr/src/app/node_modules/@puppeteer/browsers/lib/esm/launch.js:250

```typescript
reject(new Error([
^
````

Error: Failed to launch the browser process! undefined
[18:18:0531/203130.811200:ERROR:zygote_host_impl_linux.cc(100)] Running as root without --no-sandbox is not supported. See https://crbug.com/638180.

TROUBLESHOOTING: https://pptr.dev/troubleshooting

    at ChildProcess.onClose (file:///usr/src/app/node_modules/@puppeteer/browsers/lib/esm/launch.js:250:24)
    at ChildProcess.emit (node:events:525:35)
    at ChildProcess._handle.onexit (node:internal/child_process:291:12)

Node.js v18.16.

```html
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="file:///usr/src/app/node_modules/@puppeteer/browsers/lib/esm/launch.js:250"
```

```typescript
reject(new Error([
^

Error: Failed to launch the browser process! undefined
[18:18:0531/203130.811200:ERROR:zygote_host_impl_linux.cc(100)]
```

Running as root without --no-sandbox is not supported. See https://crbug.com/638180.

TROUBLESHOOTING: https://pptr.dev/troubleshooting

    at ChildProcess.onClose (file:///usr/src/app/node_modules/@puppeteer/browsers/lib/esm/launch.js:250:24)
    at ChildProcess.emit (node:events:525:35)
    at ChildProcess._handle.onexit (node:internal/child_process:291:12)

Node.js v18.16.0"

```html
tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">Notably, this error occurred even after I tried installing the list of dependencies on the Puppeteer website <em>and</em> after I tried installing the list of dependencies on the Chromium website.</p><p dir="auto"><strong>Details (with reproduction example):</strong></p><p dir="auto">I'm running into a problem getting this to work with the latest version of the <code class="notranslate">node:18-buster</code> Docker image.</p><p dir="auto">I have a Node.js script that works if I run it locally without using Docker. It's a slightly modified version of the one I found in the website "getting started" content.</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-c">// Import puppeteer</span>
<span class="pl-k">import</span> <span class="pl-s1">puppeteer</span> <span class="pl-k">from</span> <span class="pl-s">'puppeteer'</span><span class="pl-kos">;</span>

<span class="pl-kos">(</span><span class="pl-k">async</span> <span class="pl-kos">(</span><span class="pl-kos">)</span> <span class="pl-c1">=&gt;</span> <span class="pl-kos">{</span>
<span class="pl-c">// Launch the browser</span>
<span class="pl-k">const</span> <span class="pl-s1">browser</span> <span class="pl-c1">=</span> <span class="pl-k">await</span> <span class="pl-s1">puppeteer</span><span class="pl-kos">.</span><span class="pl-en">launch</span><span class="pl-kos">(</span><span class="pl-kos">{</span>
<span class="pl-c1">headless</span>: <span class="pl-s">'new'</span><span class="pl-kos">,</span>
<span class="pl-kos">}</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

    <span class="pl-c">// Create a page</span>
    <span class="pl-k">const</span> <span class="pl-s1">page</span> <span class="pl-c1">=</span> <span class="pl-k">await</span> <span class="pl-s1">browser</span><span class="pl-kos">.</span><span class="pl-en">newPage</span><span class="pl-kos">(</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

    <span class="pl-c">// Go to your site</span>
    <span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">goto</span><span class="pl-kos">(</span><span class="pl-s">'https://pptr.dev/guides/query-selectors'</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

    <span class="pl-c">// Query for an element handle.</span>
    <span class="pl-k">const</span> <span class="pl-s1">inner_html</span> <span class="pl-c1">=</span> <span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">$eval</span><span class="pl-kos">(</span><span class="pl-s">'h1'</span><span class="pl-kos">,</span> <span class="pl-s1">element</span> <span class="pl-c1">=&gt;</span> <span class="pl-s1">element</span><span class="pl-kos">.</span><span class="pl-c1">innerHTML</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

    <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">`Inner HTML: <span class="pl-s1"><span class="pl-kos">${</span><span class="pl-s1">inner_html</span><span class="pl-kos">}</span></span>`</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

    <span class="pl-c">// Close browser.</span>
    <span class="pl-k">await</span> <span class="pl-s1">browser</span><span class="pl-kos">.</span><span class="pl-en">close</span><span class="pl-kos">(</span><span class="pl-kos">)</span><span class="pl-kos">;</span>

<span class="pl-kos">}</span><span class="pl-kos">)</span><span class="pl-kos">(</span><span class="pl-kos">)</span><span class="pl-kos">;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="// Import puppeteer
import puppeteer from 'puppeteer';
```

```javascript
(async () =&gt; {
// Launch the browser
const browser = await puppeteer.launch({
headless: 'new',
});

    // Create a page
    const page = await browser.newPage();

    // Go to your site
    await page.goto('https://pptr.dev/guides/query-selectors');

    // Query for an element handle.
    const inner_html = await page.$eval('h1', element =&gt; element.innerHTML);

    console.log(`Inner HTML: ${inner_html}`);

    // Close browser.
    await browser.close();

})();
```

```html
" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code class="notranslate">$ node index.mjs
Inner HTML: Query Selectors
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="$ node index.mjs
Inner HTML: Query Selectors" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">(this output is good, because that's what the website has right now)</p><p dir="auto">Then, I tried to Dockerize it because my ultimate goal is to create a runtime for a FaaS provider that would allow users to use Puppeteer from their code. I started with a simple Dockerfile that I expected would not work because I'm not installing anything to support Puppeteer.</p><div class="highlight highlight-source-dockerfile notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">FROM</span> node:18-buster

<span class="pl-k">WORKDIR</span> /usr/src/app

<span class="pl-k">COPY</span> package\*.json ./

<span class="pl-k">RUN</span> npm install

<span class="pl-k">COPY</span> . .

<span class="pl-k">CMD</span> [ <span class="pl-s">"node"</span>, <span class="pl-s">"index.mjs"</span> ]</pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="FROM node:18-buster
```

```bash
WORKDIR /usr/src/app

COPY package\*.json ./

RUN npm install

COPY . .
```

```html
CMD [ &quot;node&quot;, &quot;index.mjs&quot; ]" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">I got an error related to starting the process, like I expected.</p><div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code class="notranslate">Error: Failed to launch the browser process!
/root/.cache/puppeteer/chrome/linux-113.0.5672.63/chrome-linux64/chrome: error while loading shared libraries: libnss3.so: cannot open shared object file: No such file or directory

TROUBLESHOOTING: https://pptr.dev/troubleshooting
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="Error: Failed to launch the browser process!
/root/.cache/puppeteer/chrome/linux-113.0.5672.63/chrome-linux64/chrome: error while loading shared libraries: libnss3.so: cannot open shared object file: No such file or directory

TROUBLESHOOTING: https://pptr.dev/troubleshooting" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">I read that web page, got to <a href="https://pptr.dev/troubleshooting#chrome-headless-doesnt-launch-on-unix" rel="nofollow">the UNIX instructions</a> specifically, and made a new Dockerfile that installs those dependencies.</p><div class="highlight highlight-source-dockerfile notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">FROM</span> node:18-buster

<span class="pl-c"><span class="pl-c">#</span> Install system packages for puppeteer NPM dependency</span>
<span class="pl-k">RUN</span>

apt-get -y update \
 &amp;&amp; apt-get -y install --no-install-recommends \
 ca-certificates \
 fonts-liberation \
 libasound2 \
 libatk-bridge2.0-0 \
 libatk1.0-0 \
 libc6 \
 libcairo2 \
 libcups2 \
 libdbus-1-3 \
 libexpat1 \
 libfontconfig1 \
 libgbm1 \
 libgcc1 \
 libglib2.0-0 \
 libgtk-3-0 \
 libnspr4 \
 libnss3 \
 libpango-1.0-0 \
 libpangocairo-1.0-0 \
 libstdc++6 \
 libx11-6 \
 libx11-xcb1 \
 libxcb1 \
 libxcomposite1 \
 libxcursor1 \
 libxdamage1 \
 libxext6 \
 libxfixes3 \
 libxi6 \
 libxrandr2 \
 libxrender1 \
 libxss1 \
 libxtst6 \
 lsb-release \
 wget \
 xdg-utils \
 &amp;&amp; apt-get clean \
 &amp;&amp; rm -rf /var/lib/apt/lists/\*

<span class="pl-k">WORKDIR</span> /usr/src/app

<span class="pl-k">COPY</span> package\*.json ./

<span class="pl-k">RUN</span> npm install

<span class="pl-k">COPY</span> . .

<span class="pl-k">CMD</span> [ <span class="pl-s">"node"</span>, <span class="pl-s">"index.mjs"</span> ]</pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="FROM node:18-
```

# Install system packages for puppeteer NPM dependency

RUN apt-get -y update \
 &amp;&amp; apt-get -y install --no-install-recommends \
 ca-certificates \
 fonts-liberation \
 libasound2 \
 libatk-bridge2.0-0 \
 libatk1.0-0 \
 libc6 \
 libcairo2 \
 libcups2 \
 libdbus-1-3 \
 libexpat1 \
 libfontconfig1 \
 libgbm1 \
 libgcc1 \
 libglib2.0-0 \
 libgtk-3-0 \
 libnspr4 \
 libnss3 \
 libpango-1.0-0 \
 libpangocairo-1.0-0 \
 libstdc++6 \
 libx11-6 \
 libx11-xcb1 \
 libxcb1 \
 libxcomposite1 \
 libxcursor1 \
 libxdamage1 \
 libxext6 \
 libxfixes3 \
 libxi6 \
 libxrandr2 \
 libxrender1 \
 libxss1 \
 libxtst6 \
 lsb-release \
 wget \
 xdg-utils \
 &amp;&amp; apt-get clean \
 &amp;&amp; rm -rf /var/lib/apt/lists/\*

```bash
WORKDIR /usr/src/app

COPY package\*.json ./

RUN npm install

COPY . .
```

```html
CMD [ &quot;node&quot;, &quot;index.mjs&quot; ]" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">This didn't work though, which surprised me. It was especially surprising because the error message said the error was "undefined".</p><div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code class="notranslate">Error: Failed to launch the browser process! undefined
[18:18:0531/201731.497189:ERROR:zygote_host_impl_linux.cc(100)] Running as root without --no-sandbox is not supported. See https://crbug.com/638180.
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="Error: Failed to launch the browser process! undefined
[18:18:0531/201731.497189:ERROR:zygote_host_impl_linux.cc(100)] Running as root without --no-sandbox is not supported. See https://crbug.com/638180." tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">I decided to troubleshoot because the website says:</p><blockquote><p dir="auto">Also, see <a href="https://source.chromium.org/chromium/chromium/src/+/main:chrome/installer/linux/debian/dist_package_versions.json" rel="nofollow">https://source.chromium.org/chromium/chromium/src/+/main:chrome/installer/linux/debian/dist_package_versions.json</a> for the up-to-date list of dependencies declared by the Chrome installer.</p></blockquote><p dir="auto">I followed that link and found a new set of dependencies, listed under "Debian 10 (Buster)". I made a new Dockerfile using them.</p><div class="highlight highlight-source-dockerfile notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">FROM</span> node:18-buster

<span class="pl-c"><span class="pl-c">#</span> Install system packages for puppeteer NPM dependency</span>
<span class="pl-c"><span class="pl-c">#</span> From source.chromium.org</span>
<span class="pl-k">RUN</span>

apt-get update &amp;&amp; apt-get install -y --no-install-recommends \
 libasound2=1.1.8-1 \
 libatk-bridge2.0-0=2.30.0-5 \
 libatk1.0-0=2.30.0-2 \
 libatspi2.0-0=2.30.0-7 \
 libc6=2.28-10+deb10u1 \
 libcairo2=1.16.0-4+deb10u1 \
 libcups2=2.2.10-6+deb10u5 \
 libdbus-1-3=1.12.20-0+deb10u1 \
 libdrm2=2.4.97-1 \
 libexpat1=2.2.6-2+deb10u4 \
 libgbm1=18.3.6-2+deb10u1 \
 libgcc1=1:8.3.0-6 \
 libglib2.0-0=2.58.3-2+deb10u3 \
 libnspr4=2:4.20-1 \
 libnss3=2:3.42.1-1+deb10u5 \
 libpango-1.0-0=1.42.4-7~deb10u1 \
 libpangocairo-1.0-0=1.42.4-7~deb10u1 \
 libstdc++6=8.3.0-6 \
 libuuid1=2.33.1-0.1 \
 libx11-6=2:1.6.7-1+deb10u2 \
 libx11-xcb1=2:1.6.7-1+deb10u2 \
 libxcb-dri3-0=1.13.1-2 \
 libxcb1=1.13.1-2 \
 libxcomposite1=1:0.4.4-2 \
 libxcursor1=1:1.1.15-2 \
 libxdamage1=1:1.1.4-3+b3 \
 libxext6=2:1.3.3-1+b2 \
 libxfixes3=1:5.0.3-1 \
 libxi6=2:1.7.9-1 \
 libxkbcommon0=0.8.2-1 \
 libxrandr2=2:1.5.1-1 \
 libxrender1=1:0.9.10-1 \
 libxshmfence1=1.3-1 \
 libxss1=1:1.2.3-1 \
 libxtst6=2:1.2.3-1 \
 &amp;&amp; apt-get clean \
 &amp;&amp; rm -rf /var/lib/apt/lists/\*

<span class="pl-k">WORKDIR</span> /usr/src/app

<span class="pl-k">COPY</span> package\*.json ./

<span class="pl-k">RUN</span> npm install

<span class="pl-k">COPY</span> . .

<span class="pl-k">CMD</span> [ <span class="pl-s">"node"</span>, <span class="pl-s">"index.mjs"</span> ]

</pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="FROM node:18-buster
```

# Install system packages for puppeteer NPM dependency

# From source.chromium.org

```bash
RUN apt-get update &amp;&amp; apt-get install -y --no-install-recommends \
 libasound2=1.1.8-1 \
 libatk-bridge2.0-0=2.30.0-5 \
 libatk1.0-0=2.30.0-2 \
 libatspi2.0-0=2.30.0-7 \
 libc6=2.28-10+deb10u1 \
 libcairo2=1.16.0-4+deb10u1 \
 libcups2=2.2.10-6+deb10u5 \
 libdbus-1-3=1.12.20-0+deb10u1 \
 libdrm2=2.4.97-1 \
 libexpat1=2.2.6-2+deb10u4 \
 libgbm1=18.3.6-2+deb10u1 \
 libgcc1=1:8.3.0-6 \
 libglib2.0-0=2.58.3-2+deb10u3 \
 libnspr4=2:4.20-1 \
 libnss3=2:3.42.1-1+deb10u5 \
 libpango-1.0-0=1.42.4-7~deb10u1 \
 libpangocairo-1.0-0=1.42.4-7~deb10u1 \
 libstdc++6=8.3.0-6 \
 libuuid1=2.33.1-0.1 \
 libx11-6=2:1.6.7-1+deb10u2 \
 libx11-xcb1=2:1.6.7-1+deb10u2 \
 libxcb-dri3-0=1.13.1-2 \
 libxcb1=1.13.1-2 \
 libxcomposite1=1:0.4.4-2 \
 libxcursor1=1:1.1.15-2 \
 libxdamage1=1:1.1.4-3+b3 \
 libxext6=2:1.3.3-1+b2 \
 libxfixes3=1:5.0.3-1 \
 libxi6=2:1.7.9-1 \
 libxkbcommon0=0.8.2-1 \
 libxrandr2=2:1.5.1-1 \
 libxrender1=1:0.9.10-1 \
 libxshmfence1=1.3-1 \
 libxss1=1:1.2.3-1 \
 libxtst6=2:1.2.3-1 \
 &amp;&amp; apt-get clean \
 &amp;&amp; rm -rf /var/lib/apt/lists/\*

WORKDIR /usr/src/app

COPY package\*.json ./

RUN npm install

COPY . .
```

```html
CMD [ &quot;node&quot;, &quot;index.mjs&quot; ]
" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">This time, the Docker image build didn't even complete. Among the errors output by the build were:</p><div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code class="notranslate">#0 2.690 E: Version '2.2.10-6+deb10u5' for 'libcups2' was not found
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="#0 2.690 E: Version '2.2.10-6+deb10u5' for 'libcups2' was not found" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">I was able to find information about <a href="https://packages.debian.org/buster/libcups2" rel="nofollow">libcups2</a>. This is when I learned that the most recent version of that package is <code class="notranslate">2.2.10-6+deb10u6</code> right now, not <code class="notranslate">2.2.10-6+deb10u5</code>. After more troubleshooting, I realized that Debian doesn't seem to publish any version except the most recent version of each package (I tested this with another dependency from that list too).</p><p dir="auto">So then I thought a way to get it working could be to remove the version numbers from that list of dependencies from the Chromium website so that it ends up installing the latest version of each.</p><div class="highlight highlight-source-dockerfile notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">FROM</span> node:18-buster

<span class="pl-c"><span class="pl-c">#</span> From source.chromium.org, with the specific versions removed.</span>
<span class="pl-k">RUN</span> apt-get update &amp;&amp; apt-get install -y --no-install-recommends \
 libasound2 \
 libatk-bridge2.0-0 \
 libatk1.0-0 \
 libatspi2.0-0 \
 libc6 \
 libcairo2 \
 libcups2 \
 libdbus-1-3 \
 libdrm2 \
 libexpat1 \
 libgbm1 \
 libgcc1 \
 libglib2.0-0 \
 libnspr4 \
 libnss3 \
 libpango-1.0-0 \
 libpangocairo-1.0-0 \
 libstdc++6 \
 libuuid1 \
 libx11-6 \
 libx11-xcb1 \
 libxcb-dri3-0 \
 libxcb1 \
 libxcomposite1 \
 libxcursor1 \
 libxdamage1 \
 libxext6 \
 libxfixes3 \
 libxi6 \
 libxkbcommon0 \
 libxrandr2 \
 libxrender1 \
 libxshmfence1 \
 libxss1 \
 libxtst6 \
 &amp;&amp; apt-get clean \
 &amp;&amp; rm -rf /var/lib/apt/lists/\*

<span class="pl-k">WORKDIR</span> /usr/src/app

<span class="pl-k">COPY</span> package\*.json ./

<span class="pl-k">RUN</span> npm install

<span class="pl-k">COPY</span> . .

<span class="pl-k">CMD</span> [ <span class="pl-s">"node"</span>, <span class="pl-s">"index.mjs"</span> ]</pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="FROM node:18-buster
```

# From source.chromium.org, with the specific versions removed.

```bash
RUN apt-get update &amp;&amp; apt-get install -y --no-install-recommends \
 libasound2 \
 libatk-bridge2.0-0 \
 libatk1.0-0 \
 libatspi2.0-0 \
 libc6 \
 libcairo2 \
 libcups2 \
 libdbus-1-3 \
 libdrm2 \
 libexpat1 \
 libgbm1 \
 libgcc1 \
 libglib2.0-0 \
 libnspr4 \
 libnss3 \
 libpango-1.0-0 \
 libpangocairo-1.0-0 \
 libstdc++6 \
 libuuid1 \
 libx11-6 \
 libx11-xcb1 \
 libxcb-dri3-0 \
 libxcb1 \
 libxcomposite1 \
 libxcursor1 \
 libxdamage1 \
 libxext6 \
 libxfixes3 \
 libxi6 \
 libxkbcommon0 \
 libxrandr2 \
 libxrender1 \
 libxshmfence1 \
 libxss1 \
 libxtst6 \
 &amp;&amp; apt-get clean \
 &amp;&amp; rm -rf /var/lib/apt/lists/\*

WORKDIR /usr/src/app

COPY package\*.json ./

RUN npm install

COPY . .
```

```html
CMD [ &quot;node&quot;, &quot;index.mjs&quot; ]" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">This didn't work either. It was the same "undefined" error again.</p><div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code class="notranslate">Error: Failed to launch the browser process! undefined
[18:18:0531/202504.802808:ERROR:zygote_host_impl_linux.cc(100)] Running as root without --no-sandbox is not supported. See https://crbug.com/638180.
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="Error: Failed to launch the browser process! undefined
[18:18:0531/202504.802808:ERROR:zygote_host_impl_linux.cc(100)] Running as root without --no-sandbox is not supported. See https://crbug.com/638180." tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">This concluded my troubleshooting. At this point, I came to the conclusion that either I was doing something wrong or that either the list of required dependencies for Debian on the Puppeteer website or on the Chromium website are out of date.</p><p dir="auto">I think it's also worth noting that there appear to be <a href="https://github.com/puppeteer/puppeteer/issues/290" data-hovercard-type="issue" data-hovercard-url="/puppeteer/puppeteer/issues/290/hovercard">other people recently experiencing issues running Puppeteer on Debian too</a>.</p><h3 dir="auto">Bug behavior</h3><ul class="contains-task-list"><li class="task-list-item"><span class="handle"><svg class="drag-handle" aria-hidden="true" width="16" height="16"><path d="M10 13a1 1 0 100-2 1 1 0 000 2zm-4 0a1 1 0 100-2 1 1 0 000 2zm1-5a1 1 0 11-2 0 1 1 0 012 0zm3 1a1 1 0 100-2 1 1 0 000 2zm1-5a1 1 0 11-2 0 1 1 0 012 0zM6 5a1 1 0 100-2 1 1 0 000 2z"></path></svg></span><input type="checkbox" id="" disabled="" class="task-list-item-checkbox"> Flaky</li><li class="task-list-item"><span class="handle"><svg class="drag-handle" aria-hidden="true" width="16" height="16"><path d="M10 13a1 1 0 100-2 1 1 0 000 2zm-4 0a1 1 0 100-2 1 1 0 000 2zm1-5a1 1 0 11-2 0 1 1 0 012 0zm3 1a1 1 0 100-2 1 1 0 000 2zm1-5a1 1 0 11-2 0 1 1 0 012 0zM6 5a1 1 0 100-2 1 1 0 000 2z"></path></svg></span><input type="checkbox" id="" disabled="" class="task-list-item-checkbox"> PDF</li></ul><h3 dir="auto">Minimal, reproducible example</h3><div class="highlight highlight-source-ts notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-smi">Minimal</span> <span class="pl-s1">example</span> is <span class="pl-s1">multiple</span> <span class="pl-s1">files</span><span class="pl-kos">,</span> <span class="pl-s1">so</span> <span class="pl-s1">see</span> <span class="pl-s1">detailed</span> <span class="pl-s1">reproducible</span> <span class="pl-s1">example</span> <span class="pl-s1">above</span><span class="pl-kos">.</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="Minimal example is multiple files, so see detailed reproducible example above." tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><h3 dir="auto">Error string</h3><p dir="auto">Error: Failed to launch the browser process! undefined</p><h3 dir="auto">Puppeteer configuration</h3><p dir="auto"><em>No response</em></p><h3 dir="auto">Puppeteer version</h3><p dir="auto">20.5.0</p><h3 dir="auto">Node version</h3><p dir="auto">18.16.0</p><h3 dir="auto">Package manager</h3><p dir="auto">npm</p><h3 dir="auto">Package manager version</h3><p dir="auto">9.6.7</p><h3 dir="auto">Operating system</h3><p dir="auto">Linux</p></td></tr><tr class="d-block pl-3 pr-3 pb-3 js-comment-body-error" hidden=""><td class="d-block"><div class="flash flash-warn" role="alert"><p class="mb-1"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-info"><path d="M0 8a8 8 0 1 1 16 0A8 8 0 0 1 0 8Zm8-6.5a6.5 6.5 0 1 0 0 13 6.5 6.5 0 0 0 0-13ZM6.5 7.75A.75.75 0 0 1 7.25 7h1a.75.75 0 0 1 .75.75v2.75h.25a.75.75 0 0 1 0 1.5h-2a.75.75 0 0 1 0-1.5h.25v-2h-.25a.75.75 0 0 1-.75-.75ZM8 6a1 1 0 1 1 0-2 1 1 0 0 1 0 2Z"></path></svg>The text was updated successfully, but these errors were encountered:</p><ol class="mb-0 pl-4 ml-4"></ol></div></td></tr></tbody></table>
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 1 lianghua1987 reacted with thumbs up emoji

All reactions

-   👍 1 reaction

[![@mattwelke](https://avatars.githubusercontent.com/u/7719209?s=40&u=80f02a799323b1472b389b836d95957c93a6d856&v=4)](https://github.com/mattwelke) [mattwelke](https://github.com/mattwelke) added the [ bug ](https://github.com/puppeteer/puppeteer/labels/bug) label [May 31, 2023](https://github.com/puppeteer/puppeteer/issues/10285#event-9395253746)

[![@github-actions](https://avatars.githubusercontent.com/in/15368?s=40&v=4)](https://github.com/apps/github-actions) [github-actions](https://github.com/apps/github-actions) bot added [ needs-feedback ](https://github.com/puppeteer/puppeteer/labels/needs-feedback) [ not-reproducible ](https://github.com/puppeteer/puppeteer/labels/not-reproducible) labels [May 31, 2023](https://github.com/puppeteer/puppeteer/issues/10285#event-9395287868)

[![@github-actions](https://avatars.githubusercontent.com/in/15368?s=80&v=4)](https://github.com/apps/github-actions)

Sorry, something went wrong.

Quote reply

###

**[github-actions](https://github.com/apps/github-actions) bot** commented [May 31, 2023](https://github.com/puppeteer/puppeteer/issues/10285#issuecomment-1570923218)

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">
                    This issue was not reproducible. Please check that your
                    example runs locally and the following:
                </p>
                <ul dir="auto">
                    <li>
                        Ensure the script does not rely on dependencies outside
                        of <code class="notranslate">puppeteer</code> and
                        <code class="notranslate">puppeteer-core</code>.
                    </li>
                    <li>
                        Ensure the error string is just the error message.
                        <ul dir="auto">
                            <li>
                                <p dir="auto">Bad:</p>
                                <div
                                    class="highlight highlight-source-ts notranslate position-relative overflow-auto"
                                    dir="auto"
                                >
                                    <pre
                                        class="notranslate"
                                    >Error: <span class="pl-s1">something</span> <span class="pl-s1">went</span> <span class="pl-s1">wrong</span>
  <span class="pl-s1">at</span> <span class="pl-smi">Object</span><span class="pl-kos">.</span><span class="pl-c1">&lt;</span><span class="pl-s1">anonymous</span><span class="pl-c1">&gt;</span> <span class="pl-kos">(</span><span class="pl-pds"><span class="pl-c1">/</span>Users<span class="pl-c1">/</span>username</span><span class="pl-c1">/</span><span class="pl-s1">repository</span><span class="pl-c1">/</span><span class="pl-s1">script</span><span class="pl-kos">.</span><span class="pl-c1">js</span>:<span class="pl-c1">2</span>:<span class="pl-c1">1</span><span class="pl-kos">)</span>
  <span class="pl-s1">at</span> <span class="pl-smi">Module</span><span class="pl-kos">.</span><span class="pl-en">_compile</span> <span class="pl-kos">(</span><span class="pl-s1">node</span>:<span class="pl-s1">internal</span><span class="pl-c1">/</span><span class="pl-s1">modules</span><span class="pl-c1">/</span><span class="pl-s1">cjs</span><span class="pl-c1">/</span><span class="pl-s1">loader</span>:<span class="pl-c1">1159</span>:<span class="pl-c1">14</span><span class="pl-kos">)</span>
  <span class="pl-s1">at</span> <span class="pl-smi">Module</span><span class="pl-kos">.</span><span class="pl-c1">_extensions</span><span class="pl-kos">.</span><span class="pl-kos">.</span><span class="pl-en">js</span> <span class="pl-kos">(</span><span class="pl-s1">node</span>:<span class="pl-s1">internal</span><span class="pl-c1">/</span><span class="pl-s1">modules</span><span class="pl-c1">/</span><span class="pl-s1">cjs</span><span class="pl-c1">/</span><span class="pl-s1">loader</span>:<span class="pl-c1">1213</span>:<span class="pl-c1">10</span><span class="pl-kos">)</span>
  <span class="pl-s1">at</span> <span class="pl-smi">Module</span><span class="pl-kos">.</span><span class="pl-en">load</span> <span class="pl-kos">(</span><span class="pl-s1">node</span>:<span class="pl-s1">internal</span><span class="pl-c1">/</span><span class="pl-s1">modules</span><span class="pl-c1">/</span><span class="pl-s1">cjs</span><span class="pl-c1">/</span><span class="pl-s1">loader</span>:<span class="pl-c1">1037</span>:<span class="pl-c1">32</span><span class="pl-kos">)</span>
  <span class="pl-s1">at</span> <span class="pl-smi">Module</span><span class="pl-kos">.</span><span class="pl-en">_load</span> <span class="pl-kos">(</span><span class="pl-s1">node</span>:<span class="pl-s1">internal</span><span class="pl-c1">/</span><span class="pl-s1">modules</span><span class="pl-c1">/</span><span class="pl-s1">cjs</span><span class="pl-c1">/</span><span class="pl-s1">loader</span>:<span class="pl-c1">878</span>:<span class="pl-c1">12</span><span class="pl-kos">)</span>
  <span class="pl-s1">at</span> <span class="pl-smi">Function</span><span class="pl-kos">.</span><span class="pl-c1">executeUserEntryPoint</span> <span class="pl-kos">[</span><span class="pl-s1">as</span> <span class="pl-s1">runMain</span><span class="pl-kos">]</span> <span class="pl-kos">(</span><span class="pl-s1">node</span>:<span class="pl-s1">internal</span><span class="pl-c1">/</span><span class="pl-s1">modules</span><span class="pl-c1">/</span><span class="pl-s1">run_main</span>:<span class="pl-c1">81</span>:<span class="pl-c1">12</span><span class="pl-kos">)</span>
  at <span class="pl-s1">node</span>:<span class="pl-s1">internal</span><span class="pl-c1">/</span><span class="pl-s1">main</span><span class="pl-c1">/</span><span class="pl-s1">run_main_module</span>:<span class="pl-c1">23</span>:<span class="pl-c1">47</span></pre>
                                    <div
                                        class="zeroclipboard-container position-absolute right-0 top-0"
                                    >
                                        <clipboard-copy
                                            aria-label="Copy"
                                            class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay"
                                            data-copy-feedback="Copied!"
                                            data-tooltip-direction="w"
                                            value="Error: something went wrong
  at Object.&lt;anonymous&gt; (/Users/username/repository/script.js:2:1)
  at Module._compile (node:internal/modules/cjs/loader:1159:14)
  at Module._extensions..js (node:internal/modules/cjs/loader:1213:10)
  at Module.load (node:internal/modules/cjs/loader:1037:32)
  at Module._load (node:internal/modules/cjs/loader:878:12)
  at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:81:12)
  at node:internal/main/run_main_module:23:47"
                                            tabindex="0"
                                            role="button"
                                            ><svg
                                                aria-hidden="true"
                                                height="16"
                                                viewBox="0 0 16 16"
                                                version="1.1"
                                                width="16"
                                                data-view-component="true"
                                                class="octicon octicon-copy js-clipboard-copy-icon m-2"
                                            >
                                                <path
                                                    d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"
                                                ></path>
                                                <path
                                                    d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"
                                                ></path></svg
                                            ><svg
                                                aria-hidden="true"
                                                height="16"
                                                viewBox="0 0 16 16"
                                                version="1.1"
                                                width="16"
                                                data-view-component="true"
                                                class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"
                                            >
                                                <path
                                                    d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"
                                                ></path></svg
                                        ></clipboard-copy>
                                    </div>
                                </div>
                            </li>
                            <li>
                                <p dir="auto">
                                    Good:
                                    <code class="notranslate"
                                        >Error: something went wrong</code
                                    >.
                                </p>
                            </li>
                        </ul>
                    </li>
                    <li>
                        Ensure your configuration file (if applicable) is valid.
                    </li>
                    <li>
                        If the issue is flaky (does not reproduce all the time),
                        make sure 'Flaky' is checked.
                    </li>
                    <li>
                        If the issue is not expected to error, make sure to
                        write 'no error'.
                    </li>
                </ul>
                <p dir="auto">
                    Once the above checks are satisfied, please edit your issue
                    with the changes and we will<br />try to reproduce the bug
                    again.
                </p>
                <hr />
                <p dir="auto">
                    <a
                        href="https://github.com/puppeteer/puppeteer/actions/runs/5137489008"
                        >Analyzer run</a
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

All reactions

Sorry, something went wrong.

[![@mattwelke](https://avatars.githubusercontent.com/u/7719209?s=80&u=80f02a799323b1472b389b836d95957c93a6d856&v=4)](https://github.com/mattwelke)

Sorry, something went wrong.

Quote reply

Contributor Author

###

**[mattwelke](https://github.com/mattwelke)** commented [May 31, 2023](https://github.com/puppeteer/puppeteer/issues/10285#issuecomment-1571225635)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">Looks like I didn't take that warning that talked about "sandbox" seriously enough.</p><p dir="auto">I was able to search this on the web and ended up getting things to work by changing my Node.js code to launch the browser without the sandbox:</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-c">// Launch the browser</span>
<span class="pl-k">const</span> <span class="pl-s1">browser</span> <span class="pl-c1">=</span> <span class="pl-k">await</span> <span class="pl-s1">puppeteer</span><span class="pl-kos">.</span><span class="pl-en">launch</span><span class="pl-kos">(</span><span class="pl-kos">{</span>
    <span class="pl-c1">headless</span>: <span class="pl-s">'new'</span><span class="pl-kos">,</span>
    <span class="pl-c1">args</span>: <span class="pl-kos">[</span><span class="pl-s">'--no-sandbox'</span><span class="pl-kos">,</span> <span class="pl-s">'--disable-setuid-sandbox'</span><span class="pl-kos">]</span><span class="pl-kos">,</span>
<span class="pl-kos">}</span><span class="pl-kos">)</span><span class="pl-kos">;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="// Launch the browser
const browser = await puppeteer.launch({
    headless: 'new',
    args: ['--no-sandbox', '--disable-setuid-sandbox'],
});" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">Looks like my next steps are to research running as non-root in Docker and what the sandbox mode is all about, and then to decide how to structure my Dockerfile so that things work while still being secure.</p></td></tr></tbody></table>

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 4 cupliz, DerekGray2022, SakhriHoussem, and nnnhansgt reacted with thumbs up emoji 🎉 4 safety97, cupliz, DerekGray2022, and SakhriHoussem reacted with hooray emoji 🚀 3 DerekGray2022, SakhriHoussem, and dhwaj1902 reacted with rocket emoji

All reactions

-   👍 4 reactions
-   🎉 4 reactions
-   🚀 3 reactions

Sorry, something went wrong.

[![@mattwelke](https://avatars.githubusercontent.com/u/7719209?s=40&u=80f02a799323b1472b389b836d95957c93a6d856&v=4)](https://github.com/mattwelke) [mattwelke](https://github.com/mattwelke) closed this as [completed](https://github.com/puppeteer/puppeteer/issues?q=is%3Aissue+is%3Aclosed+archived%3Afalse+reason%3Acompleted) [May 31, 2023](https://github.com/puppeteer/puppeteer/issues/10285#event-9397319944)

[![@safety97](https://avatars.githubusercontent.com/u/1236381?s=80&u=28ad5ca6b206690b25494cdad628c12bd90834bc&v=4)](https://github.com/safety97)

Sorry, something went wrong.

Quote reply

###

**[safety97](https://github.com/safety97)** commented [Jul 28, 2023](https://github.com/puppeteer/puppeteer/issues/10285#issuecomment-1655628694)

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">thank you save my day !</p>
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

😄 1 mattwelke reacted with laugh emoji

All reactions

-   😄 1 reaction

Sorry, something went wrong.

[![@DerekGray2022](https://avatars.githubusercontent.com/u/105393523?s=80&u=36658b01d2a73af71504b08a4b1647e17df25c9f&v=4)](https://github.com/DerekGray2022)

Sorry, something went wrong.

Quote reply

###

**[DerekGray2022](https://github.com/DerekGray2022)** commented [Sep 14, 2023](https://github.com/puppeteer/puppeteer/issues/10285#issuecomment-1719285349)

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">
                    Saved me many days!! Thanks,
                    <a
                        class="user-mention notranslate"
                        data-hovercard-type="user"
                        data-hovercard-url="/users/mattwelke/hovercard"
                        data-octo-click="hovercard-link-click"
                        data-octo-dimensions="link_type:self"
                        href="https://github.com/mattwelke"
                        >@mattwelke</a
                    >!!
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

🎉 1 mattwelke reacted with hooray emoji

All reactions

-   🎉 1 reaction

Sorry, something went wrong.

[![@avvRobertoAlma](https://avatars.githubusercontent.com/u/25185257?s=80&u=feee0427525432a51ead764ce19a59783cb25bd6&v=4)](https://github.com/avvRobertoAlma)

Sorry, something went wrong.

Quote reply

###

**[avvRobertoAlma](https://github.com/avvRobertoAlma)** commented [Jan 15, 2024](https://github.com/puppeteer/puppeteer/issues/10285#issuecomment-1892846711)

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
    <tbody class="d-block">
        <tr class="d-block">
            <td class="d-block comment-body markdown-body  js-comment-body">
                <p dir="auto">
                    <a
                        class="user-mention notranslate"
                        data-hovercard-type="user"
                        data-hovercard-url="/users/mattwelke/hovercard"
                        data-octo-click="hovercard-link-click"
                        data-octo-dimensions="link_type:self"
                        href="https://github.com/mattwelke"
                        >@mattwelke</a
                    >
                    could you please publish your working dockerfile?
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

[![@mattwelke](https://avatars.githubusercontent.com/u/7719209?s=80&u=80f02a799323b1472b389b836d95957c93a6d856&v=4)](https://github.com/mattwelke)

Sorry, something went wrong.

Quote reply

Contributor Author

###

**[mattwelke](https://github.com/mattwelke)** commented [Jan 15, 2024](https://github.com/puppeteer/puppeteer/issues/10285#issuecomment-1892854517) •

edited

```html
<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto"><a class="user-mention notranslate" data-hovercard-type="user" data-hovercard-url="/users/avvRobertoAlma/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="https://github.com/avvRobertoAlma">@avvRobertoAlma</a> I don't remember which Dockerfile I ended up using for this but I do remember that things started to work when I fixed my Node.js code. It was my program code that was the problem, not the Dockerfile, because <a href="https://github.com/puppeteer/puppeteer/issues/10285#issuecomment-1571225635" data-hovercard-type="issue" data-hovercard-url="/puppeteer/puppeteer/issues/10285/hovercard">I was launching Puppeteer in a way that wasn't compatible with the Debian image</a>.</p><p dir="auto">Try this:</p><div class="highlight highlight-source-dockerfile notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">FROM</span> node:18-buster

<span class="pl-k">WORKDIR</span> /usr/src/app

<span class="pl-k">COPY</span> package\*.json ./

<span class="pl-k">RUN</span> npm install

<span class="pl-k">COPY</span> . .

<span class="pl-k">CMD</span> [ <span class="pl-s">"node"</span>, <span class="pl-s">"index.mjs"</span> ]</pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="FROM node:18-buster
```

```bash
WORKDIR /usr/src/app

COPY package\*.json ./

RUN npm install

COPY . .
```

```html
CMD [ &quot;node&quot;, &quot;index.mjs&quot; ]" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">And if your Node.js code launches Puppeteer correctly, it should work, like it did for me. Then, you'll probably want to double check that <code class="notranslate">18-buster</code> is still the best version of the <code class="notranslate">node</code> image to use for this. It might not be by now.</p></td></tr></tbody></table>
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀
