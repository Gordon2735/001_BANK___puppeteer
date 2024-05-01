# The Best Font Loading Strategies and How to Execute Them

[![Avatar of Zell Liew](https://secure.gravatar.com/avatar/00eedd7282eab774e300918f9e32558b?s=80&d=retro&r=pg)](https://css-tricks.com/author/zellwk/)

[Zell Liew](https://css-tricks.com/author/zellwk/) on Mar 2, 2021

Zach Leatherman wrote up a [comprehensive list of font loading strategies](https://www.zachleat.com/web/comprehensive-webfonts/) that have been widely shared in the web development field. I took a look at this list before, but got so scared (and confused), that I decided _not_ to do anything at all. I don’t know how to begin loading fonts the best way and I don’t want to feel like an idiot going through this list.

Today, I gave myself time to [sit down and figure it out](https://zellwk.com/blog/figure-it-out/). In this article, I want to share with you the best loading strategies and how to execute all of them.

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-the-best-strategies)The best strategies

Zach recommends two strategies in his article:

1. **FOUT with Class** – Best approach for most situations. (This works whether we use a font-hosting company or hosting our own fonts.)
2. **Critical FOFT** – Most performant approach. (This only works if we host our own fonts.)

Before we dive into these two strategies, we need to clear up the acronyms so you understand what Zach is saying.

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-foit-fout-foft)FOIT, FOUT, FOFT

The acronyms are as follows:

-   **FOIT** means **flash of invisible text**. When web fonts are loading, we hide text so users don’t see anything. We only show the text when web fonts are loaded.
-   **FOUT** means **flash of unstyled text**. When web fonts are loading, we show users a system font. When the web font gets loaded, we change the text back to the desired web font.
-   **FOFT** means **flash of faux text**. This one is complicated and warrants more explanation. We’ll talk about it in detail when we hit the FOFT section.

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-self-hosted-fonts-vs-cloud-hosted-fonts)Self-hosted fonts vs. cloud-hosted fonts

There are two main ways to host fonts:

1. Use a cloud provider.
2. Self-host the fonts.

How we load fonts differs greatly depending on which option you choose.

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-loading-fonts-with-cloud-hosted-fonts)Loading fonts with cloud-hosted fonts

It’s often easier to cloud-hosted fonts. The provider will give us a link to load the fonts. We can simply plunk this link into our HTML and we’ll get our web font. Here’s an example where we load web fonts from Adobe Fonts now (previously known as Typekit).

```html
<link rel="stylesheet" href="https://use.typekit.net/your-kit-id.css" />
```

Unfortunately, this isn’t the best approach. The `href` blocks the browser. If loading the web font hangs, users won’t be able to do anything while they wait.

Typekit used to provide JavaScript that loads a font asynchronously. It’s a pity they don’t show this JavaScript version anymore. (The code still works though, but I have no idea when, or if, it will stop working.)

Loading fonts from Google Fonts is _slightly_ better because it provides `font-display: swap`. Here’s an example where we load Lato from Google Fonts. (The `display=swap` parameter triggers `font-display: swap`).

```html
<link
	href="https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;1,400;1,700&display=swap"
	rel="stylesheet" />
```

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-loading-fonts-with-self-hosted-fonts)Loading fonts with self-hosted fonts

**You can only self-host your fonts if you have the license to do so**. Since fonts can be expensive, most people choose to use a cloud provider instead.

