# Styling Code In and Out of Blocks

[![Avatar of Chris Coyier](https://secure.gravatar.com/avatar/8081b26e05bb4354f7d65ffc34cbbd67?s=80&d=retro&r=pg)](https://css-tricks.com/author/chriscoyier/)

[Chris Coyier](https://css-tricks.com/author/chriscoyier/) on Jan 6, 2021

There is a `<code>` tag in HTML. I literally just used it to wrap that tag in the previous sentence — so meta. It is an inline-by-default element that denotes any sort of code. It has default (user agent) styles that apply a monospace font-family, which feels like a fine default (as it’s true, most code is looked at in monospace).

```css
/* User agent styles in all browsers */
code {
    font-family: monospace;
}
```

It’s likely something that you’ll _style with the tag itself_ as well in your stylesheets. It’s just one of those elements where it seems far more natural to just use it raw, as opposed to resetting it to no styles and opting into styles with a class.

```css
/* You'll probably do this: */
code {
    /* custom styles */
}

/* Or maybe scope it to something like: */
article code {
}

/* It seems less common and more annoying to do this: */
code {
    /* reset styles */
}

code.some-class {
    /* opt-in styles */
}
```

On this site right now (v18), I apply some modest styles and scope some of them within textual elements:

```css
/* For all <code> */
code {
    font-family: MyFancyCustomFont, monospace;
    font-size: inherit;
}

/* Code in text */
p > code,
li > code,
dd > code,
td > code {
    background: #ffeff0;
    word-wrap: break-word;
    box-decoration-break: clone;
    padding: 0.1rem 0.3rem 0.2rem;
    border-radius: 0.2rem;
}
```

One thing this helps with is, say, this:

```html
<h3>The <code>.cool</code> Class</h3>
```

My styles will still make that a nice monospace font, size it to be the same as the header, but _not_ apply the background color and padding stuff I like for code within text.

![](https://i0.wp.com/css-tricks.com/wp-content/uploads/2020/12/Screen-Shot-2020-12-31-at-1.29.28-PM.png?resize=518%2C109&ssl=1)

The bigger deal when it comes to scoped-styles for `<code>` though is this very common markup:

```html
<pre><code>
  example code block
</code></pre>
```

The `<pre>` tag is important for displaying code blocks, as it respects whitespace in the HTML. But semantically, it just means “pre-formatted text.” If it’s a code block, there should be a `<code>` tag involved too. But `<code>`, remember, is an inline element. Plus, it’s highly likely that how you want it to look within a sentence is quite different from how you want it to look in a block.

Jason was tweeting about this the other day:

There was a moment of confusion in the thread where:

```css
/* this was working */
.post :not(pre) code {
}

/* and this was not */
:not(pre) code {
}
```

The problem with the second “at the root” selector is that `:not(pre)` will match things (like the `<body>`) and thus apply those styles. Within the post (the first example), it’s only going to select things — like paragraph tags and images and such — and thus behave more expectedly. I think that’s a fine approach. It’s just an alternative way of doing the scoping on that `<code>` tag such that it doesn’t get certain styles while it’s within specific elements, because the `<pre>` tag being the primary concern.

I have lots code blocks on this site, so I try to be a bit extra protective. I specifically style the `<code>` elements that within `<pre>` tags with a lot of styles to get them how I want, and potentially fight against any other undesirable styles they may have. Stuff like:

```css
pre code {
    display: block;
    background: none;
    white-space: pre;
    -webkit-overflow-scrolling: touch;
    overflow-x: scroll;
    max-width: 100%;
    min-width: 100px;
    padding: 0;
}
```

My actual styles are a bit more verbose, even than that. There is nothing clever about that snippet. I’m just pointing out that I apply a pretty good heap of styles to code blocks to make darn sure they come out right.

I find it interesting how the `<code>` element is somewhat unique in just how differently we tend to style it depending on context.

---

**Article** on Jan 14, 2020

### [](https://css-tricks.com/styling-code-in-and-out-of-blocks/#aa-considerations-for-styling-the-pre-tag)[Considerations for styling the \`pre\` tag](https://css-tricks.com/considerations-styling-pre-tag/)

[code](https://css-tricks.com/tag/code/)

[![](https://secure.gravatar.com/avatar/8081b26e05bb4354f7d65ffc34cbbd67?s=80&d=retro&r=pg)](https://css-tricks.com/author/chriscoyier/) [Chris Coyier](https://css-tricks.com/author/chriscoyier/)

**Article** on Feb 18, 2020

### [](https://css-tricks.com/styling-code-in-and-out-of-blocks/#aa-web-component-for-a-code-block)[Web Component for a Code Block](https://css-tricks.com/web-component-for-a-code-block/)

[code](https://css-tricks.com/tag/code/)

[![](https://secure.gravatar.com/avatar/8081b26e05bb4354f7d65ffc34cbbd67?s=80&d=retro&r=pg)](https://css-tricks.com/author/chriscoyier/) [Chris Coyier](https://css-tricks.com/author/chriscoyier/)

[![Digital Ocean - Simpler Cloud. Happier Devs. Better Results. Try for free](https://css-tricks.com/wp-content/uploads/2022/10/SimplerCloudHappierDevsRight.jpg)](https://try.digitalocean.com/css-tricks/?utm_medium=content_acq&utm_source=css-tricks&utm_campaign=global_brand_ad_en&utm_content=conversion_rightpane_simplercloudhappierdevs)

[See the difference yourself with a $200 free credit to try out DigitalOcean!](https://try.digitalocean.com/css-tricks/?utm_medium=content_acq&utm_source=css-tricks&utm_campaign=global_brand_ad_en&utm_content=conversion_rightpane_simplercloudhappierdevs)

[![Ad for ImageKit](https://static4.buysellads.net/uu/7/149579/1714152803-CSS-tricks_creatives.png)](https://srv.buysellads.com/ads/click/x/GTND427JCEBI427YCWSLYKQUC6BIT2JLCEBDEZ3JCAYIV5QNCTSIEK3KC6SICKJNCKBIVK3LCWSILKJJCE7IVKQKC6SI423MCWYDVK3EHJNCLSIZ)

Sponsored [Real-time URL-based video optimization, transformation, & adaptive bitrate streaming for your videos](https://srv.buysellads.com/ads/click/x/GTND427JCEBI427YCWSLYKQUC6BIT2JLCEBDEZ3JCAYIV5QNCTSIEK3KC6SICKJNCKBIVK3LCWSILKJJCE7IVKQKC6SI423MCWYDVK3EHJNCLSIZ)

[![ads via Carbon](https://srv.carbonads.net/static/30242/4f7f59796c5dda8f5dfc63a40583dfde7cebb050)](https://srv.carbonads.net/ads/click/x/GTND427JCEBI6KJIFTBLYKQUC6BDEK7MCYSDPZ3JCAYIPK3LC6YDTK3KC6SICKJNCKBIVK3LCWSILKJJCE7IK23KC6SI423MCWYDVK3EHJNCLSIZ) [ Design and Development tips in your inbox. Every weekday. ](https://srv.carbonads.net/ads/click/x/GTND427JCEBI6KJIFTBLYKQUC6BDEK7MCYSDPZ3JCAYIPK3LC6YDTK3KC6SICKJNCKBIVK3LCWSILKJJCE7IK23KC6SI423MCWYDVK3EHJNCLSIZ) [ads via Carbon](http://carbonads.net/?utm_source=csstrickscom&utm_medium=ad_via_link&utm_campaign=in_unit&utm_term=carbon)

![ads via Carbon](https://segment.prod.bidr.io/associate-segment?buzz_key=dsp&segment_key=dsp-19102)![ads via Carbon](https://secure.adnxs.com/seg?add=37012073&t=2)

_Psst!_ Create a DigitalOcean account and get [$200 in free credit](https://try.digitalocean.com/css-tricks/?utm_medium=content_acq&utm_source=css-tricks&utm_campaign=global_brand_ad_en&utm_content=conversion_postarticle_psst) for cloud-based hosting and services.

## Comments

1. Daniel M

    [Permalink to comment#](https://css-tricks.com/styling-code-in-and-out-of-blocks/#comment-1767089) January 7, 2021

    The `:not(pre) code` selector matching `<body>` can easily be fixed with `:not(pre) > code`. This will target `<code>` blocks that don’t have a `<pre>` tag as the immediate parent, which decouples the CSS from requiring a `.post` ancestor. Naturally the same works for `pre > code` to target `<code>` tags directly within `<pre>` tags, regardless of where they are. Handy for setting up common style settings like that block at the end of your post.

2. jimpogo

    [Permalink to comment#](https://css-tricks.com/styling-code-in-and-out-of-blocks/#comment-1767416) January 19, 2021

    When I see `pre` `code` I instantly think of 1920s and 30’s movies, the so-called pre-code years, before the Hays Code kicked in.

This comment thread is closed. If you have important inform
