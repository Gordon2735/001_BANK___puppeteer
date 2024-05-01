# Web Component for a Code Block

[![Avatar of Chris Coyier](https://secure.gravatar.com/avatar/8081b26e05bb4354f7d65ffc34cbbd67?s=80&d=retro&r=pg)](https://css-tricks.com/author/chriscoyier/)

[Chris Coyier](https://css-tricks.com/author/chriscoyier/) on Feb 18, 2020

We’ll get to that, but first, a long-winded introduction.

I’m still not in a confident place knowing _a good time_ to use native web components. The templating isn’t particularly robust, so that doesn’t draw me in. There is no state management, and I like having standard ways of handling that. If I’m using another library for components anyway, seems like I would just stick with that. So, at the moment, my checklist is something like:

-   Not using any other JavaScript framework that has components
-   Templating needs aren’t particularly complex
-   Don’t need particularly performant re-rendering
-   Don’t need state management

I’m sure there is tooling that helps with these things and more (the [devMode episode](https://devmode.fm/episodes/framework-agnostic-web-components-with-stencil) with some folks from [Stencil](https://stenciljs.com/) was good), but if I’m going to get into tooling-land, I’d be extra tempted to go with a framework, and probably not framework _plus another thing with a lot of overlap._

The reasons I _am_ tempted to go with native web components are:

-   They are native. No downloads of frameworks.
-   The Shadow DOM is a true encapsulation in a way a framework can’t really do.
-   I get to build my own HTML element that I use in HTML, with my own API design.

It sorta seems like the sweet spot for native web components is design system components. You build out your own little API for the components in your system, and people can use them in a way that is a lot safer than _just copy and paste this chunk of HTML_. And I suppose if consumers of the system wanted to BYO framework, they could.

So you can use like `<our-tabs active-tab="3">` rather than `<div class="tabs"> ... <a href="#3" class="tab-is-active">`. Refactoring the components certainly gets a lot easier as changes percolate everywhere.

I’ve used them here on CSS-Tricks for our `<circle-text>` component. It takes the radius as a parameter and the content via, uh, content, and outputs an `<svg>` that does the trick. It gave us a nice API for authoring that abstracted away the complexity.

### [](https://css-tricks.com/web-component-for-a-code-block/#aa-so)So!

It occurred to me a “code block” might be a nice use-case for a web component.

-   The API would be nice for it, as you could have attributes control useful things, and the code itself as the content (which is a great fallback).
-   It doesn’t really need state.
-   Syntax highlighting is a big gnarly block of CSS, so it would be kinda cool to isolate that away in the Shadow DOM.
-   It could have useful functionality like a “click to copy” button that people might enjoy having.

Altogether, it might feel like a _yeah, I could use this_ kinda component.

**This probably isn’t really production ready** (for one thing, it’s not on npm or anything yet), but here’s where I am so far:

CodePen Embed Fallback

Here’s a thought dump!

-   What do you do when a component depends on a third-party lib? The syntax highlighting here is done with [Prism.js](https://prismjs.com/). To make it more isolated, I suppose you could copy and paste the whole lib in there somewhere, but that seems silly. Maybe you just document it?
-   Styling web components [doesn’t feel like it has a great story yet](https://css-tricks.com/thinking-through-styling-options-for-web-components/), despite the fact that Shadow DOM is cool and useful.
-   Yanking in pre-formatted text to use in a template is super weird. I’m sure it’s possible to do without needing a `<pre>` tag inside the custom element, but it’s clearly much easier if you grab the content from the `<pre>`. Makes the API here just a smidge less friendly (because I’d prefer to use the `<code-block>` alone).
-   I wonder what a good practice is for passing along attributes that another library needs. Like is `data-lang="CSS"` OK to use (feels nicer), and then convert it to `class="language-css"` in the template because that’s what Prism wants? Or is it better practice to just pass along attributes as they are? (I went with the latter.)
-   People complain that there aren’t really “lifecycle methods” in native web components, but at least you have one: when the thing renders: `connectedCallback`. So, I suppose you should do all the manipulation of HTML and such before you do that final `shadowRoot.appendChild(node);`. I’m not doing that here, and instead am running Prism over the whole `shadowRoot` after it’s been appended. Just seemed to work that way. I imagine it’s probably better, and possible, to do it ahead of time rather than allow all the repainting caused by injecting spans and such.
-   The whole point of this is a nice API. Seems to me thing would be nicer if it was possible to drop un-escaped HTML in there to highlight and it could escape it for you. But that makes the fallback actually render that HTML which could be bad (or even theoretically insecure). What’s a good story for that? Maybe put the HTML in HTML comments and test if `<!--` is the start of the content and handle that as a special situation?

Anyway, if you wanna fork it or do anything fancier with it, lemme know. Maybe we can eventually put it on npm or whatever. We’ll have to see how useful people think it could be.

[![Digital Ocean - Simpler Cloud. Happier Devs. Better Results. Try for free](https://css-tricks.com/wp-content/uploads/2022/10/SimplerCloudHappierDevsRight.jpg)](https://try.digitalocean.com/css-tricks/?utm_medium=content_acq&utm_source=css-tricks&utm_campaign=global_brand_ad_en&utm_content=conversion_rightpane_simplercloudhappierdevs)

[See the difference yourself with a $200 free credit to try out DigitalOcean!](https://try.digitalocean.com/css-tricks/?utm_medium=content_acq&utm_source=css-tricks&utm_campaign=global_brand_ad_en&utm_content=conversion_rightpane_simplercloudhappierdevs)

[![Ad for ImageKit](https://static4.buysellads.net/uu/7/149579/1714152803-CSS-tricks_creatives.png)](https://srv.buysellads.com/ads/click/x/GTND427JCEBDLKJ7C67LYKQUC6BIT2QICYYDTZ3JCAYIV5QNF67I5KJKC6SICKJNCKBIVK3LCWSILKJLCAADLKJKC6SI423MCVBI6K3EHJNCLSIZ)

Sponsored [Real-time URL-based video optimization, transformation, & adaptive bitrate streaming for your videos](https://srv.buysellads.com/ads/click/x/GTND427JCEBDLKJ7C67LYKQUC6BIT2QICYYDTZ3JCAYIV5QNF67I5KJKC6SICKJNCKBIVK3LCWSILKJLCAADLKJKC6SI423MCVBI6K3EHJNCLSIZ)

[![ads via Carbon](https://srv.carbonads.net/static/30242/719965462940ad21c4bd0152867ef8e38cb4fc3f)](https://srv.carbonads.net/ads/click/x/GTND427JCEBIV27MFTBLYKQUC6BIT2QWCTBDCZ3JCAYIV5QNF67IE27KC6SICKJNCKBIVK3LCWSILKJLCAAITKQKC6SI423MCVBI6K3EHJNCLSIZ) [ Fast implementation, a customizable login experience, and flexible user journeys. Try Auth0 for free ](https://srv.carbonads.net/ads/click/x/GTND427JCEBIV27MFTBLYKQUC6BIT2QWCTBDCZ3JCAYIV5QNF67IE27KC6SICKJNCKBIVK3LCWSILKJLCAAITKQKC6SI423MCVBI6K3EHJNCLSIZ) [ads via Carbon](http://carbonads.net/?utm_source=csstrickscom&utm_medium=ad_via_link&utm_campaign=in_unit&utm_term=carbon)

![ads via Carbon](https://segment.prod.bidr.io/associate-segment?buzz_key=dsp&segment_key=dsp-19103)![ads via Carbon](https://secure.adnxs.com/seg?add=37012074&t=2)

_Psst!_ Create a DigitalOcean account and get [$200 in free credit](https://try.digitalocean.com/css-tricks/?utm_medium=content_acq&utm_source=css-tricks&utm_campaign=global_brand_ad_en&utm_content=conversion_postarticle_psst) for cloud-based hosting and services.

## Comments

1. Justin Ribeiro

    [Permalink to comment#](https://css-tricks.com/web-component-for-a-code-block/#comment-1754509) February 18, 2020

    The problem with most of the highlighters is that they don’t use ES Modules and it’s makes them hard to consume. Justin Fagnani and I have talked about this previously (ala, registries and custom namespaces).

    My code-block web component uses Prism and LitElement in a particularly dynamic loading way to cut weight and make it flexible: [https://github.com/justinribeiro/code-block](https://github.com/justinribeiro/code-block) and is available on NPM [https://www.npmjs.com/package/@justinribeiro/code-block](https://www.npmjs.com/package/@justinribeiro/code-block) I use it on my site extensively and in internal projects. It’s by no means ideal (themes work for instance, but I haven’t revisited making it easier to handle).

    Fagnani forked Rainbow to handle his case, updating it to make the module experience better ([https://www.npmjs.com/package/@justinfagnani/rainbow](https://www.npmjs.com/package/@justinfagnani/rainbow)).

2. Jamie

    [Permalink to comment#](https://css-tricks.com/web-component-for-a-code-block/#comment-1754525) February 19, 2020

    One small things solved:

    > WTF with the !important on the pre background.  
    > Not sure what that is overriding but seems to be necessary.

    Turns out, you need to get rid of the

    ```css
    background: none;
    ```

    So it becomes this:

    ```css
    pre[class*="language-"] {
      background: #111;
      color: white;
    ```

    This was just a small overlook on your part :)

    - Chris Coyier
      [Permalink to comment#](https://css-tricks.com/web-component-for-a-code-block/#comment-1754540) February 19, 2020
      Derp!

This comment thread is closed. If you have important inform