There’s a cheap way to get fonts though. [Design Cuts](https://www.designcuts.com/?ref=zellliew) runs font deals occasionally where you can get insanely high-quality fonts for just $29 per bundle. Each bundle can contain up to 12 fonts. I managed to get classics like Claredon, DIN, Futura, and a whole slew of fonts I can play around by camping on their newsletter for these deals.

If we want to self-host fonts, we need to understand two more concepts: `@font-face` and `font-display: swap`.

#### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-font-face)`@font-face`

`@font-face` lets us declare fonts in CSS. If we want to self-host fonts, we need to use `@font-face` to declare your fonts.

In this declaration, we can specify four things:

-   `font-family`: This tells CSS (and JavaScript) the name of our font.
-   `src`: Path to find the font so they can get loaded
-   `font-weight`: The font weight. Defaults to 400 if omitted.
-   `font-style`: Whether to italicize the font. Defaults to normal if omitted.

For `src`, we need to specify several font formats. For [a practical level of browser support](https://css-tricks.com/snippets/css/using-font-face/#practical-level-of-browser-support), we can use `woff2` and `woff`.

Here’s an example where we load Lato via `@font-face`.

```css
@font-face {
	font-family: Lato;
	src: url('path-to-lato.woff2') format('woff2'), url('path-to-lato.woff')
			format('woff');
}

@font-face {
	font-family: Lato;
	src: url('path-to-lato-bold.woff2') format('woff2'), url('path-to-lato-bold.woff')
			format('woff');
	font-weight: 700;
}

@font-face {
	font-family: Lato;
	src: url('path-to-lato-italic.woff2') format('woff2'), url('path-to-lato-italic.woff')
			format('woff');
	font-style: italic;
}

@font-face {
	font-family: Lato;
	src: url('path-to-lato-bold-italic.woff2') format('woff2'), url('path-to-lato-bold-italic.woff')
			format('woff');
	font-weight: 700;
	font-style: italic;
}
```

If you don’t have `woff2` or `woff` files, you can upload your font files (either Opentype or Truetype) into a [font-face generator](https://www.fontsquirrel.com/tools/webfont-generator) to get them.

Next, we declare the web font in a `font-family` property.

```css
html {
	font-family: Lato, sans-serif;
}
```

When browsers parse an element with the web font, they trigger a download for the web font.

#### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-font-display-swap)`font-display: swap`

`font-display` takes one of four possible values: `auto`, `swap`, `fallback`, and `optional`. `swap` instructs browsers to display the fallback text before web fonts get loaded. In other words, `swap` triggers FOUT for self-hosted fonts. Find out about other values from [in the CSS-Tricks almanac](https://css-tricks.com/almanac/properties/f/font-display/).

Browser support for `font-display: swap` is pretty good nowadays so we can use it in our projects.

This browser support data is from [Caniuse](http://caniuse.com/#feat=css-font-rendering-controls), which has more detail. A number indicates that browser supports the feature at that version and up.

#### Desktop

| Chrome | Firefox | IE  | Edge | Safari |
| ------ | ------- | --- | ---- | ------ |
| 60     | 58      | No  | 79   | 11.1   |

#### Mobile / Tablet

| Android Chrome | Android Firefox | Android | iOS Safari |
| -------------- | --------------- | ------- | ---------- |
| 123            | 124             | 123     | 11.3-11.4  |

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-fout-vs-fout-with-class)FOUT vs. FOUT with Class

**FOUT** means **flash of unstyled text**. You always want FOUT over FOIT (flash of invisible text) because it’s better for users to read words written with system fonts compared to words written with invisible ink. We mentioned earlier that `font-display: swap` gives you the ability to use FOUT natively.

**FOUT with Class** gives you the same results—FOUT—but it uses JavaScript to load the fonts. The mechanics are as follows:

-   First: Load system fonts.
-   Second: Load web fonts via JavaScript.
-   Third: When web fonts are loaded, add a class to the `<html>` tag.
-   Fourth: Switch the system font with the loaded web font.

Zach recommends loading fonts via JavaScript even though `font-display: swap` enjoys good browser support. In other words, Zach recommends FOUT with Class over `@font-face` + `font-display: swap`.

He recommends FOUT with Class because of these three reasons:

1. We can group repaints.
2. We can adapt to user preferences.
3. We can skip font-loading altogether if users have a slow connection.

I’ll let you dive deeper into the reasons in [another article](https://www.filamentgroup.com/lab/js-web-fonts.html). While writing this article, I found a _fourth_ reason to prefer FOUT with Class: **We can skip font-loading when users already have the font loaded in their system**. (We do this with `sessionStorage` as we’ll see below.)

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-fout-with-class-for-cloud-hosted-fonts)FOUT with Class (for cloud-hosted fonts)

First, we want to load our fonts as usual from your cloud-hosting company. Here’s an example where I loaded Lato from Google Fonts:

```html
<head>
	<link
		href="https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;1,400;1,700&display=swap"
		rel="stylesheet" />
</head>
```

Next, we want to load fonts via JavaScript. We’ll inject a `script` into the `<head>` section since the code footprint is small, and it’s going to be asynchronous anyway.

```html
<head>
	<link
		href="https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;1,400;1,700&display=swap"
		rel="stylesheet" />
	<script src="js/load-fonts.js"></script>
</head>
```

In `load-fonts.js`, we want to use the CSS Font Loading API to load the font. Here, we can use `Promise.all` to load all fonts simultaneously. When we do this, we’re grouping repaints.

The code looks like this:

```javascript
if ('fonts' in document) {
  Promise.all([
    document.fonts.load('1em Lato'),
    document.fonts.load('700 1em Lato'),
    document.fonts.load('italic 1em Lato'),
    document.fonts.load('italic 700 1em Lato')
  ]).then(_ => () {
    document.documentElement.classList.add('fonts-loaded')
  })
}
```

When fonts are loaded, we want to change the body text to the web font. We can do this via CSS by using the `.fonts-loaded` class.

```css
/* System font before [[webfont]]s get loaded */
body {
	font-family: sans-serif;
}

/* Use [[webfont]] when [[webfont]] gets loaded*/
.fonts-loaded body {
	font-family: Lato, sans-serif;
}
```

**Pay attention here:** We need to use the `.fonts-loaded` class with this approach.

We cannot write the web font directly in the `<body>`‘s `font-family`; doing this will trigger fonts to download, which means you’re using `@font-face + font-display: swap`. It also means the JavaScript is redundant.

```css
/* DO NOT DO THIS */
body {
	font-family: Lato, sans-serif;
}
```

If users visit additional pages on the site, they already have the fonts loaded in their browser. We can skip the font-loading process (to speed things up) by using `sessionStorage`.

```javascript
if (sessionStorage.fontsLoaded) {
  document.documentElement.classList.add('fonts-loaded')
} else {
  if ('fonts' in document) {
  Promise.all([
    document.fonts.load('1em Lato'),
    document.fonts.load('700 1em Lato'),
    document.fonts.load('italic 1em Lato'),
    document.fonts.load('italic 700 1em Lato')
  ]).then(_ => () {
    document.documentElement.classList.add('fonts-loaded')
  })
  }
}
```

If we want to optimize the JavaScript for readability, we can use an early return pattern to reduce indentation.

```javascript
function loadFonts () {
  if (sessionStorage.fontsLoaded) {
    document.documentElement.classList.add('fonts-loaded')
    return
  }

if ('fonts' in document) {
  Promise.all([
    document.fonts.load('1em Lato'),
    document.fonts.load('700 1em Lato'),
    document.fonts.load('italic 1em Lato'),
    document.fonts.load('italic 700 1em Lato')
  ]).then(_ => () {
    document.documentElement.classList.add('fonts-loaded')
  })
}

loadFonts()
```

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-fout-with-class-for-self-hosted-fonts)FOUT with Class (for self-hosted fonts)

First, we want to load our fonts as usual via `@font-face`. The `font-display: swap` property is optional since we’re loading fonts via JavaScript.

```css
@font-face {
	font-family: Lato;
	src: url('path-to-lato.woff2') format('woff2'), url('path-to-lato.woff')
			format('woff');
}

/* Other @font-face declarations */
```

Next, we load the web fonts via JavaScript.

```javascript
if ('fonts' in document) {
  Promise.all([
    document.fonts.load('1em Lato'),
    document.fonts.load('700 1em Lato'),
    document.fonts.load('italic 1em Lato'),
    document.fonts.load('italic 700 1em Lato')
  ]).then(_ => () {
    document.documentElement.classList.add('fonts-loaded')
  })
}
```

Then we want to change the body text to the web font via CSS:

```css
/* System font before webfont is loaded */
body {
	font-family: sans-serif;
}

/* Use webfont when it loads */
.fonts-loaded body {
	font-family: Lato, sans-serif;
}
```

Finally, we skip font loading for repeat visits.

```javascript
if ('fonts' in document) {
  Promise.all([
    document.fonts.load('1em Lato'),
    document.fonts.load('700 1em Lato'),
    document.fonts.load('italic 1em Lato'),
    document.fonts.load('italic 700 1em Lato')
  ]).then(_ => () {
    document.documentElement.classList.add('fonts-loaded')
  })
}
```

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-css-font-loader-api-vs-fontfaceobserver)CSS Font Loader API vs. `FontFaceObserver`

The CSS Font Loader API has pretty good browser support, but it’s a pretty cranky API.

This browser support data is from [Caniuse](http://caniuse.com/#feat=font-loading), which has more detail. A number indicates that browser supports the feature at that version and up.

#### Desktop

| Chrome | Firefox | IE  | Edge | Safari |
| ------ | ------- | --- | ---- | ------ |
| 35     | 41      | No  | 79   | 10     |

#### Mobile / Tablet

| Android Chrome | Android Firefox | Android | iOS Safari |
| -------------- | --------------- | ------- | ---------- |
| 123            | 124             | 123     | 10.0-10.2  |

So, if you need to support older browsers (like IE 11 and below), or if you find the API weird and unwieldy, you might want to use Bramstein’s `[FontFaceObserver](https://github.com/bramstein/fontfaceobserver)`. It’s super lightweight so there’s not much harm.

The code looks like this. (It’s _much_ nicer compared to the CSS Font Loader API).

```javascript
new FontFaceObserver('lato').load().then((_) => {
	document.documentElement.classList.add('fonts-loaded');
});
```

Make sure to use `[fontfaceobserver.standalone.js](https://github.com/bramstein/fontfaceobserver/blob/master/fontfaceobserver.standalone.js)` if you intend to it to load fonts on browsers that don’t support Promises.

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-foft)FOFT

**FOFT** means **flash of faux text**. The idea here is we split font loading into three stages:

-   **Step 1: Use fallback font** when web fonts aren’t loaded yet.
-   **Step 2: Load the Roman** (also called “book” or “regular”) **version of the font first**. This replaces most of the text. Bold and italics will be faked by the browser (hence “faux text”).
-   **Step 3: Load the rest of the fonts**

Note: Zach also calls this **Standard FOFT**.

#### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-using-standard-foft)Using Standard FOFT

First, we load the Roman font.

```css
@font-face {
	font-family: LatoInitial;
	src: url('path-to-lato.woff2') format('woff2'), url('path-to-lato.woff')
			format('woff');
	unicode-range: U+65-90, U+97-122;
}

.fonts-loaded-1 body {
	font-family: LatoInitial;
}
```

```javascript
if ('fonts' in document) {
	document.fonts.load('1em LatoInitial').then((_) => {
		document.documentElement.classList.add('fonts-loaded-1');
	});
}
```

Then, we load other fonts.

Pay attention here: we’re loading `Lato` again, but this time, we set `font-family` to `Lato` instead of `LatoInitial`.

```css
/* Load this first */
@font-face {
	font-family: LatoInitial;
	src: url('path-to-lato.woff2') format('woff2'), url('path-to-lato.woff')
			format('woff');
	unicode-range: U+65-90, U+97-122;
}

/* Load these afterwards */
@font-face {
	font-family: Lato;
	src: url('path-to-lato.woff2') format('woff2'), url('path-to-lato.woff')
			format('woff');
	unicode-range: U+65-90, U+97-122;
}

/* Other @font-face for different weights and styles*/

.fonts-loaded-1 body {
	font-family: LatoInitial;
}

.fonts-loaded-2 body {
	font-family: Lato;
}
```

```javascript
if ('fonts' in document) {
	document.fonts.load('1em LatoInitial').then((_) => {
		document.documentElement.classList.add('fonts-loaded-1');

		Promise.all([
			document.fonts.load('400 1em Lato'),
			document.fonts.load('700 1em Lato'),
			document.fonts.load('italic 1em Lato'),
			document.fonts.load('italic 700 1em Lato')
		]).then((_) => {
			document.documentElement.classList.add('fonts-loaded-2');
		});
	});
}
```

Again, we can optimize it for repeat views.

Here, we can add `fonts-loaded-2` to the `<html>` straightaway since fonts are already loaded.

```javascript
function loadFonts() {
	if (sessionStorage.fontsLoaded) {
		document.documentElement.classList.add('fonts-loaded-2');
		return;
	}

	if ('fonts' in document) {
		document.fonts.load('1em Lato').then((_) => {
			document.documentElement.classList.add('fonts-loaded-1');

			Promise.all([
				document.fonts.load('400 1em Lato'),
				document.fonts.load('700 1em Lato'),
				document.fonts.load('italic 1em Lato'),
				document.fonts.load('italic 700 1em Lato')
			]).then((_) => {
				document.documentElement.classList.add('fonts-loaded-2');

				// Optimization for Repeat Views
				sessionStorage.fontsLoaded = true;
			});
		});
	}
}
```

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-critical-foft)Critical FOFT

The “critical” part comes from ‘critical css” (I believe) – where we load only essential CSS before loading the rest. We do this because it improves performance.  
When it comes to typography, the only critical things are letters A to Z (both capitals and small letters). We can create a subset of these fonts with `unicode-range`.

When we create this subset, we can also create a separate font file with the necessary characters.

Here’s what `@font-face` declaration looks like:

```css
@font-face {
	font-family: LatoSubset;
	src: url('path-to-optimized-lato.woff2') format('woff2'), url('path-to-optimized-lato.woff')
			format('woff');
	unicode-range: U+65-90, U+97-122;
}
```

We load this subset first.

```css
.fonts-loaded-1 body {
	font-family: LatoSubset;
}
```

```javascript
if ('fonts' in document) {
	document.fonts.load('1em LatoSubset').then((_) => {
		document.documentElement.classList.add('fonts-loaded-1');
	});
}
```

And we load other font files later.

```css
.fonts-loaded-2 body {
	font-family: Lato;
}
```

```javascript
if ('fonts' in document) {
	document.fonts.load('1em LatoSubset').then((_) => {
		document.documentElement.classList.add('fonts-loaded-1');

		Promise.all([
			document.fonts.load('400 1em Lato'),
			document.fonts.load('700 1em Lato'),
			document.fonts.load('italic 1em Lato'),
			document.fonts.load('italic 700 1em Lato')
		]).then((_) => {
			document.documentElement.classList.add('fonts-loaded-2');
		});
	});
}
```

Again, we can optimize it for repeat views:

```javascript
function loadFonts() {
	if (sessionStorage.fontsLoaded) {
		document.documentElement.classList.add('fonts-loaded-2');
		return;
	}

	if ('fonts' in document) {
		document.fonts.load('1em LatoSubset').then((_) => {
			document.documentElement.classList.add('fonts-loaded-1');

			Promise.all([
				document.fonts.load('400 1em Lato'),
				document.fonts.load('700 1em Lato'),
				document.fonts.load('italic 1em Lato'),
				document.fonts.load('italic 700 1em Lato')
			]).then((_) => {
				document.documentElement.classList.add('fonts-loaded-2');

				// Optimization for Repeat Views
				sessionStorage.fontsLoaded = true;
			});
		});
	}
}
```

#### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-critical-foft-variants)Critical FOFT variants

Zach proposed two additional Critical FOFT variants:

-   Critical FOFT with Data URI
-   Critical FOFT with Preload

#### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-critical-foft-with-data-uris)Critical FOFT with data URIs

In this variant, we load the critical font (the subsetted roman font) with data URIs instead of a normal link. Here’s what it looks like. (And it’s scary.)

```css
@font-face {
	font-family: LatoSubset;
	src: url('data:application/x-font-woff;charset=utf-8;base64,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')
		format('woff');
	/* ... */
}
```

This code looks scary, but there’s no need to be scared. The hardest part here is generating the data URI, and [CSS-Tricks has us covered here](https://css-tricks.com/data-uris/).

#### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-critical-foft-with-preload)Critical FOFT with preload

In this variant, we add a link with the `preload` tag to the critical font file. Here’s what it looks like:

```html
<link
	rel="preload"
	href="path-to-roman-subset.woff2"
	as="font"
	type="font/woff2"
	crossorigin />
```

We should only preload one font here. If we load more than one, [we can adversely affect the initial load time](https://www.zachleat.com/web/preload/#use-with-a-font-loading-strategy).

In the [strategy list](https://www.zachleat.com/web/comprehensive-webfonts/), Zach also mentioned he prefers using a data URI over the `preload` variant. He only prefers it because browser support for `preload` used to be bad. Today, I feel that browser support is decent enough to choose preloading over a data URI.

This browser support data is from [Caniuse](http://caniuse.com/#feat=link-rel-preload), which has more detail. A number indicates that browser supports the feature at that version and up.

#### Desktop

| Chrome | Firefox | IE  | Edge | Safari |
| ------ | ------- | --- | ---- | ------ |
| 50     | 85      | No  | 79   | 11.1   |

#### Mobile / Tablet

| Android Chrome | Android Firefox | Android | iOS Safari |
| -------------- | --------------- | ------- | ---------- |
| 123            | 124             | 123     | 11.3-11.4  |

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-final-note-from-zach)Final note from Zach

Chris ran this article via Zach and Zach wished he prioritized a JavaScript-free approach in his [original article](https://www.zachleat.com/web/comprehensive-webfonts/).

> I think the article is good but I think my article that its based off of is probably a little dated in a few ways. I wish it prioritized no-JS approaches more when you’re only using one or two font files (or more but only 1 or 2 of each typeface). The JS approaches are kind of the exception nowadays I think (unless you’re using a **lot** of font files or a cloud provider that doesn’t support `font-display: swap`)

This switches the verdict a tiny bit, which I’m going to summarize in the next section.

### [](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#aa-which-font-loading-strategy-to-use)Which font loading strategy to use?

If you use a cloud-hosted provider:

-   Use `font-display: swap` if the host provides it.
-   Otherwise, use FOUT with class

If you host your web fonts, you have a few choices:

1. `@font-face` + `font-display: swap`
2. FOUT with Class
3. Standard FOFT
4. Critical FOFT

Here’s how to choose between them:

-   **Choose `@font-face` + `font-display: swap`** if you’re starting out and don’t want to mess with JavaScript. It’s the simplest of them all. Also choose this option if you use only few font files (fewer than two files) for each typeface.
-   **Choose Standard FOFT** if you’re ready to use JavaScript, but don’t want to do the extra work of subsetting the Roman font.
-   **Choose a Critical FOFT variant** if you want to go all the way for performance.

That’s it! I hope you found all of this useful!

If you loved this article, you may like other articles I wrote. Consider subscribing to my [newsletter](https://zellwk.com/newsletter/) 😉. Also, feel free to [reach out to me](https://zellwk.com/contact) if you have questions. I’ll try my best to help!

[![Digital Ocean - Simpler Cloud. Happier Devs. Better Results. Try for free](https://css-tricks.com/wp-content/uploads/2022/10/SimplerCloudHappierDevsRight.jpg)](https://try.digitalocean.com/css-tricks/?utm_medium=content_acq&utm_source=css-tricks&utm_campaign=global_brand_ad_en&utm_content=conversion_rightpane_simplercloudhappierdevs)

[See the difference yourself with a $200 free credit to try out DigitalOcean!](https://try.digitalocean.com/css-tricks/?utm_medium=content_acq&utm_source=css-tricks&utm_campaign=global_brand_ad_en&utm_content=conversion_rightpane_simplercloudhappierdevs)

[![Ad for ImageKit](https://static4.buysellads.net/uu/7/149579/1714152803-CSS-tricks_creatives.png)](https://srv.buysellads.com/ads/click/x/GTND427JCEBDE5QIC67LYKQUC6BIT2QYCV7DVZ3JCAYIV5QNCESIV53KC6SICKJNCKBIVK3LCWSILKJJF6AIC2JKC6SI423MCVYIKK3EHJNCLSIZ)

Sponsored [Real-time URL-based video optimization, transformation, & adaptive bitrate streaming for your videos](https://srv.buysellads.com/ads/click/x/GTND427JCEBDE5QIC67LYKQUC6BIT2QYCV7DVZ3JCAYIV5QNCESIV53KC6SICKJNCKBIVK3LCWSILKJJF6AIC2JKC6SI423MCVYIKK3EHJNCLSIZ)

[![ads via Carbon](https://srv.carbonads.net/static/30242/4f7f59796c5dda8f5dfc63a40583dfde7cebb050)](https://srv.carbonads.net/ads/click/x/GTND427JCEBIPKQJFTBLYKQUC6BDEKJICVBDLZ3JCAYIPK3ICKYIKK3KC6SICKJNCKBIVK3LCWSILKJJF6AIC53KC6SI423MCVYIKK3EHJNCLSIZ) [ Design and Development tips in your inbox. Every weekday. ](https://srv.carbonads.net/ads/click/x/GTND427JCEBIPKQJFTBLYKQUC6BDEKJICVBDLZ3JCAYIPK3ICKYIKK3KC6SICKJNCKBIVK3LCWSILKJJF6AIC53KC6SI423MCVYIKK3EHJNCLSIZ) [ads via Carbon](http://carbonads.net/?utm_source=csstrickscom&utm_medium=ad_via_link&utm_campaign=in_unit&utm_term=carbon)

![ads via Carbon](https://segment.prod.bidr.io/associate-segment?buzz_key=dsp&segment_key=dsp-19102)![ads via Carbon](https://secure.adnxs.com/seg?add=37012073&t=2)

_Psst!_ Create a DigitalOcean account and get [$200 in free credit](https://try.digitalocean.com/css-tricks/?utm_medium=content_acq&utm_source=css-tricks&utm_campaign=global_brand_ad_en&utm_content=conversion_postarticle_psst) for cloud-based hosting and services.

## Comments

1. Glenn

    [Permalink to comment#](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#comment-1769250) March 2, 2021

    In regards to the FOUT with Class suggestion, I have some rebuttles.  
    1\. On repaints, it’s a bit pedantic but sure, fonts will load at different rates so I’ll give you that one.  
    2 and 3. User preferences / slow connection: This can be taken care of with the prefers-reduced-data media query (low browser support for now though).  
    The fourth point about loading local fonts can be taken care of with the “local” attribute in your font-face declaration. For example:

    ```
    @font-face {
      font-family: 'Inter';
      src:
        local('Inter Regular'),
        local('Inter-Regular'),
        url('../fonts/Inter-Regular.woff2') format('woff2'),
        url('../fonts/Inter-Regular.woff') format('woff');
      font-weight: normal;
      font-style: normal;
      font-display: swap;
    }
    ```

    These suggestions basically seem to be fighting the browser in a way that probably isn’t necessary.  
    I don’t mean to say you SHOULDN’T do these things – after all the point of the article is the absolute best performance you can get out of font-loading. My points are more of a Developer Experience point.

2. Sora2455

    [Permalink to comment#](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#comment-1769251) March 2, 2021

    You forgot to actually set sessionStorage.fontsLoaded when you loaded the fonts…

    Also, the definitions of LatoInitial and Lato are identical, so I’m not sure why we’re swapping between them.

    Finally, I prefer font-display: swap myself. Any bugs in it are the browser’s job to fix, not mine, and it works without JS – which none of your other strategies do.

    - the_art_of_disappearing
      [Permalink to comment#](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#comment-1769297) March 3, 2021
      Thanks for pointing out the missing `sessionStorage.setItem("fontsLoaded", 1);` statement. I was wondering how that was being set!
    - Guillaume
      [Permalink to comment#](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#comment-1769306) March 4, 2021
        > Finally, I prefer font-display: swap myself. Any bugs in it are the browser’s job to fix, not mine, and it works without JS – which none of your other strategies do.
        > Loading with JS speeds up font loading, since it can start before the DOM is loaded, while `font-display: swap` will load it after. This ensures that the font is not loaded when it’s not used in the DOM.
        > But a JS free version of this would be great (eg. `font-display: swap eager`?), I agree.
    - Chris Z
      [Permalink to comment#](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#comment-1769312) March 4, 2021
      Sora is correct about the duplicate font declaration. If you look at [Zach Leatherman’s demo code](https://gist.githubusercontent.com/zachleat/3b9414a4be8565999a5d483039cf82d1/raw/ad654f97667f7355c4b49d0a64cb35e3cc1dfff7/foft.html), he doesn’t do that.

3. Chris Z

    [Permalink to comment#](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#comment-1769314) March 4, 2021

    For what it’s worth, I’ve written a WordPress plugin to aid in implementing Zach’s [preferred font-loading recipe](https://github.com/zachleat/web-font-loading-recipes#the-compromise-critical-foft-with-preload-with-a-polyfill-fallback-emulating-font-display-optional). Search for “WP FOFT Loader” in the plugins repository if you’d like to try it out.

4. Adam Norwood

    [Permalink to comment#](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#comment-1769321) March 4, 2021

    Thanks for this summary — I’ve followed Zach’s excellent blog post for years with all of the updates, and I’m so glad that the Font Loading API is now reasonably good enough for most purposes (but good ol’ FontFaceObserver and other JS workarounds can still function to patch things up where better performance or support is needed). Such a confusing topic!

    Also I hope that some of these techniques become less relevant when variable fonts are more widely available. Delivering one optimized web font is so much nicer than having to queue up separate downloads for each variant.

    As Sora2455 has already noted, the code examples on this post have minor errors that, as written, would lead to them not actually being helpful:

    All of the examples with `sessionStorage.fontsLoaded` need to have that property actually set to `true` in the `then()` method, otherwise those conditionals will never get hit and fonts will just continue to load on every subsequent page load. (I’ve accidentally done this on a production site and didn’t notice for quite a while! ugh!)  
    The _Standard FOFT_ example with `LatoInitial` and `Lato` would only make sense if additional `Lato` references were added for other weights and styles — maybe those can be added to the example, so that that section has an understandable purpose?

    Also, it might be worth mentioning that many web font licenses forbid modifications like subsetting and maybe even conversion from the foundry’s provided format (e.g. using FontSquirrel or `fonttools` to convert a .otf to .woff2), which could be a consideration depending on what the reader wants to do…

5. Chloe

    [Permalink to comment#](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#comment-1770045) March 23, 2021

    If you use the “fout with class” method does it make sense to also preload the font?

6. Shawn

    [Permalink to comment#](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#comment-1770801) April 14, 2021

    Has anyone had success with reducing CLS caused by using Typekit fonts & display: swap? As mentioned in the article, Adobe now recommends using their css ” method, so there is no ‘wf-loaded’ class to work with anymore. I have the display: swap option enabled, but of course the fallback fonts and the loaded fonts have different line heights, so there is always CLS rearing its ugly head.

7. edoardo+gargano

    [Permalink to comment#](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/#comment-1774888) June 29, 2021

    ```
    function loadFonts() {
      if (sessionStorage.fontsLoaded) {
        document.documentElement.classList.add('fonts-loaded')
        return
      }

      if ('fonts' in document) {
        Promise.all([
          document.fonts.load('1em Inter'),
          document.fonts.load('700 1em Inter'),
          document.fonts.load('italic 1em Inter'),
          document.fonts.load('italic 700 1em Inter')
        ]).then(_ => {
          document.documentElement.classList.add('fonts-loaded')
          // Optimization for Repeat Views
          sessionStorage.fontsLoaded = true
        })
      }
    }

    loadFonts()
    ```

    Just fix 2 typo for future visitors

This comment thread is closed. If you have important information
