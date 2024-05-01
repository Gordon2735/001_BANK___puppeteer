# how to check if selector exists or is present ? #1149

Closed

[fran0254](https://github.com/fran0254) opened this issue Oct 24, 2017 · 28 comments

Closed

# [how to check if selector exists or is present ?](https://github.com/puppeteer/puppeteer/issues/1149#top) #1149

[fran0254](https://github.com/fran0254) opened this issue Oct 24, 2017 · 28 comments

## Comments

[![@fran0254](https://avatars.githubusercontent.com/u/32681199?s=80&v=4)](https://github.com/fran0254)

Sorry, something went wrong.

Quote reply

###

**[fran0254](https://github.com/fran0254)** commented [Oct 24, 2017](https://github.com/puppeteer/puppeteer/issues/1149#issue-268021879)

how to check if selector exists or is present waiting for (x) time or when the page is fully loaded ? with this code it does not work for me.

```typescript
if (await page.$eval('selector', { timeout: 3000 })) {
	console.log('found');
} else {
	console.log('no found');
}
```

The text was updated successfully, but these errors were encountered:</p><ol class="mb-0 pl-4 ml-4"></ol></div></td></tr></tbody></table>

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 3 alexander-elgin, gaelmbs, and ShantanuLamba reacted with thumbs up emoji

All reactions

-   👍 3 reactions

[![@vsemozhetbyt](https://avatars.githubusercontent.com/u/10393198?s=80&u=c5e420d0445e0d0fafd27913c0cce29d8def9539&v=4)](https://github.com/vsemozhetbyt)

Sorry, something went wrong.

Quote reply

Contributor

###

**[vsemozhetbyt](https://github.com/vsemozhetbyt)** commented [Oct 24, 2017](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-339020744)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">As a variant:</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">if</span> <span class="pl-kos">(</span><span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">$</span><span class="pl-kos">(</span><span class="pl-s1">selector</span><span class="pl-kos">)</span> <span class="pl-c1">!==</span> <span class="pl-c1">null</span><span class="pl-kos">)</span> <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">'found'</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
<span class="pl-k">else</span> <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">'not found'</span><span class="pl-kos">)</span><span class="pl-kos">;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="if (await page.$(selector) !== null) console.log('found');
else console.log('not found');" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div></td></tr></tbody></table>

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 202 aslushnikov, cliang57, kader-hlby, ramidecodes, rustemkzk, mseltene, sajibcse68, conradoqg, temitope, oscarnevarezleal, and 192 more reacted with thumbs up emoji 👎 6 BenjaminBrodwolf, Maintrust, Speedphoenix, webdevbyjoss, typescriptlover, and pipebits reacted with thumbs down emoji 😄 3 orassayag, truongleeuet, and Eduard-Faus reacted with laugh emoji 🎉 17 rotimi-best, jaggedsoft, Refath, arthurbh, Yokii908, sainu, ashco, vikas304, clouedoc, Fusseldieb, and 7 more reacted with hooray emoji ❤️ 33 lightofhell, jaggedsoft, jukefr, azmatrana, Refath, gentios, dinkydani, arthurbh, Yokii908, zxl634, and 23 more reacted with heart emoji 🚀 20 UdeeshaInduwara, sainu, TAnas0, OliverGrayDG, Fusseldieb, TheArmagan, eugenepolschikov, webdevbyjoss, aalvarezv, b3nThomas, and 10 more reacted with rocket emoji

All reactions

-   👍 202 reactions
-   👎 6 reactions
-   😄 3 reactions
-   🎉 17 reactions
-   ❤️ 33 reactions
-   🚀 20 reactions

Sorry, something went wrong.

[![@aslushnikov](https://avatars.githubusercontent.com/u/746130?s=40&u=bc83ba749f90def9710c03f1502595f1c3af49a9&v=4)](https://github.com/aslushnikov) [aslushnikov](https://github.com/aslushnikov) closed this as [completed](https://github.com/puppeteer/puppeteer/issues?q=is%3Aissue+is%3Aclosed+archived%3Afalse+reason%3Acompleted) [Oct 24, 2017](https://github.com/puppeteer/puppeteer/issues/1149#event-1308644165)

[![@apollo17march](https://avatars.githubusercontent.com/u/1325453?s=80&u=bf8eb73e5fc0b8f27406f31bcf1b48e0ab1a70f5&v=4)](https://github.com/apollo17march)

Sorry, something went wrong.

Quote reply

###

**[apollo17march](https://github.com/apollo17march)** commented [Mar 15, 2018](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-373308781)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto"><a class="user-mention notranslate" data-hovercard-type="user" data-hovercard-url="/users/vsemozhetbyt/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="https://github.com/vsemozhetbyt">@vsemozhetbyt</a> not working for me</p></td></tr></tbody></table>

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

[![@vsemozhetbyt](https://avatars.githubusercontent.com/u/10393198?s=80&u=c5e420d0445e0d0fafd27913c0cce29d8def9539&v=4)](https://github.com/vsemozhetbyt)

Sorry, something went wrong.

Quote reply

Contributor

###

**[vsemozhetbyt](https://github.com/vsemozhetbyt)** commented [Mar 15, 2018](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-373339318)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto"><a class="user-mention notranslate" data-hovercard-type="user" data-hovercard-url="/users/apollo17march/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="https://github.com/apollo17march">@apollo17march</a> Can you provide a small code example where it does not work?</p></td></tr></tbody></table>

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

[![@ratkorle](https://avatars.githubusercontent.com/u/33107251?s=80&u=9b7d2967c5dce994f1afc87b9b3aeb7026036e58&v=4)](https://github.com/ratkorle)

Sorry, something went wrong.

Quote reply

###

**[ratkorle](https://github.com/ratkorle)** commented [Sep 26, 2018](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-424677043)

This works for me :

```typescript
for (let o = 0; o &lt; otherSelectorsPath.length; o++) { let otherSelectorText; let otherSelector = otherSelectorsPath[o]; if (!(await page.$(otherSelector)) || (await page.$(otherSelector) === false) || (await page.$(otherSelector) === undefined) || (await page.$(otherSelector) === null) || (await page.$(otherSelector).length === 0)) { //check if selector exist on the page otherSelectorText = ''; 

} else { 
    otherSelectorText = await page.$eval(otherSelector, text =&gt; text.innerText); 
    } resultObject.push(otherSelectorText); 
    }
```

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👎 80 bonzinho, louremedi, MatteoGioioso, fededirocco34, acravenho, AlonsoK28, NikolaiT, ben-shepherd, michaelhgchen, sburtenshawIR, and 70 more reacted with thumbs down emoji 😄 40 ben-shepherd, Ovski4, younes0, stoplion, ykumar21, kissu, mkantautas, jbeacher6, Smolyan91, the-unbearable-lightness-of-being, and 30 more reacted with laugh emoji 😕 17 Smolyan91, coch110149, matej2, abhidp, AbetangJoseph, nickdotht, BornaSadeghi, ssamnani, arismelachroinos, Melvynx, and 7 more reacted with confused emoji 👀 5 uraden, ADCDS, Prasanth-BS, dieguezz, and Inkvatordor reacted with eyes emoji

All reactions

-   👎 80 reactions
-   😄 40 reactions
-   😕 17 reactions
-   👀 5 reactions

Sorry, something went wrong.

[![@kantuni](https://avatars.githubusercontent.com/u/6151409?s=80&u=fc3fa97b5570b46ccb79030e58ca22b8ea7fc684&v=4)](https://github.com/kantuni)

Sorry, something went wrong.

Quote reply

###

**[kantuni](https://github.com/kantuni)** commented [Oct 6, 2018](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-427546136) •

edited

If you are not certain that a DOM element will appear:
</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">try</span>

```typescript
await  waitForSelector selector// ...catch error
console.log("The element didn't appear.")

try {
  await page.waitForSelector(selector)
  // ...
} catch (error) {
  console.log("The element didn't appear")
} 
```


-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 54 bonzinho, reinaldoacosta, stoplion, seyfer, Smolyan91, Nattasak, DynamicLearningIO, Andraide, Mitigy, shamera82, and 44 more reacted with thumbs up emoji 🎉 12 0791msolomon, louistb, kyler-hyuna, Dima1022, Beenyaa, webdevbyjoss, ctnels, Qoraiche, EwertonDutra, merianos, and 2 more reacted with hooray emoji ❤️ 7 azazrehman, Qoraiche, EwertonDutra, SkelosJS, merianos, Prasanth-BS, and Creative-Difficulty reacted with heart emoji

All reactions

-   👍 54 reactions
-   🎉 12 reactions
-   ❤️ 7 reactions

Sorry, something went wrong.

[![@ivanjeremic](https://avatars.githubusercontent.com/u/13917696?s=80&u=1d188eb9d1fca33a31b98bd48074a88ad27ce795&v=4)](https://github.com/ivanjeremic)

Sorry, something went wrong.

Quote reply

###

**[ivanjeremic](https://github.com/ivanjeremic)** commented [Oct 30, 2018](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-434264401)

If you are not certain that a DOM element will appear:

```typescript
try {
  await page.waitForSelector(selector)
 // ...
} catch   (  error )   { 
   console.log("The element didn't appear.")
}try {
  await page.waitForSelector(selector)
  // ...
} catch (error) {
  console.log("The element didn't appear")
}
```
Thank you kantuni, this is perfect and not a 50 Line code like someone did here....you are a good coder!


[![@kantuni](https://avatars.githubusercontent.com/u/6151409?s=80&u=fc3fa97b5570b46ccb79030e58ca22b8ea7fc684&v=4)](https://github.com/kantuni)

Sorry, something went wrong.

Quote reply

###

**[kantuni](https://github.com/kantuni)** commented [Oct 30, 2018](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-434302298) •

edited

Thank you kantuni, this is perfect and not a 50 Line code like someone did here....you are a good coder!
My pleasure! P.S. You can also pass an optional timeout to the 
`waitForSelector` function. The default timeout is 30 seconds, which is a lot (especially for scrapers).

```typescript
try { 
 await page.waitForSelector(selector, { timeout:  5000 } ) 
   // ...</span>
 } catch ( error ) {
  console.log("The element didn't appear.")
}
try {
  await page.waitForSelector(selector, { timeout: 5000 })
  // ...
} catch (error) {
  console.log("The element didn't ")
}
```

**[L-Jovi](https://github.com/L-Jovi)** commented [Jan 17, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-455022385)

Is  `await page.waitForSelector` better than `await page.$(selector)`?


**[vsemozhetbyt](https://github.com/vsemozhetbyt)** commented [Jan 17, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-455073491)
L-Jovi

```typescript
page.waitForSelector()

// will wait for element till it appears or till timeout exceeds. 
page.$(selector)
 // will return the result immediately without waiting. If you sure that the element should already be on the page, you can use 
page.$(selector)
 check, otherwise 
 
page.waitForSelector()
// is safer.
```


<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto"><a class="user-mention notranslate" data-hovercard-type="user" data-hovercard-url="/users/vsemozhetbyt/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="https://github.com/vsemozhetbyt">@vsemozhetbyt</a> Thanks for explanation :)</p></td></tr></tbody></table>

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 3 vsemozhetbyt, gregoire78, and czerian reacted with thumbs up emoji

All reactions

-   👍 3 reactions

Sorry, something went wrong.

[![@shoroqAltamimi](https://avatars.githubusercontent.com/u/34303167?s=80&v=4)](https://github.com/shoroqAltamimi)

Sorry, something went wrong.

Quote reply

###

**[shoroqAltamimi](https://github.com/shoroqAltamimi)** commented [Nov 15, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-554446239)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto"><a class="user-mention notranslate" data-hovercard-type="user" data-hovercard-url="/users/vsemozhetbyt/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="https://github.com/vsemozhetbyt">@vsemozhetbyt</a> how to ensure I'm successfully logged in , by ensure some element is present or return element is not present if it failed to log in ??</p></td></tr></tbody></table>

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

[![@vsemozhetbyt](https://avatars.githubusercontent.com/u/10393198?s=80&u=c5e420d0445e0d0fafd27913c0cce29d8def9539&v=4)](https://github.com/vsemozhetbyt)

Sorry, something went wrong.

Quote reply

Contributor

###

**[vsemozhetbyt](https://github.com/vsemozhetbyt)** commented [Nov 15, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-554450000)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">It seems the way is the same: use <code class="notranslate">page.waitForSelector()</code> to wait for the element, timeout means failed log-in.</p></td></tr></tbody></table>

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

[![@shoroqAltamimi](https://avatars.githubusercontent.com/u/34303167?s=80&v=4)](https://github.com/shoroqAltamimi)

Sorry, something went wrong.

Quote reply

###

**[shoroqAltamimi](https://github.com/shoroqAltamimi)** commented [Nov 15, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-554516848) •

edited

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto"><a class="user-mention notranslate" data-hovercard-type="user" data-hovercard-url="/users/vsemozhetbyt/hovercard" data-octo-click="hovercard-link-click" data-octo-dimensions="link_type:self" href="https://github.com/vsemozhetbyt">@vsemozhetbyt</a> but it doesn't work with me :(</p><p dir="auto">there is my script</p><div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code class="notranslate"> if (await page.waitForSelector('[data-ghost="Click-MyAccount"]')) {
       console.log("found")
    } else console.log("not found");
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value=" if (await page.waitForSelector('[data-ghost=&quot;Click-MyAccount&quot;]')) {
       console.log(&quot;found&quot;)
    } else console.log(&quot;not found&quot;);" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div><p dir="auto">I need to focus the element in the page and return the element is not present if the login failed</p></td></tr></tbody></table>

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

[![@vsemozhetbyt](https://avatars.githubusercontent.com/u/10393198?s=80&u=c5e420d0445e0d0fafd27913c0cce29d8def9539&v=4)](https://github.com/vsemozhetbyt)

Sorry, something went wrong.

Quote reply

Contributor

###

**[vsemozhetbyt](https://github.com/vsemozhetbyt)** commented [Nov 16, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-554620377)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">Try this:</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate">  <span class="pl-k">try</span> <span class="pl-kos">{</span>
    <span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">waitForSelector</span><span class="pl-kos">(</span><span class="pl-s">'img'</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
    <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">'found'</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
  <span class="pl-kos">}</span> <span class="pl-k">catch</span> <span class="pl-kos">{</span>
    <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">'not found'</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
  <span class="pl-kos">}</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="  try {
    await page.waitForSelector('img');
    console.log('found');
  } catch {
    console.log('not found');
  }" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div></td></tr></tbody></table>

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

[![@shoroqAltamimi](https://avatars.githubusercontent.com/u/34303167?s=80&v=4)](https://github.com/shoroqAltamimi)

Sorry, something went wrong.

Quote reply

###

**[shoroqAltamimi](https://github.com/shoroqAltamimi)** commented [Nov 16, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-554623291) via email

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body email-format js-comment-body"><div class="email-fragment">I'm trying it but nothing happens</div><span class="email-hidden-toggle"><a href="https://github.com/puppeteer/puppeteer/issues/1149#">…</a></span><div class="email-hidden-reply"><div class="email-quoted-reply">On Sat, Nov 16, 2019 at 11:26 AM Vse Mozhet Byt ***@***.***&gt; wrote: Try this: try { await page.waitForSelector('img'); console.log('found'); } catch { console.log('not found'); } — You are receiving this because you commented. Reply to this email directly, view it on GitHub &lt;<a class="issue-link js-issue-link" data-error-text="Failed to load title" data-id="268021879" data-permission-text="Title is private" data-url="https://github.com/puppeteer/puppeteer/issues/1149" href="https://github.com/puppeteer/puppeteer/issues/1149">#1149</a>&gt;, or unsubscribe &lt;<a href="https://github.com/notifications/unsubscribe-auth/AIFWZP5UPMVJK6OMVTDZTRLQT64EXANCNFSM4EARQSFQ">https://github.com/notifications/unsubscribe-auth/AIFWZP5UPMVJK6OMVTDZTRLQT64EXANCNFSM4EARQSFQ</a>&gt; .</div><div class="email-fragment"></div></div></td></tr></tbody></table>

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

[![@vsemozhetbyt](https://avatars.githubusercontent.com/u/10393198?s=80&u=c5e420d0445e0d0fafd27913c0cce29d8def9539&v=4)](https://github.com/vsemozhetbyt)

Sorry, something went wrong.

Quote reply

Contributor

###

**[vsemozhetbyt](https://github.com/vsemozhetbyt)** commented [Nov 16, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-554624083)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">Do you wait for the default timeout (30 sec)?</p></td></tr></tbody></table>

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

[![@shoroqAltamimi](https://avatars.githubusercontent.com/u/34303167?s=80&v=4)](https://github.com/shoroqAltamimi)

Sorry, something went wrong.

Quote reply

###

**[shoroqAltamimi](https://github.com/shoroqAltamimi)** commented [Nov 16, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-554625272) •

edited

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">ya, but I want to focus the div element when it exists<br>how I can do it<br>I'm trying page.focus(selector) it doesn't work</p></td></tr></tbody></table>

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

[![@vsemozhetbyt](https://avatars.githubusercontent.com/u/10393198?s=80&u=c5e420d0445e0d0fafd27913c0cce29d8def9539&v=4)](https://github.com/vsemozhetbyt)

Sorry, something went wrong.

Quote reply

Contributor

###

**[vsemozhetbyt](https://github.com/vsemozhetbyt)** commented [Nov 16, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-554625655)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">Maybe if you provide a small but complete script example, somebody will be able to help.</p></td></tr></tbody></table>

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

[![@namename-123](https://avatars.githubusercontent.com/u/46111311?s=80&u=e299d6ad0f9eee4f5e2c22888796b9dea14ddcc8&v=4)](https://github.com/namename-123)

Sorry, something went wrong.

Quote reply

###

**[namename-123](https://github.com/namename-123)** commented [Dec 11, 2019](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-564747564)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">Hello, is it possible to use this on Recaptcha?<br>To wait for it to load.</p></td></tr></tbody></table>

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

[![@alidanial7](https://avatars.githubusercontent.com/u/30351558?s=80&v=4)](https://github.com/alidanial7)

Sorry, something went wrong.

Quote reply

###

**[alidanial7](https://github.com/alidanial7)** commented [Jan 13, 2020](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-573568874)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto"><code class="notranslate">test('should have element', async () =&gt; { const page = await browser.newPage() await page.goto('http://localhost:3000/') await expect(page.$('#id') !== null) }, 100000)</code></p></td></tr></tbody></table>

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

[![@lewyuburi](https://avatars.githubusercontent.com/u/2156790?s=80&u=815a02481965633c2a11cb167a91845d951be635&v=4)](https://github.com/lewyuburi)

Sorry, something went wrong.

Quote reply

###

**[lewyuburi](https://github.com/lewyuburi)** commented [Jan 31, 2020](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-580844773)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">I use</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">waitForSelector</span><span class="pl-kos">(</span><span class="pl-s">'selector'</span><span class="pl-kos">,</span> <span class="pl-kos">{</span> <span class="pl-c1">timeout</span>: <span class="pl-c1">5000</span> <span class="pl-kos">}</span><span class="pl-kos">)</span>
  <span class="pl-kos">.</span><span class="pl-en">catch</span> <span class="pl-kos">(</span><span class="pl-kos">(</span><span class="pl-s1">error</span><span class="pl-kos">)</span> <span class="pl-c1">=&gt;</span> <span class="pl-kos">{</span>
    <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">"The element didn't appear."</span><span class="pl-kos">)</span>
  <span class="pl-kos">}</span><span class="pl-kos">)</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="await page.waitForSelector('selector', { timeout: 5000 })
  .catch ((error) =&gt; {
    console.log(&quot;The element didn't appear.&quot;)
  })" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div></td></tr></tbody></table>

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 8 sanjay-boricha, jalmoreno, cristoffer-andersson-stratsys, kerematam, khoi01, allcapsc, Globerada, and coalexandr reacted with thumbs up emoji

All reactions

-   👍 8 reactions

Sorry, something went wrong.

[![@NearW](https://avatars.githubusercontent.com/u/12533626?s=40&v=4)](https://github.com/NearW) [NearW](https://github.com/NearW) mentioned this issue [Aug 24, 2020](https://github.com/puppeteer/puppeteer/issues/1149#ref-pullrequest-684452427)

[fix/1161/solve-unclosing-node-options MaibornWolff/codecharta#1169](https://github.com/MaibornWolff/codecharta/pull/1169)

Merged

[![@UviFarchi](https://avatars.githubusercontent.com/u/24434367?s=80&v=4)](https://github.com/UviFarchi)

Sorry, something went wrong.

Quote reply

###

**[UviFarchi](https://github.com/UviFarchi)** commented [Sep 28, 2020](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-700146812)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><blockquote><blockquote><p dir="auto">Thank you kantuni, this is perfect and not a 50 Line code like someone did here....you are a good coder!</p></blockquote><p dir="auto">My pleasure!</p><p dir="auto">P.S. You can also pass an optional timeout to the <code class="notranslate">waitForSelector</code> function. The default timeout is 30 seconds, which is a lot (especially for scrapers).</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">try</span> <span class="pl-kos">{</span>
  <span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">waitForSelector</span><span class="pl-kos">(</span><span class="pl-s1">selector</span><span class="pl-kos">,</span> <span class="pl-kos">{</span> <span class="pl-c1">timeout</span>: <span class="pl-c1">5000</span> <span class="pl-kos">}</span><span class="pl-kos">)</span>
  <span class="pl-c">// ...</span>
<span class="pl-kos">}</span> <span class="pl-k">catch</span> <span class="pl-kos">(</span><span class="pl-s1">error</span><span class="pl-kos">)</span> <span class="pl-kos">{</span>
  <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">"The element didn't appear."</span><span class="pl-kos">)</span>
<span class="pl-kos">}</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="try {
  await page.waitForSelector(selector, { timeout: 5000 })
  // ...
} catch (error) {
  console.log(&quot;The element didn't appear.&quot;)
}" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div></blockquote><p dir="auto">It works, but in general terms you shouldn't use exception handling for flow control. I would have thought someone who's katnuni would be a stickler for the forms.</p></td></tr></tbody></table>

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

[![@chanakaDe](https://avatars.githubusercontent.com/u/7803591?s=80&u=a13bf3b121527b166029a887fbd639a33ad1c1f6&v=4)](https://github.com/chanakaDe)

Sorry, something went wrong.

Quote reply

###

**[chanakaDe](https://github.com/chanakaDe)** commented [Jan 11, 2021](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-757864050)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><blockquote><p dir="auto">If you are not certain that a DOM element will appear:</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">try</span> <span class="pl-kos">{</span>
  <span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">waitForSelector</span><span class="pl-kos">(</span><span class="pl-s1">selector</span><span class="pl-kos">)</span>
  <span class="pl-c">// ...</span>
<span class="pl-kos">}</span> <span class="pl-k">catch</span> <span class="pl-kos">(</span><span class="pl-s1">error</span><span class="pl-kos">)</span> <span class="pl-kos">{</span>
  <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">"The element didn't appear."</span><span class="pl-kos">)</span>
<span class="pl-kos">}</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="try {
  await page.waitForSelector(selector)
  // ...
} catch (error) {
  console.log(&quot;The element didn't appear.&quot;)
}" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div></blockquote><p dir="auto">This saved my day. Simple and quick solution. Thanks man. Much love</p></td></tr></tbody></table>

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

[![@jhsuP](https://avatars.githubusercontent.com/u/56209781?s=40&v=4)](https://github.com/jhsuP) [jhsuP](https://github.com/jhsuP) mentioned this issue [Jan 18, 2021](https://github.com/puppeteer/puppeteer/issues/1149#ref-issue-787536882)

[Review: Scrapers internaloha/internaloha#100](https://github.com/internaloha/internaloha/issues/100)

Closed

[![@northmatt](https://avatars.githubusercontent.com/u/33724702?s=80&v=4)](https://github.com/northmatt)

Sorry, something went wrong.

Quote reply

###

**[northmatt](https://github.com/northmatt)** commented [Feb 19, 2021](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-782232360)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><blockquote><p dir="auto">If you are not certain that a DOM element will appear:</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">try</span> <span class="pl-kos">{</span>
  <span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">waitForSelector</span><span class="pl-kos">(</span><span class="pl-s1">selector</span><span class="pl-kos">)</span>
  <span class="pl-c">// ...</span>
<span class="pl-kos">}</span> <span class="pl-k">catch</span> <span class="pl-kos">(</span><span class="pl-s1">error</span><span class="pl-kos">)</span> <span class="pl-kos">{</span>
  <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">"The element didn't appear."</span><span class="pl-kos">)</span>
<span class="pl-kos">}</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="try {
  await page.waitForSelector(selector)
  // ...
} catch (error) {
  console.log(&quot;The element didn't appear.&quot;)
}" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div></blockquote><p dir="auto">That causes a memory leak for me on failed attempts. Basically am constantly checking for a DOM element that will almost never appear over the course of some hours, so a lot of failed attempts will happen. So idk if that is an ideal solution.</p></td></tr></tbody></table>

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 3 arthurborgesdev, agocharbhatia, and AHHusam reacted with thumbs up emoji

All reactions

-   👍 3 reactions

Sorry, something went wrong.

[![@DvDream](https://avatars.githubusercontent.com/u/45291289?s=80&v=4)](https://github.com/DvDream)

Sorry, something went wrong.

Quote reply

###

**[DvDream](https://github.com/DvDream)** commented [Sep 20, 2021](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-922778130) •

edited

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><blockquote><p dir="auto">If you are not certain that a DOM element will appear:</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">try</span> <span class="pl-kos">{</span>
  <span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">waitForSelector</span><span class="pl-kos">(</span><span class="pl-s1">selector</span><span class="pl-kos">)</span>
  <span class="pl-c">// ...</span>
<span class="pl-kos">}</span> <span class="pl-k">catch</span> <span class="pl-kos">(</span><span class="pl-s1">error</span><span class="pl-kos">)</span> <span class="pl-kos">{</span>
  <span class="pl-smi">console</span><span class="pl-kos">.</span><span class="pl-en">log</span><span class="pl-kos">(</span><span class="pl-s">"The element didn't appear."</span><span class="pl-kos">)</span>
<span class="pl-kos">}</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="try {
  await page.waitForSelector(selector)
  // ...
} catch (error) {
  console.log(&quot;The element didn't appear.&quot;)
}" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div></blockquote><p dir="auto">What if I expect that the selector won't appear and instead is appearing once my page has loaded? How could I make the test failing with that? thanks :)</p></td></tr></tbody></table>

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

[![@vsemozhetbyt](https://avatars.githubusercontent.com/u/10393198?s=80&u=c5e420d0445e0d0fafd27913c0cce29d8def9539&v=4)](https://github.com/vsemozhetbyt)

Sorry, something went wrong.

Quote reply

Contributor

###

**[vsemozhetbyt](https://github.com/vsemozhetbyt)** commented [Sep 20, 2021](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-923115330)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">Maybe this:</p><div class="highlight highlight-source-js notranslate position-relative overflow-auto" dir="auto"><pre class="notranslate"><span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">waitForTimeout</span><span class="pl-kos">(</span><span class="pl-s1">someTime</span><span class="pl-kos">)</span><span class="pl-kos">;</span>
<span class="pl-k">if</span> <span class="pl-kos">(</span><span class="pl-k">await</span> <span class="pl-s1">page</span><span class="pl-kos">.</span><span class="pl-en">$</span><span class="pl-kos">(</span><span class="pl-s1">selector</span><span class="pl-kos">)</span><span class="pl-kos">)</span> <span class="pl-k">throw</span> <span class="pl-k">new</span> <span class="pl-v">Error</span><span class="pl-kos">(</span><span class="pl-s">'Unexpected element.'</span><span class="pl-kos">)</span><span class="pl-kos">;</span></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="await page.waitForTimeout(someTime);
if (await page.$(selector)) throw new Error('Unexpected element.');" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div></td></tr></tbody></table>

-   👍
-   👎
-   😄
-   🎉
-   😕
-   ❤️
-   🚀
-   👀

👍 2 Zicio and Arthur-Diesel reacted with thumbs up emoji

All reactions

-   👍 2 reactions

Sorry, something went wrong.

[![@mykhailo-kobylianskyi](https://avatars.githubusercontent.com/u/16340722?s=80&u=b8d802c0c5b4b9f3deb7feea73072e2f45d78e8e&v=4)](https://github.com/mykhailo-kobylianskyi)

Sorry, something went wrong.

Quote reply

###

**[mykhailo-kobylianskyi](https://github.com/mykhailo-kobylianskyi)** commented [Sep 19, 2022](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-1251582114)

<table class="d-block user-select-contain" data-paste-markdown-skip=""><tbody class="d-block"><tr class="d-block"><td class="d-block comment-body markdown-body  js-comment-body"><p dir="auto">this method will return true if element exist, and false if element not exist of locator is invalid</p><div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code class="notranslate">async isSelectorExists(selector: string) {
  return await this._page.$(selector).catch(() =&gt; null) !== null;
}
</code></pre><div class="zeroclipboard-container position-absolute right-0 top-0"><clipboard-copy aria-label="Copy" class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay" data-copy-feedback="Copied!" data-tooltip-direction="w" value="async isSelectorExists(selector: string) {
  return await this._page.$(selector).catch(() =&gt; null) !== null;
}" tabindex="0" role="button"><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon m-2"><path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2"><path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg></clipboard-copy></div></div></td></tr></tbody></table>

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

[![@CactusWren2020](https://avatars.githubusercontent.com/u/63522908?s=80&u=a51c822def13477faf49d6451c8c9d02cea9fcb2&v=4)](https://github.com/CactusWren2020)

Sorry, something went wrong.

Quote reply

###

**[CactusWren2020](https://github.com/CactusWren2020)** commented [Oct 7, 2022](https://github.com/puppeteer/puppeteer/issues/1149#issuecomment-1271868819)

```html
<table class="d-block user-select-contain" data-paste-markdown-skip="">
	<tbody class="d-block">
		<tr class="d-block">
			<td class="d-block comment-body markdown-body  js-comment-body">
				<blockquote>
					<p dir="auto">
						this method will return true if element exist, and false
						if element not exist of locator is invalid
					</p>
					<div
						class="snippet-clipboard-content notranslate position-relative overflow-auto">
						<pre
							class="notranslate"><code class="notranslate">async isSelectorExists(selector: string) {
  return await this._page.$(selector).catch(() =&gt; null) !== null;
}
</code></pre>
						<div
							class="zeroclipboard-container position-absolute right-0 top-0">
							<clipboard-copy
								aria-label="Copy"
								class="ClipboardButton btn js-clipboard-copy m-2 p-0 tooltipped-no-delay"
								data-copy-feedback="Copied!"
								data-tooltip-direction="w"
								value="async isSelectorExists(selector: string) {
  return await this._page.$(selector).catch(() =&gt; null) !== null;
}"
								tabindex="0"
								role="button"
								><svg
									aria-hidden="true"
									height="16"
									viewBox="0 0 16 16"
									version="1.1"
									width="16"
									data-view-component="true"
									class="octicon octicon-copy js-clipboard-copy-icon m-2">
									<path
										d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path>
									<path
										d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path></svg
								><svg
									aria-hidden="true"
									height="16"
									viewBox="0 0 16 16"
									version="1.1"
									width="16"
									data-view-component="true"
									class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none m-2">
									<path
										d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path></svg
							></clipboard-copy>
						</div>
					</div>
				</blockquote>
				<p dir="auto">
					Would it be possible to show more context? My program
					crashes when I try to implement this.
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

[![@Gordon2735](https://avatars.githubusercontent.com/u/81874061?s=80&v=4)](https://github.com/Gordon2735)

#### Add a comment
