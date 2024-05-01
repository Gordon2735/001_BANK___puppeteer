# Check if an Object is Empty in TypeScript

Last Updated : 01 Mar, 2024



In [TypeScript](https://www.geeksforgeeks.org/introduction-to-typescript/), checking if an object is empty or not can be done by checking the properties of the object. We can check for the presence of properties in the object using various built-in methods and loops. In this article, we will explore three different approaches for checking if an object is empty or not in TypeScript.

Table of Content

-   [Using Object.keys() function](https://www.geeksforgeeks.org/check-if-an-object-is-empty-in-typescript/#using-objectkeys-function)
-   [Using for…in Loop](https://www.geeksforgeeks.org/check-if-an-object-is-empty-in-typescript/#using-forin-loop)
-   [Using JSON.stringify() function](https://www.geeksforgeeks.org/check-if-an-object-is-empty-in-typescript/#using-jsonstringify-function)

## Using Object.keys() function

In this approach, we are using the [Object.keys()](https://www.geeksforgeeks.org/javascript-object-keys-method/) function in TypeScript to check if an object is empty. The condition \***\*Object.keys(obj).length === 0\*\*** evaluates to true when the object (obj) has no properties, which indicates that the object is empty

### Syntax:

Object.keys(obj)

\***\*Example:\*\*** The below example uses Object.keys() function to check if an Object is empty in TypeScript.

```css
:root {
	--avp-font-family: Gilroy, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont,
		'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif;
	--avp-brand-color: #ed1e1e;
	--avp-color: #fff;
	--avp-border-radius: 4px;
	--avp-source-background: #000;
	--avp-view-background: #0000004d;
	--avp-overlay-background: #0000008c;
	--avp-edge-row-indent: 0px;
	--avp-edge-column-indent: var(--avp-edge-row-indent);
	--avp-scale: 0.5;
	--avp-offset-top: 0px;
	--avp-offset-right: 0px;
	--avp-offset-bottom: 0px;
	--avp-offset-left: 0px;
	--avp-transition-duration: 0.2s;
	--avp-transition: opacity var(--avp-transition-duration), transform var(--avp-transition-duration),
		rotate var(--avp-transition-duration), translate var(--avp-transition-duration),
		scale var(--avp-transition-duration);
	--avp-transition-scale-value: 1.5;
	--avp-transition-move-value: 100%;
	--avp-main-width: 100%;
	--avp-main-height: 100%;
	--avp-view-width: 480px;
	--avp-view-height: 100%;
	--avp-view-aspect-ratio: 16/9;
	--avp-primary-control-size: 42px;
	--avp-primary-control-max-size-factor: 0.25;
	--avp-primary-control-padding: 8px;
	--avp-primary-control-transition-bend: -0.15;
	--avp-primary-control-transform-origin-bend: 2;
	--avp-primary-middle-control-size: 48px;
	--avp-primary-middle-control-padding: 4px;
	--avp-secondary-control-size: 24px;
	--avp-secondary-control-padding: 4px;
	--avp-secondary-control-background-color: #0000;
	--avp-secondary-control-border-radius: 0;
	--avp-volume-slider-block-size: 3px;
	--avp-volume-slider-inline-size: 57px;
	--avp-volume-slider-volume: 1;
	--avp-volume-thumb-diameter: 10px;
	--avp-timeline-block-size: 6px;
	--avp-timeline-minimize-scale-factor: 0.6667;
	--avp-timeline-clickable-area-gap: 12px;
	--avp-timeline-chapter-gap: 2px;
	--avp-timeline-chapter-gap-in-fullscreen: 3px;
	--avp-timeline-pointer-scale-factor: 2.167;
	--avp-timeline-pointer-size: calc(
		var(--avp-timeline-block-size) \* var(
				--avp-timeline-pointer-scale-factor
			)
	);
	--avp-close-button-overlay-margin: 30px;
	--avp-close-button-overlay-top: 3px;
	--avp-close-button-overlay-right: 3px;
	--avp-close-button-overlay-bottom: 3px;
	--avp-close-button-overlay-left: 0px;
	--avp-logo-inline-offset: var(--avp-secondary-control-padding);
	--avp-logo-block-offset: var(--avp-logo-inline-offset);
	--avp-logo-image-width: 16px;
	--avp-logo-image-height: var(--avp-logo-image-width);
	--avp-logo-image-aspect-ratio: 1;
	--avp-logo-title-offset: 4px;
	--avp-auto-skip-track-size: 5px;
	--avp-auto-skip-progress-color: var(--avp-brand-color);
	--avp-caption-height: 24px;
	--avp-caption-padding: 5px;
	--avp-carousel-view-inline-size: 100%;
	--avp-carousel-view-block-size: 100%;
	--avp-carousel-items-per-page: 4;
	--avp-carousel-item-inline-size: 25%;
	--avp-carousel-item-block-size: 100%;
	--avp-carousel-item-gap: 5px;
	--avp-carousel-prev-next-control-inline-size: 44px;
	--avp-carousel-item-placeholder-image-background: #d0d0d0;
	--avp-playlist-background-color: #0000;
	--avp-annotation-background-color: #ffffffd9;
	--avp-annotation-color: #000;
	--avp-annotation-font-size: 16px;
	--avp-annotation-text-align: left;
	--avp-aside-color: var(--avp-color);
	--avp-aside-font-size: 16px;
	--avp-aside-font-family: inherit;
	--avp-aside-text-align: left;
	--avp-top-height: calc(
		var(--avp-secondary-control-size) + var(--avp-edge-row-indent) \* 2
	);
	--avp-bottom-height: var(--avp-top-height);
	--avp-control-panel-block-size: calc(
		var(--avp-secondary-control-size) + var(--avp-timeline-block-size)
	);
	--avp-left-width: 35%;
	--avp-read-more-button-background-color: var(--avp-brand-color);
	--avp-read-more-button-text-color: var(--avp-color);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[avp\] {
	background: none;
	border: none;
	border-radius: 0;
	box-shadow: none;
	box-sizing: border-box;
	color: inherit;
	cursor: inherit;
	flex-direction: row;
	font: inherit;
	height: auto;
	letter-spacing: inherit;
	line-height: 1;
	margin: 0;
	max-width: none;
	min-height: 0;
	min-width: 0;
	outline: none;
	overflow: visible;
	padding: 0;
	pointer-events: inherit;
	position: static;
	text-align: inherit;
	-webkit-text-decoration: none;
	text-decoration: none;
	transform: none;
	transition: none;
	vertical-align: initial;
	white-space: inherit;
	width: auto;
	word-break: inherit;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) aside\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) div\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) p\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) section\[avp\] {
	display: block;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) span\[avp\] {
	display: inline;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) a\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) button\[avp\] {
	background: none;
	border: none;
	padding: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) a\[href\]\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) button\[avp\] {
	cursor: pointer;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) canvas\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) img\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) video\[avp\] {
	overflow: hidden;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) img\[avp\] {
	vertical-align: top;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) strong\[avp\] {
	font-weight: 600;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[inert\]\[avp\] {
	pointer-events: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[hidden\]\[avp\] {
	display: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) avp-icon\[avp\] {
	fill: #fff;
	stroke: #fff;
	transform-box: fill-box;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon
	svg\[avp\] {
	display: block;
	height: 100%;
	overflow: hidden;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-button\[avp\] {
	background-color: var(--avp-secondary-control-background-color);
	border-radius: var(--avp-secondary-control-border-radius);
	color: var(--avp-color);
	cursor: pointer;
	flex-shrink: 0;
	height: var(--avp-secondary-control-size);
	padding: var(--avp-secondary-control-padding);
	pointer-events: auto;
	width: var(--avp-secondary-control-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-button
	avp-icon\[avp\] {
	fill: currentColor;
	stroke: currentColor;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-button.avp-primary\[avp\] {
	height: var(--avp-primary-control-size);
	padding: var(--avp-primary-control-padding);
	width: var(--avp-primary-control-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-transition-active\[avp\] {
	transition: var(--avp-transition);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fade-enter-from\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fade-leave-done\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fade-leave-to\[avp\] {
	opacity: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scale-enter-from\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scale-leave-done\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scale-leave-to\[avp\] {
	opacity: 0;
	scale: var(--avp-transition-scale-value);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scale-down-enter-from\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scale-down-leave-done\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scale-down-leave-to\[avp\] {
	opacity: 0;
	scale: 0.5;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-left-enter-from\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-left-leave-done\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-left-leave-to\[avp\] {
	opacity: 0;
	translate: var(--avp-transition-move-value);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-right-enter-from\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-right-leave-done\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-right-leave-to\[avp\] {
	opacity: 0;
	translate: calc(var(--avp-transition-move-value) \* -1);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-up-enter-from\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-up-leave-done\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-up-leave-to\[avp\] {
	opacity: 0;
	translate: 0 var(--avp-transition-move-value);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-down-enter-from\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-down-leave-done\[avp\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-move-down-leave-to\[avp\] {
	opacity: 0;
	translate: 0 calc(var(--avp-transition-move-value) \* -1);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-cross-placement-container\[avp\] {
	display: grid;
	grid-template: minmax(0, 1fr) / minmax(0, 1fr);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-cross-placement-container
	> \[avp\] {
	grid-area: 1/1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-no-scrollbars\[avp\]::-webkit-scrollbar {
	height: 0;
	width: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-no-scrollbars\[avp\] {
	-ms-overflow-style: none;
	overflow: -moz-scrollbars-none;
	scrollbar-width: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-no-scrollbars\[avp\]::-webkit-scrollbar {
	display: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-reflect\[avp\] {
	transform: scaleX(-1);
	transform-origin: center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1e4-h\] {
	--avp-control-panel-block-size: calc(
		var(--avp-secondary-control-size) + var(--avp-timeline-block-size)
	);
	--avp-read-more-button-background-color: var(--avp-brand-color);
	align-items: center;
	color: var(--avp-color);
	direction: ltr;
	display: flex;
	flex-direction: column;
	font-family: var(--avp-font-family);
	font-size: 16px;
	font-style: normal;
	font-weight: 400;
	letter-spacing: normal;
	overflow-anchor: none;
	scroll-behavior: smooth;
	tab-size: 4;
	text-align: left;
	width: 100%;
	word-break: normal;
	-webkit-tap-highlight-color: transparent;
	-webkit-overflow-scrolling: touch;
	-webkit-text-size-adjust: none;
	-moz-text-size-adjust: none;
	text-size-adjust: none;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1e4-h\]
	::cue {
	background: #0006;
	color: #fff;
	font: inherit;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1e4-h\]
	#videoslot.avp-loaded {
	animation: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =x4s\]\[\_382ee1e4-h\] {
	--avp-secondary-control-size: 32px;
	--avp-secondary-control-padding: 7px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =x3s\]\[\_382ee1e4-h\] {
	--avp-primary-middle-control-padding: 3px;
	--avp-secondary-control-size: 36px;
	--avp-secondary-control-padding: 9px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xxs\]\[\_382ee1e4-h\] {
	--avp-primary-control-padding: 6px;
	--avp-primary-control-size: 48px;
	--avp-primary-middle-control-size: 84px;
	--avp-primary-middle-control-padding: 12px;
	--avp-secondary-control-size: 42px;
	--avp-secondary-control-padding: 11px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]\[\_382ee1e4-h\] {
	--avp-primary-control-size: 72px;
	--avp-primary-control-padding: 18px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fullscreen\[\_382ee1e4-h\] {
	--avp-timeline-chapter-gap: 3px;
	--avp-timeline-block-size: 8px;
	--avp-timeline-minimize-scale-factor: 0.625;
	--avp-timeline-pointer-scale-factor: 2.5;
	--avp-timeline-pointer-size: calc(
		var(--avp-timeline-block-size) \* var(
				--avp-timeline-pointer-scale-factor
			)
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fullscreen\[w
	~ =xs\]\[\_382ee1e4-h\] {
	--avp-primary-control-size: 78px;
	--avp-primary-middle-control-size: 96px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fullscreen\[w
	~ =m\]\[\_382ee1e4-h\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =l\]\[\_382ee1e4-h\] {
	--avp-primary-control-size: 84px;
	--avp-primary-middle-control-size: 108px;
	--avp-secondary-control-size: 54px;
	--avp-secondary-control-padding: 14px;
	--avp-carousel-prev-next-control-inline-size: 72px;
	--avp-volume-slider-block-size: 4px;
	--avp-volume-slider-inline-size: 78px;
	--avp-volume-thumb-diameter: 16px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fullscreen\[w
	~ =l\]\[\_382ee1e4-h\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xl\]\[\_382ee1e4-h\] {
	--avp-carousel-prev-next-control-inline-size: 84px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-concealed\[\_382ee1e4-h\] {
	height: auto;
	pointer-events: none;
	position: absolute;
	visibility: hidden;
	width: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-dragging\[\_382ee1e4-h\]
	.avp-view\[\_382ee1e4\] {
	pointer-events: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-floating-container\[\_382ee1e4\] {
	background: var(--avp-background);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-shadow\[\_382ee1e4\] {
	box-shadow: 1px 1px 6px 3px #0006;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scale\[\_382ee1e4\] {
	scale: var(--avp-scale);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed\[\_382ee1e4\] {
	position: fixed;
	z-index: 10000001;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom-center\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top-center\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top\[\_382ee1e4\] {
	background: var(--avp-background, #000);
	left: var(--avp-offset-left);
	width: calc(100% - var(--avp-offset-left) - var(--avp-offset-right));
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top-center\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top-left\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top-right\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top\[\_382ee1e4\] {
	top: var(--avp-offset-top);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom-center\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom-left\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom-right\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom\[\_382ee1e4\] {
	bottom: var(--avp-offset-bottom);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom-right\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top-right\[\_382ee1e4\] {
	right: var(--avp-offset-right);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom-left\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top-left\[\_382ee1e4\] {
	left: var(--avp-offset-left);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top-center\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top\[\_382ee1e4\] {
	transform-origin: top;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top-left\[\_382ee1e4\] {
	transform-origin: top left;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top-right\[\_382ee1e4\] {
	transform-origin: top right;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom-center\[\_382ee1e4\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom\[\_382ee1e4\] {
	transform-origin: bottom;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom-left\[\_382ee1e4\] {
	transform-origin: bottom left;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom-right\[\_382ee1e4\] {
	transform-origin: bottom right;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-body\[\_382ee1e4\] {
	background: var(--avp-background);
	display: flex;
	justify-content: center;
	position: relative;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed
	.avp-body\[\_382ee1e4\] {
	background: var(--avp-background, #000);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-main\[\_382ee1e4\] {
	display: flex;
	flex-direction: column;
	flex-shrink: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e4-h\]
	.avp-main\[\_382ee1e4\] {
	flex-direction: row;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-source\[\_382ee1e4\] {
	background: var(--avp-source-background);
	height: var(--avp-view-height);
	position: relative;
	width: var(--avp-view-width);
	z-index: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fullscreen\[\_382ee1e4-h\]
	.avp-source\[\_382ee1e4\] {
	bottom: 0 !important;
	box-sizing: border-box !important;
	height: 100% !important;
	left: 0 !important;
	margin: 0 !important;
	max-height: none !important;
	max-width: none !important;
	min-height: 0 !important;
	min-width: 0 !important;
	object-fit: contain;
	position: fixed !important;
	right: 0 !important;
	top: 0 !important;
	transform: none !important;
	-webkit-user-select: text;
	user-select: text;
	width: 100% !important;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-source.avp-clickable\[\_382ee1e4\] {
	cursor: pointer;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee146-h\]
	svg {
	height: 0;
	overflow: hidden;
	position: absolute;
	width: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1e1-h\] {
	--avp-top-height: calc(
		var(--avp-secondary-control-size) + var(--avp-edge-column-indent) \* 2
	);
	--avp-bottom-height: var(--avp-top-height);
	display: flex;
	height: 100%;
	left: 0;
	overflow: hidden;
	pointer-events: none;
	position: absolute;
	top: 0;
	transition: background var(--avp-transition-duration);
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	\[\_382ee1e1-h\] {
	--avp-edge-row-indent: 5px;
	--avp-edge-column-indent: var(--avp-edge-row-indent);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =s\]
	\[\_382ee1e1-h\] {
	--avp-edge-row-indent: 10px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-ui-background\[\_382ee1e1-h\] {
	background: var(--avp-view-background);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-hidden\[\_382ee1e1-h\] {
	background: none;
	cursor: none;
	transform-origin: center center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-annotation\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-description\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-logo\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-next-preview\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-share\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-title\[\_382ee1e1\] {
	cursor: auto;
	pointer-events: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-bottom\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top\[\_382ee1e1\] {
	display: flex;
	justify-content: space-between;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-bottom\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-top\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top-center\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top-left\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top-right\[\_382ee1e1\] {
	display: flex;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top\[\_382ee1e1\] {
	flex: 0 0 var(--avp-top-height);
	padding: var(--avp-edge-column-indent) var(--avp-edge-row-indent);
}
@supports (display: grid) {
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-top\[\_382ee1e1\] {
		height: var(--avp-top-height);
	}
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top-center\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top-left\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top-right\[\_382ee1e1\] {
	align-items: center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top-center\[\_382ee1e1\] {
	flex: 1;
	flex-direction: column;
	justify-content: center;
	justify-self: center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-bottom\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-top\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle\[\_382ee1e1\] {
	display: grid;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle\[\_382ee1e1\] {
	flex: 1;
	flex-direction: column;
	position: relative;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-bottom\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-middle\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-top\[\_382ee1e1\] {
	pointer-events: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-bottom\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-top\[\_382ee1e1\] {
	height: 50%;
	transition: var(--avp-transition);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-top\[\_382ee1e1\] {
	align-items: flex-start;
	align-self: flex-start;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-top.avp-expanded\[\_382ee1e1\] {
	transform: translateY(
		calc(
			var(--avp-edge-row-indent) + var(--avp-secondary-control-padding) -
				var(--avp-top-height)
		)
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-middle\[\_382ee1e1\] {
	align-items: center;
	height: 100%;
	justify-content: center;
	position: absolute;
	width: 100%;
}
@supports (display: grid) {
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-middle-middle\[\_382ee1e1\] {
		position: static;
	}
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-bottom\[\_382ee1e1\] {
	align-items: flex-end;
	align-self: flex-end;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-middle-bottom.avp-expanded\[\_382ee1e1\] {
	transform: translateY(
		calc(
			var(--avp-bottom-height) - var(--avp-edge-row-indent) - var(--avp-secondary-control-padding)
		)
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-primary-controls\[\_382ee1e1\] {
	z-index: 2;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-bottom\[\_382ee1e1\] {
	align-items: flex-end;
	flex: 0 0 var(--avp-bottom-height);
}
@supports (display: grid) {
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-bottom\[\_382ee1e1\] {
		height: var(--avp-bottom-height);
	}
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-control-bar\[\_382ee1e1\] {
	display: flex;
	flex-shrink: 0;
	position: relative;
	z-index: 5;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-bottom\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-control-bar\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top\[\_382ee1e1\] {
	flex-shrink: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-bottom\[\_382ee1e1\]:before,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-control-bar\[\_382ee1e1\]:before,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top\[\_382ee1e1\]:before {
	content: '';
	opacity: 0;
	pointer-events: none;
	position: absolute;
	transition: opacity var(--avp-transition-duration);
	z-index: -2;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-bottom.avp-background-gradient\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-control-bar.avp-background-gradient\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top.avp-background-gradient\[\_382ee1e1\] {
	position: relative;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-bottom.avp-background-gradient\[\_382ee1e1\]:before,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-control-bar.avp-background-gradient\[\_382ee1e1\]:before,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top.avp-background-gradient\[\_382ee1e1\]:before {
	opacity: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-bottom\[\_382ee1e1\]:before,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top\[\_382ee1e1\]:before {
	left: 0;
	right: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e1-h\]
	.avp-bottom\[\_382ee1e1\]:before,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e1-h\]
	.avp-top\[\_382ee1e1\]:before {
	left: -100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top\[\_382ee1e1\]:before {
	background-image: linear-gradient(var(--avp-overlay-background), #0000);
	height: calc(var(--avp-top-height) \* 1.1);
	top: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-bottom\[\_382ee1e1\]:before {
	background-image: linear-gradient(
		#0000,
		var(--avp-overlay-background) 110%
	);
	bottom: 0;
	height: var(--avp-bottom-height);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-control-bar\[\_382ee1e1\]:before {
	background-image: linear-gradient(
		to left,
		#0000,
		var(--avp-overlay-background) 110%
	);
	bottom: 0;
	left: 0;
	top: 0;
	width: var(--avp-top-height);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top-left
	avp-logo\[\_382ee1e1\] {
	margin-right: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-top-right
	avp-logo\[\_382ee1e1\] {
	margin-left: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-heading\[\_382ee1e1\] {
	font-size: 14px;
	line-height: 1em;
	padding: 0 var(--avp-secondary-control-padding);
	white-space: nowrap;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	.avp-heading\[\_382ee1e1\] {
	font-size: 18px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =m\]
	.avp-heading\[\_382ee1e1\] {
	font-size: 20px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-heading
	avp-description\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-heading
	avp-title\[\_382ee1e1\] {
	overflow: hidden;
	padding: 1px 0;
	text-overflow: ellipsis;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =x4s\]
	.avp-heading
	avp-description\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =x4s\]
	.avp-heading
	avp-title\[\_382ee1e1\] {
	padding-bottom: 2px;
	padding-top: 2px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	.avp-heading
	avp-description\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	.avp-heading
	avp-title\[\_382ee1e1\] {
	padding-bottom: 3px;
	padding-top: 1px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =m\]
	.avp-heading
	avp-description\[\_382ee1e1\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =m\]
	.avp-heading
	avp-title\[\_382ee1e1\] {
	padding-bottom: 4px;
	padding-top: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-heading
	avp-title\[\_382ee1e1\] {
	font-weight: 600;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-heading
	avp-description\[\_382ee1e1\] {
	font-size: 0.7em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-auto-skip\[\_382ee1e1\] {
	margin-top: -15px;
	position: absolute;
	right: 0;
	top: 50%;
	z-index: 4;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =s\]
	avp-auto-skip\[\_382ee1e1\] {
	margin-top: calc(var(--avp-secondary-control-size) \* -1 / 2);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-auto-skip.avp-with-stay-button\[\_382ee1e1\] {
	margin-top: calc(-30px - var(--avp-auto-skip-track-size) / 2);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =s\]
	avp-auto-skip.avp-with-stay-button\[\_382ee1e1\] {
	margin-top: calc(
		var(--avp-secondary-control-size) \* -1 - var(
				--avp-auto-skip-track-size
			) / 2
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1e1-h\] {
	align-items: stretch;
	display: grid;
	flex-direction: column;
	grid-template-rows: auto 1fr auto;
}
@supports (width: max(0px, 0px)) {
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		\[\_382ee1e1-h\] {
		--avp-bottom-height: max(
			calc(
				var(--avp-secondary-control-size) + var(--avp-edge-row-indent) \*
					2
			),
			var(--avp-control-panel-block-size)
		);
	}
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =s\]
	.avp-playlist-open\[\_382ee1e1-h\]
	avp-primary-controls {
	transform: translateY(-50%);
	transition: var(--avp-transition);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =s\]
	.avp-playlist-visible\[\_382ee1e1-h\]
	avp-primary-controls {
	transition: var(--avp-transition);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-secondary-controls\[\_382ee1e1\] {
	align-items: flex-end;
	height: var(--avp-secondary-control-size);
	padding: 0 var(--avp-edge-row-indent);
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	avp-secondary-controls\[\_382ee1e1\]:first-child:last-child {
	margin-bottom: var(--avp-timeline-block-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-control-bar\[\_382ee1e1\] {
	flex-direction: column;
	width: 100%;
}
@media (prefers-reduced-motion: no-preference) {
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-title-letter\[\_1a96284f\],
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-title-word\[\_1a96284f\] {
		white-space: break-spaces;
	}
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-title-letter.avp-animate\[\_1a96284f\],
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-title-word.avp-animate\[\_1a96284f\] {
		animation-duration: var(--avp-transition-duration);
		animation-fill-mode: forwards;
		animation-timing-function: ease;
	}
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-title-word\[\_1a96284f\] {
		animation-delay: calc(
			var(--avp-index) \* var(--avp-transition-duration) / 4
		);
		display: inline;
	}
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-title-letter\[\_1a96284f\] {
		animation-delay: calc(
			var(--avp-index) \* var(--avp-transition-duration) / 40
		);
		animation-name: fade-in-\_1a96284f;
		animation-timing-function: linear;
		display: inline;
	}
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-title-letter.avp-animate\[\_1a96284f\] {
		opacity: 0;
	}
}
@keyframes move-up-\_1a96284f {
	0% {
		opacity: 0;
		translate: 0 100%;
	}
	to {
		opacity: 1;
		translate: none;
	}
}
@keyframes fade-in-\_1a96284f {
	0% {
		opacity: 0;
	}
	to {
		opacity: 1;
	}
}
@keyframes bounce-\_1a96284f {
	0% {
		transform: translateY(-100%);
	}
	20%,
	50%,
	80%,
	to {
		transform: translateY(0);
	}
	40% {
		transform: translateY(-80%);
	}
	60% {
		transform: translateY(-40%);
	}
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1e0-h\] {
	height: var(--avp-timeline-block-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1e0-h\]
	.avp-chapters\[\_382ee1e0\] {
	flex-direction: row;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1e0-h\]
	avp-timeline-chapter\[\_382ee1e0\] {
	margin-left: var(--avp-timeline-chapter-gap);
	margin-top: calc(var(--avp-timeline-clickable-area-gap) \* -1);
	padding-top: var(--avp-timeline-clickable-area-gap);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1e0-h\]
	avp-timeline-chapter\[\_382ee1e0\]:before {
	height: 100%;
	left: calc(var(--avp-timeline-chapter-gap) \* -1);
	right: 100%;
	top: 0;
	width: var(--avp-timeline-chapter-gap);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1e0-h\]
	avp-timeline-chapter\[\_382ee1e0\]:first-child {
	margin-left: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1e0-h\]
	.avp-time-tooltip\[\_382ee1e0\] {
	bottom: 100%;
	top: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1e0-h\]
	.avp-time-tooltip-content\[\_382ee1e0\] {
	transform: translateY(10%);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-end\[\_382ee1e0-h\] {
	margin: 0 var(--avp-secondary-control-padding);
	width: calc(100% - var(--avp-secondary-control-padding) \* 2);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-hidden
	.avp-horizontal.avp-end\[\_382ee1e0-h\] {
	transform: translateY(var(--avp-secondary-control-size));
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-end\[\_382ee1e0-h\]
	.avp-time-tooltip\[\_382ee1e0\] {
	margin-left: 0;
	margin-right: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-rl
	.avp-chapters\[\_382ee1e0\] {
	flex-direction: row-reverse;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-pointer-container.avp-horizontal\[\_382ee1e0\] {
	bottom: calc(
		(var(--avp-timeline-block-size) - var(--avp-timeline-pointer-size)) / 2
	);
	left: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-pointer-container.avp-horizontal
	.avp-pointer\[\_382ee1e0\] {
	transform: translateX(-50%) scale(0);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-pointer-container.avp-horizontal.avp-visible
	.avp-pointer\[\_382ee1e0\] {
	transform: translateX(-50%) scale(1);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-rl
	avp-timeline-chapter\[\_382ee1e0\] {
	margin-left: var(--avp-timeline-chapter-gap);
	margin-right: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-rl
	avp-timeline-chapter\[\_382ee1e0\]:last-child {
	margin-left: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e0-h\] {
	width: var(--avp-timeline-block-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e0-h\]
	.avp-chapters\[\_382ee1e0\] {
	flex-direction: column-reverse;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e0-h\]
	avp-timeline-chapter\[\_382ee1e0\] {
	margin-bottom: var(--avp-timeline-chapter-gap);
	margin-right: calc(var(--avp-timeline-clickable-area-gap) \* -1);
	padding-right: var(--avp-timeline-clickable-area-gap);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e0-h\]
	avp-timeline-chapter\[\_382ee1e0\]:before {
	bottom: calc(var(--avp-timeline-chapter-gap) \* -1);
	height: var(--avp-timeline-chapter-gap);
	left: 0;
	top: 100%;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e0-h\]
	avp-timeline-chapter\[\_382ee1e0\]:first-child {
	margin-bottom: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e0-h\]
	avp-timeline-chapter:hover
	~ avp-timeline-chapter\[\_382ee1e0\]
	.avp-hover-progress {
	height: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e0-h\]
	.avp-time-tooltip\[\_382ee1e0\] {
	left: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1e0-h\]
	.avp-time-tooltip-content\[\_382ee1e0\] {
	transform: translateX(-10%);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical.avp-end\[\_382ee1e0-h\] {
	height: calc(100% - var(--avp-secondary-control-padding) \* 2);
	margin: var(--avp-secondary-control-padding) 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-hidden
	.avp-vertical.avp-end\[\_382ee1e0-h\] {
	transform: translateX(calc(var(--avp-secondary-control-size) \* -1));
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical.avp-end\[\_382ee1e0-h\]
	.avp-time-tooltip\[\_382ee1e0\] {
	margin-bottom: 0;
	margin-top: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-tb
	.avp-chapters\[\_382ee1e0\] {
	flex-direction: column;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-pointer-container.avp-vertical\[\_382ee1e0\] {
	bottom: auto;
	top: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-pointer-container.avp-vertical
	.avp-pointer\[\_382ee1e0\] {
	transform: translate(calc(var(--avp-timeline-block-size) / -2), -50%) scale(
			0
		);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-pointer-container.avp-vertical.avp-visible
	.avp-pointer\[\_382ee1e0\] {
	transform: translate(calc(var(--avp-timeline-pointer-size) / -4), -50%) scale(
			1
		);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1e0-h\] {
	cursor: pointer;
	flex-shrink: 0;
	pointer-events: auto;
	position: relative;
	touch-action: none;
	transition: var(--avp-transition);
	z-index: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-start\[\_382ee1e0-h\] {
	z-index: 2;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-inert\[\_382ee1e0-h\] {
	pointer-events: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-pointer-container\[\_382ee1e0\] {
	bottom: 0;
	left: 0;
	pointer-events: none;
	position: absolute;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-pointer\[\_382ee1e0\] {
	background-color: var(--avp-brand-color);
	border-radius: 50%;
	box-shadow: 0 0 5px #0006;
	height: var(--avp-timeline-pointer-size);
	opacity: 0;
	transition: var(--avp-transition);
	width: var(--avp-timeline-pointer-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-pointer-container.avp-visible
	.avp-pointer\[\_382ee1e0\] {
	opacity: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-chapters\[\_382ee1e0\] {
	display: flex;
	height: 100%;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-time-tooltip\[\_382ee1e0\] {
	left: 0;
	margin: var(--avp-timeline-block-size);
	pointer-events: none;
	position: absolute;
	top: 0;
	-webkit-user-select: none;
	user-select: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-time-tooltip
	span\[\_382ee1e0\] {
	display: inline-block;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-time-tooltip-content\[\_382ee1e0\] {
	background: #000c;
	border-radius: 3px;
	font-size: 0.8em;
	line-height: normal;
	opacity: 0;
	padding: 4px;
	text-align: center;
	transition: opacity var(--avp-transition-duration), transform var(--avp-transition-duration);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =s\]
	.avp-time-tooltip-content\[\_382ee1e0\] {
	font-size: 1em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =l\]
	.avp-time-tooltip-content\[\_382ee1e0\] {
	font-size: 1.2em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-dragging\[\_382ee1e0-h\]
	.avp-time-tooltip-content\[\_382ee1e0\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1e0-h\]:hover
	.avp-time-tooltip-content\[\_382ee1e0\] {
	opacity: 1;
	transform: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1e0-h\]
	.avp-time-tooltip-content:empty,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[inert\]\[\_382ee1e0-h\]
	.avp-time-tooltip-content\[\_382ee1e0\] {
	opacity: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-horizontal
	.avp-dragging\[\_382ee1ca-h\]
	~ \[\_382ee1ca-h\]
	.avp-hover-progress,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-horizontal
	\[\_382ee1ca-h\]:hover
	~ \[\_382ee1ca-h\]
	.avp-hover-progress {
	width: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-horizontal
	.avp-track\[\_382ee1ca\] {
	height: auto;
	top: var(--avp-timeline-clickable-area-gap);
	transform: scaleY(var(--avp-timeline-minimize-scale-factor));
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-horizontal
	.avp-buffer\[\_382ee1ca\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-horizontal
	.avp-progress\[\_382ee1ca\] {
	transform: scaleX(0);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-vertical
	.avp-track\[\_382ee1ca\] {
	right: var(--avp-timeline-clickable-area-gap);
	transform: scaleX(var(--avp-timeline-minimize-scale-factor));
	width: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-vertical
	.avp-buffer\[\_382ee1ca\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-vertical
	.avp-progress\[\_382ee1ca\] {
	transform: scaleY(0);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1ca\] {
	bottom: 0;
	height: 100%;
	left: 0;
	position: absolute;
	width: 100%;
	z-index: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-horizontal.avp-end
	\[\_382ee1ca\] {
	transform-origin: left center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-horizontal.avp-end.avp-reversed
	\[\_382ee1ca\] {
	transform-origin: right center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-view.avp-hidden
	avp-timeline.avp-horizontal.avp-end
	\[\_382ee1ca\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-horizontal.avp-start
	\[\_382ee1ca\] {
	transform-origin: left bottom;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-view.avp-hidden
	avp-timeline.avp-horizontal.avp-end.avp-reversed
	\[\_382ee1ca\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-horizontal.avp-start.avp-reversed
	\[\_382ee1ca\] {
	transform-origin: right bottom;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-view.avp-hidden
	avp-timeline.avp-vertical.avp-end
	\[\_382ee1ca\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-vertical.avp-start
	\[\_382ee1ca\] {
	transform-origin: top left;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-view.avp-hidden
	avp-timeline.avp-vertical.avp-end.avp-reversed
	\[\_382ee1ca\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-vertical.avp-start.avp-reversed
	\[\_382ee1ca\] {
	transform-origin: bottom left;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-vertical.avp-end
	\[\_382ee1ca\] {
	transform-origin: top center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-vertical.avp-end.avp-reversed
	\[\_382ee1ca\] {
	transform-origin: bottom center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1ca-h\] {
	box-sizing: initial;
	display: block;
	position: relative;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-horizontal
	\[\_382ee1ca-h\] {
	touch-action: pan-x;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-vertical
	\[\_382ee1ca-h\] {
	height: 100%;
	touch-action: pan-y;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1ca-h\]:before {
	content: '';
	display: block;
	pointer-events: auto;
	position: absolute;
	z-index: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1ca-h\]:first-child:before {
	content: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-track\[\_382ee1ca\] {
	background-color: #ffffff40;
	transform-origin: center;
	transition: transform-origin var(--avp-transition-duration), transform var(--avp-transition-duration);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-buffer\[\_382ee1ca\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-hover-progress\[\_382ee1ca\] {
	background-color: #fff6;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-hover-progress\[\_382ee1ca\] {
	display: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-progress\[\_382ee1ca\] {
	background-color: var(--avp-brand-color);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-dragging
	.avp-track\[\_382ee1ca\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline:hover
	.avp-track\[\_382ee1ca\] {
	transform: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline.avp-dragging
	.avp-hover-progress\[\_382ee1ca\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-timeline:hover
	.avp-hover-progress\[\_382ee1ca\] {
	display: block;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1c8-h\] {
	display: flex;
	flex-shrink: 0;
	justify-content: space-between;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary-controls-center\[\_382ee1c8\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary-controls-end\[\_382ee1c8\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary-controls-start\[\_382ee1c8\] {
	cursor: auto;
	display: flex;
	pointer-events: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c8-h\]
	.avp-secondary-controls-center\[\_382ee1c8\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c8-h\]
	.avp-secondary-controls-end\[\_382ee1c8\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c8-h\]
	.avp-secondary-controls-start\[\_382ee1c8\] {
	align-items: flex-end;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c8-h\]
	.avp-secondary-controls-center\[\_382ee1c8\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c8-h\]
	.avp-secondary-controls-end\[\_382ee1c8\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c8-h\]
	.avp-secondary-controls-start\[\_382ee1c8\] {
	flex-direction: column;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary-controls-end\[\_382ee1c8\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary-controls-start\[\_382ee1c8\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-secondary-middle-controls\[\_382ee1c8\] {
	flex-shrink: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary-controls-center\[\_382ee1c8\] {
	flex: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c8-h\]
	.avp-secondary-controls-center\[\_382ee1c8\] {
	justify-content: center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary\[\_382ee18b-h\]
	.avp-default-icon\[\_382ee18b\] {
	stroke-width: 2.5;
	transform: scale(1.14);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-animate-fill-opacity\[\_1a96284b\] {
	fill-opacity: 0.1;
	transition: fill-opacity var(--avp-transition-duration);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-button.avp-active
	.avp-animate-fill-opacity\[\_1a96284b\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-button:hover
	.avp-animate-fill-opacity\[\_1a96284b\] {
	fill-opacity: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary\[\_382ee18a-h\]
	.avp-default-icon\[\_382ee18a\] {
	stroke-width: 2.5;
	transform: scale(1.12);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1c6-h\] {
	display: flex;
	flex-shrink: 0;
	-webkit-user-select: none;
	user-select: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-dragging\[\_382ee1c6-h\]
	avp-icon\[\_382ee1c6\]:first-of-type,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1c6-h\]:hover
	avp-icon\[\_382ee1c6\]:first-of-type {
	opacity: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-dragging\[\_382ee1c6-h\]
	avp-icon\[\_382ee1c6\]:last-of-type,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1c6-h\]:hover
	avp-icon\[\_382ee1c6\]:last-of-type {
	opacity: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c6-h\] {
	height: var(--avp-secondary-control-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c6-h\]
	avp-volume-slider\[\_382ee1c6\] {
	align-items: center;
	transition: width var(--avp-transition-duration) cubic-bezier(0.4, 0, 1, 1);
	width: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c6-h\]
	avp-volume-slider\[\_382ee1c6\]:focus {
	width: var(--avp-volume-slider-inline-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-dragging\[\_382ee1c6-h\]
	avp-volume-slider\[\_382ee1c6\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c6-h\]:hover
	avp-volume-slider\[\_382ee1c6\] {
	transition: width var(--avp-transition-duration) cubic-bezier(0, 0, 0.2, 1);
	width: var(--avp-volume-slider-inline-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c6-h\] {
	flex-direction: column;
	justify-content: flex-end;
	width: var(--avp-secondary-control-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c6-h\]
	.avp-volume-button\[\_382ee1c6\] {
	order: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c6-h\]
	avp-volume-slider\[\_382ee1c6\] {
	align-items: flex-end;
	height: 0;
	justify-content: center;
	transition: height var(--avp-transition-duration) linear;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical.avp-dragging\[\_382ee1c6-h\]
	avp-volume-slider\[\_382ee1c6\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c6-h\]
	avp-volume-slider\[\_382ee1c6\]:focus,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c6-h\]:hover
	avp-volume-slider\[\_382ee1c6\] {
	height: var(--avp-volume-slider-inline-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-volume-button\[\_382ee1c6\] {
	height: var(--avp-secondary-control-size);
	padding: var(--avp-secondary-control-padding);
	position: relative;
	width: var(--avp-secondary-control-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-volume-button\[\_382ee1c6\]:after {
	background: currentColor;
	box-shadow: 1px 1px 2px #0000004d;
	content: '';
	display: block;
	height: 2px;
	left: var(--avp-secondary-control-padding);
	position: absolute;
	top: calc(var(--avp-secondary-control-padding) - 1px);
	transform: rotate(45deg);
	transform-origin: left center;
	transition: width var(--avp-transition-duration);
	width: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-muted
	.avp-volume-button\[\_382ee1c6\]:after {
	width: calc(
		(
				var(--avp-secondary-control-size) -
					(var(--avp-secondary-control-padding) \* 2)
			)
			\* 1.4142
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee1c6\] {
	height: calc(
		var(--avp-secondary-control-size) - var(--avp-secondary-control-padding)
			\* 2
	);
	width: calc(
		var(--avp-secondary-control-size) - var(--avp-secondary-control-padding)
			\* 2
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee1c6\]:first-of-type,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee1c6\]:last-of-type {
	left: 0;
	margin: var(--avp-secondary-control-padding);
	position: absolute;
	top: 0;
	transition: opacity var(--avp-transition-duration);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee1c6\]:first-of-type {
	opacity: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee1c6\]:last-of-type {
	opacity: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1c5-h\] {
	cursor: pointer;
	display: flex;
	margin-left: 0;
	overflow: hidden;
	position: relative;
	z-index: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-muted
	\[\_382ee1c5-h\] {
	color: #fff6;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c5-h\] {
	touch-action: pan-x;
	width: var(--avp-volume-slider-inline-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c5-h\]
	.avp-volume-range\[\_382ee1c5\] {
	height: var(--avp-volume-slider-block-size);
	width: inherit;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c5-h\]
	.avp-volume-range\[\_382ee1c5\]:before {
	height: var(--avp-volume-slider-block-size);
	width: calc(
		var(--avp-volume-slider-volume) \* var(--avp-volume-slider-inline-size)
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee1c5-h\]
	.avp-volume-thumb\[\_382ee1c5\] {
	left: 0;
	top: calc(
		(var(--avp-volume-slider-block-size) - var(--avp-volume-thumb-diameter)) /
			2
	);
	transform: translateX(
		calc(
			var(--avp-volume-slider-volume) \* (var(
							--avp-volume-slider-inline-size
						) - var(--avp-volume-thumb-diameter))
		)
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-muted
	.avp-horizontal\[\_382ee1c5-h\]
	.avp-volume-thumb\[\_382ee1c5\] {
	transform: translateX(0);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c5-h\] {
	height: var(--avp-volume-slider-inline-size);
	touch-action: pan-y;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c5-h\]
	.avp-volume-range\[\_382ee1c5\] {
	height: inherit;
	width: var(--avp-volume-slider-block-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c5-h\]
	.avp-volume-range\[\_382ee1c5\]:before {
	height: calc(
		var(--avp-volume-slider-volume) \* var(--avp-volume-slider-inline-size)
	);
	width: var(--avp-volume-slider-block-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee1c5-h\]
	.avp-volume-thumb\[\_382ee1c5\] {
	bottom: 0;
	left: calc(
		(var(--avp-volume-slider-block-size) - var(--avp-volume-thumb-diameter)) /
			2
	);
	transform: translateY(
		calc(
			var(--avp-volume-slider-volume) \* (var(
							--avp-volume-thumb-diameter
						) - var(--avp-volume-slider-inline-size))
		)
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-muted
	.avp-vertical\[\_382ee1c5-h\]
	.avp-volume-thumb\[\_382ee1c5\] {
	transform: translateY(0);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-volume-range\[\_382ee1c5\] {
	background-color: #fff6;
	border-radius: var(--avp-volume-slider-block-size);
	position: relative;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-volume-range\[\_382ee1c5\]:before {
	background: currentColor;
	border-radius: inherit;
	bottom: 0;
	content: '';
	display: block;
	left: 0;
	position: absolute;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-volume-thumb\[\_382ee1c5\] {
	background-color: #fff;
	border-radius: 50%;
	height: var(--avp-volume-thumb-diameter);
	position: absolute;
	width: var(--avp-volume-thumb-diameter);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_1a962853-h\] {
	--avp-secondary-control-size: calc(
		var(--avp-caption-height) - var(--avp-close-button-overlay-top) - var(--avp-close-button-overlay-bottom)
	);
	--avp-secondary-control-padding: var(--avp-caption-padding);
	align-items: flex-end;
	color: #000;
	display: flex;
	flex: 1;
	overflow: hidden;
	width: var(--avp-view-width);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[data-owner=ad\]\[data-ad-owner=display\]
	\[\_1a962853-h\] {
	background: #737373;
	font-weight: 700;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-playlist-visible
	\[\_1a962853-h\] {
	width: var(--avp-main-width);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom
	\[\_1a962853-h\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-bottom-center
	\[\_1a962853-h\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top
	\[\_1a962853-h\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-fixed.avp-top-center
	\[\_1a962853-h\] {
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_1a962853-h\]
	path {
	stroke-width: 2px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-caption-body\[\_1a962853\] {
	font-size: 12px;
	line-height: var(--avp-caption-height);
	padding: 0 var(--avp-caption-padding);
	white-space: nowrap;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-caption-title\[\_1a962853\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-skip-display-ad-button\[\_1a962853\] {
	display: inline;
	line-height: inherit;
	overflow: hidden;
	text-overflow: ellipsis;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[data-owner=ad\]\[data-ad-owner=display\]
	.avp-caption-title\[\_1a962853\] {
	color: #b9b9b9;
	text-transform: uppercase;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_1a962851-h\] {
	flex-shrink: 0;
	margin: calc(
			var(--avp-close-button-overlay-top) - var(--avp-close-button-overlay-margin)
		) calc(
			var(--avp-close-button-overlay-right) - var(--avp-close-button-overlay-margin)
		)
		calc(
			var(--avp-close-button-overlay-bottom) - var(--avp-close-button-overlay-margin)
		) calc(
			var(--avp-close-button-overlay-left) - var(--avp-close-button-overlay-margin)
		);
	padding: var(--avp-close-button-overlay-margin);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee14d-h\] {
	height: 100%;
	left: 0;
	pointer-events: none;
	position: absolute;
	top: 0;
	visibility: hidden;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active\[\_382ee14d-h\] {
	visibility: inherit;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	img\[\_382ee14d\] {
	height: 100%;
	object-fit: cover;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee149-h\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	video\[\_382ee149\] {
	height: 100%;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee149-h\] {
	background: #000;
	left: 0;
	overflow: hidden;
	position: absolute;
	top: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee148-h\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	video\[\_382ee148\] {
	height: 100%;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee148-h\] {
	left: 0;
	overflow: hidden;
	position: absolute;
	top: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee14c-h\] {
	flex-direction: column;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-inside\[\_382ee14c-h\] {
	padding: 0 calc(var(--avp-secondary-control-padding) + var(--avp-edge-row-indent));
	z-index: 3;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-inside.avp-scrollable\[\_382ee14c-h\] {
	padding: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-outside\[\_382ee14c-h\] {
	width: var(--avp-view-width);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-outside.avp-start\[\_382ee14c-h\]
	avp-carousel\[\_382ee14c\] {
	margin-bottom: var(--avp-carousel-item-gap);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-outside.avp-end\[\_382ee14c-h\]
	avp-carousel\[\_382ee14c\] {
	margin-top: var(--avp-carousel-item-gap);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14c-h\] {
	flex-direction: row;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical.avp-inside\[\_382ee14c-h\] {
	padding: var(--avp-edge-column-indent) 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical.avp-inside.avp-scrollable\[\_382ee14c-h\] {
	padding: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical.avp-outside\[\_382ee14c-h\] {
	height: var(--avp-view-height);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical.avp-outside.avp-start\[\_382ee14c-h\]
	avp-carousel\[\_382ee14c\] {
	margin-right: var(--avp-carousel-item-gap);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical.avp-outside.avp-end\[\_382ee14c-h\]
	avp-carousel\[\_382ee14c\] {
	margin-left: var(--avp-carousel-item-gap);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee14c-h\] {
	--avp-transition-move-value: 50%;
	display: flex;
	flex-shrink: 0;
	pointer-events: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-outside\[\_382ee14c-h\] {
	background-color: var(--avp-playlist-background-color);
	overflow: hidden;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-outside\[\_382ee14c-h\]
	avp-carousel\[\_382ee14c\] {
	margin: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-carousel\[\_382ee14c\] {
	flex: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee14b-h\] {
	height: var(--avp-carousel-view-block-size);
	margin: var(--avp-carousel-item-gap) 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee14b-h\]
	.avp-next-button\[\_382ee14b\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee14b-h\]
	.avp-prev-button\[\_382ee14b\] {
	height: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee14b-h\]
	.avp-prev-button\[\_382ee14b\] {
	background: radial-gradient(
		at 100% 50%,
		var(--avp-carousel-button-background-color, #0000),
		#0000
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee14b-h\]
	.avp-next-button\[\_382ee14b\] {
	background: radial-gradient(
		at 0 50%,
		var(--avp-carousel-button-background-color, #0000),
		#0000
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee14b-h\]
	avp-carousel-item\[\_382ee14b\] {
	margin-left: var(--avp-carousel-item-gap);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal\[\_382ee14b-h\]
	avp-carousel-item\[\_382ee14b\]:first-of-type {
	margin-left: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-compact\[\_382ee14b-h\]
	.avp-prev-button\[\_382ee14b\] {
	margin-right: calc(var(--avp-carousel-prev-next-control-inline-size) \* -1);
	transform: translateX(-100%);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal.avp-compact\[\_382ee14b-h\]
	.avp-next-button\[\_382ee14b\] {
	margin-left: calc(var(--avp-carousel-prev-next-control-inline-size) \* -1);
	transform: translateX(100%);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\]
	.avp-items\[\_382ee14b\] {
	flex-direction: column;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\] {
	margin: 0 var(--avp-carousel-item-gap);
	width: var(--avp-carousel-view-block-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\]
	.avp-next-button\[\_382ee14b\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\]
	.avp-prev-button\[\_382ee14b\] {
	width: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\]
	.avp-next-button
	avp-icon\[\_382ee14b\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\]
	.avp-prev-button
	avp-icon\[\_382ee14b\] {
	transform: rotate(90deg);
	transform-origin: center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\]
	.avp-prev-button\[\_382ee14b\] {
	background: radial-gradient(
		at 50% 100%,
		var(--avp-carousel-button-background-color, #0000),
		#0000
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\]
	.avp-next-button\[\_382ee14b\] {
	background: radial-gradient(
		at 50% 0,
		var(--avp-carousel-button-background-color, #0000),
		#0000
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\]
	avp-carousel-item\[\_382ee14b\] {
	margin-top: var(--avp-carousel-item-gap);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical\[\_382ee14b-h\]
	avp-carousel-item\[\_382ee14b\]:first-of-type {
	margin-top: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical.avp-compact\[\_382ee14b-h\]
	.avp-prev-button\[\_382ee14b\] {
	margin-bottom: calc(
		var(--avp-carousel-prev-next-control-inline-size) \* -1
	);
	transform: translateY(-100%);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical.avp-compact\[\_382ee14b-h\]
	.avp-next-button\[\_382ee14b\] {
	margin-top: calc(var(--avp-carousel-prev-next-control-inline-size) \* -1);
	transform: translateY(100%);
}
@property --avp-carousel-button-background-color {
	syntax: '<color>';
	inherits: true;
	initial-value: #0000;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-view\[\_382ee14b\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee14b-h\] {
	flex: 1;
	touch-action: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee14b-h\] {
	display: flex;
	justify-content: center;
	overflow: hidden;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-compact\[\_382ee14b-h\] {
	border-radius: var(--avp-border-radius);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scrollable\[\_382ee14b-h\] {
	margin-left: 0;
	margin-right: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-disabled\[\_382ee14b-h\] {
	filter: grayscale(1);
	pointer-events: none;
}
@media (hover: hover) {
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-compact\[\_382ee14b-h\]:hover
		.avp-next-button\[\_382ee14b\],
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		.avp-compact\[\_382ee14b-h\]:hover
		.avp-prev-button\[\_382ee14b\] {
		transform: none;
	}
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-view\[\_382ee14b\] {
	overflow: auto;
	overscroll-behavior: contain;
	position: relative;
	-webkit-user-select: none;
	user-select: none;
	z-index: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal
	.avp-view.avp-scroll-snap\[\_382ee14b\] {
	scroll-snap-type: x mandatory;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical
	.avp-view.avp-scroll-snap\[\_382ee14b\] {
	scroll-snap-type: y mandatory;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-view.avp-scroll-snap
	avp-carousel-item\[\_382ee14b\] {
	scroll-snap-align: start;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-items\[\_382ee14b\] {
	display: flex;
	flex: 1 var(--avp-carousel-view-inline-size);
	height: 100%;
	justify-content: center;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scrollable
	.avp-items\[\_382ee14b\] {
	justify-content: flex-start;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical
	.avp-items\[\_382ee14b\] {
	touch-action: pan-y;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal
	.avp-items\[\_382ee14b\] {
	touch-action: pan-x;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-next-button\[\_382ee14b\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-prev-button\[\_382ee14b\] {
	--avp-carousel-button-background-color: #00000040;
	background: var(--avp-carousel-button-background-color, #0000);
	border: none;
	cursor: pointer;
	display: none;
	flex: 0 0 var(--avp-carousel-prev-next-control-inline-size);
	outline: none;
	padding: 0;
	position: relative;
	transition: --avp-carousel-button-background-color var(--avp-transition-duration),
		background var(--avp-transition-duration),
		transform var(--avp-transition-duration), opacity var(--avp-transition-duration);
	z-index: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scrollable
	.avp-next-button\[\_382ee14b\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-scrollable
	.avp-prev-button\[\_382ee14b\] {
	display: block;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-next-button\[\_382ee14b\]:hover,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-prev-button\[\_382ee14b\]:hover {
	--avp-carousel-button-background-color: #00000080;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-next-button
	div\[\_382ee14b\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-prev-button
	div\[\_382ee14b\] {
	align-items: center;
	display: flex;
	height: 100%;
	justify-content: center;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-compact\[\_382ee14b-h\]
	.avp-next-button\[\_382ee14b\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-compact\[\_382ee14b-h\]
	.avp-prev-button\[\_382ee14b\] {
	background: #000;
	opacity: 0.5;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-compact\[\_382ee14b-h\]
	.avp-next-button\[\_382ee14b\]:hover,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-compact\[\_382ee14b-h\]
	.avp-prev-button\[\_382ee14b\]:hover {
	background: #000c;
	opacity: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee14b\] {
	height: 50%;
	width: 50%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee14a-h\] {
	--avp-carousel-item-inline-size: calc(
		(
				var(--avp-carousel-view-inline-size) - var(
						--avp-carousel-item-gap
					) \* (var(--avp-carousel-items-per-page) - 1)
			) / var(--avp-carousel-items-per-page)
	);
	align-items: flex-end;
	border: 1px solid #0000;
	border-radius: var(--avp-border-radius);
	cursor: pointer;
	display: flex;
	flex: 0 0 var(--avp-carousel-item-inline-size);
	overflow: hidden;
	position: relative;
	transition: border-color var(--avp-transition-duration);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-horizontal
	\[\_382ee14a-h\] {
	height: var(--avp-carousel-view-block-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-vertical
	\[\_382ee14a-h\] {
	width: var(--avp-carousel-view-block-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active\[\_382ee14a-h\] {
	border-color: #ffffffbf;
	cursor: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active-text\[\_382ee14a\] {
	align-items: center;
	background: #00000059;
	display: flex;
	font-size: 14px;
	height: 100%;
	justify-content: center;
	left: 0;
	padding: 10px;
	position: absolute;
	text-align: center;
	top: 0;
	width: 100%;
	z-index: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =l\]
	.avp-active-text\[\_382ee14a\] {
	font-size: 18px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xl\]
	.avp-active-text\[\_382ee14a\] {
	font-size: 20px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-image\[\_382ee14a\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee14a\] {
	bottom: 0;
	height: 100%;
	left: 0;
	pointer-events: none;
	position: absolute;
	right: 0;
	top: 0;
	transition: transform var(--avp-transition-duration);
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee14a-h\]:hover
	.avp-image\[\_382ee14a\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee14a-h\]:hover
	avp-icon\[\_382ee14a\] {
	transform: scale(1.1);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active\[\_382ee14a-h\]
	.avp-image\[\_382ee14a\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active\[\_382ee14a-h\]
	avp-icon\[\_382ee14a\] {
	transform: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee14a\] {
	background: currentColor;
	background: linear-gradient(135deg, currentColor, #0000);
	color: var(--avp-carousel-item-placeholder-image-background);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-image\[\_382ee14a\] {
	background-position: 50%;
	background-size: cover;
	object-fit: cover;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-duration\[\_382ee14a\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-title\[\_382ee14a\] {
	background: #000c;
	font-size: 0.75em;
	transition: var(--avp-transition);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =l\]
	.avp-duration\[\_382ee14a\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =l\]
	.avp-title\[\_382ee14a\] {
	font-size: 1em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xl\]
	.avp-duration\[\_382ee14a\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xl\]
	.avp-title\[\_382ee14a\] {
	font-size: 1.2em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active
	.avp-duration\[\_382ee14a\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active
	.avp-title\[\_382ee14a\] {
	opacity: 0;
	pointer-events: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-title\[\_382ee14a\] {
	line-height: 22px;
	overflow: hidden;
	padding: 0 8px;
	position: relative;
	text-align: center;
	text-overflow: ellipsis;
	white-space: nowrap;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	.avp-title\[\_382ee14a\] {
	line-height: 24px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =l\]
	.avp-title\[\_382ee14a\] {
	line-height: 30px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xl\]
	.avp-title\[\_382ee14a\] {
	line-height: 34px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-duration\[\_382ee14a\] {
	border-radius: var(--avp-border-radius);
	margin: 4px;
	padding: 3px 4px;
	position: absolute;
	right: 0;
	top: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =l\]
	.avp-duration\[\_382ee14a\] {
	padding: 4px 6px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1a4-h\] {
	align-items: center;
	display: flex;
	flex-shrink: 0;
	justify-content: center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a4-h\]
	> :first-child:nth-last-child(3),
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a4-h\]
	> :nth-child(2):nth-last-child(4) {
	--avp-transition-scale-value: calc(
		1.5 + var(--avp-primary-control-transition-bend)
	);
	transform-origin: calc(
		50% + 50%\* var(--avp-primary-control-transform-origin-bend)
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a4-h\]
	> :last-child:nth-child(3),
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a4-h\]
	> :nth-last-child(2):nth-child(4) {
	--avp-transition-scale-value: calc(
		1.5 + var(--avp-primary-control-transition-bend)
	);
	transform-origin: calc(
		50% - 50%\* var(--avp-primary-control-transform-origin-bend)
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a4-h\]
	> :first-child:nth-last-child(5) {
	transform-origin: calc(
		50% + 150%\* var(--avp-primary-control-transform-origin-bend)
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a4-h\]
	> :first-child:nth-last-child(5),
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a4-h\]
	> :last-child:nth-child(5) {
	--avp-transition-scale-value: calc(
		1.5 + var(--avp-primary-control-transition-bend) \* 2
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a4-h\]
	> :last-child:nth-child(5) {
	transform-origin: calc(
		50% - 150%\* var(--avp-primary-control-transform-origin-bend)
	);
}
@supports (display: grid) {
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		\[\_382ee1a4-h\] {
		display: grid;
		grid-template-columns: repeat(
				2,
				minmax(var(--avp-primary-control-size), 100%)
			) minmax(var(--avp-primary-middle-control-size), 100%) repeat(2, minmax(var(--avp-primary-control-size), 100%));
		justify-items: center;
		margin: 0 var(--avp-primary-control-padding);
	}
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		\[w
		~ =xs\]
		\[\_382ee1a4-h\] {
		grid-template-columns: repeat(
				2,
				minmax(
					var(--avp-primary-control-size),
					calc(
						var(--avp-primary-control-size) \* (1 + var(--avp-primary-control-max-size-factor))
					)
				)
			) minmax(
				var(--avp-primary-middle-control-size),
				calc(
					var(--avp-primary-middle-control-size) + var(
							--avp-primary-control-size
						) \* var(--avp-primary-control-max-size-factor)
				)
			) repeat(2, minmax(var(--avp-primary-control-size), calc(var(
								--avp-primary-control-size
							) \* (1 + var(--avp-primary-control-max-size-factor)))));
	}
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		avp-fast-backward-button\[\_382ee1a4\] {
		grid-column: 1;
	}
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		avp-prev-button\[\_382ee1a4\] {
		grid-column: 2;
	}
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		avp-primary-middle-controls\[\_382ee1a4\] {
		grid-column: 3;
	}
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		avp-next-button\[\_382ee1a4\] {
		grid-column: 4;
	}
	#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
		avp-fast-forward-button\[\_382ee1a4\] {
		grid-column: 5;
	}
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee186-h\] {
	position: relative;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-x-sec-value\[\_382ee186\] {
	font-size: 12px;
	font-weight: 600;
	left: 50%;
	position: absolute;
	top: 50%;
	transform: translate(-50%, -50%);
	-webkit-user-select: none;
	user-select: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary
	.avp-x-sec-value\[\_382ee186\] {
	font-size: 10px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-primary\[\_382ee189-h\]
	.avp-default-icon\[\_382ee189\] {
	stroke-width: 1.5;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary\[\_382ee189-h\]
	.avp-default-icon\[\_382ee189\] {
	stroke-width: 2.5;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1a3-h\] {
	flex-shrink: 0;
	height: var(--avp-primary-middle-control-size);
	width: var(--avp-primary-middle-control-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a3-h\]
	.avp-button.avp-primary {
	height: 100%;
	padding: var(--avp-primary-middle-control-padding);
	width: 100%;
	z-index: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1a2-h\] {
	height: var(--avp-primary-middle-control-size);
	padding: var(--avp-primary-middle-control-padding);
	pointer-events: none;
	width: var(--avp-primary-middle-control-size);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	svg\[\_382ee1a2\] {
	fill: none;
	stroke-width: 4;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	svg
	circle\[\_382ee1a2\] {
	transform-origin: center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	svg
	circle\[\_382ee1a2\]:first-of-type {
	stroke: #fff3;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	svg
	circle\[\_382ee1a2\]:last-of-type {
	stroke: #fff;
	stroke-linecap: round;
	animation: spin-dash-\_382ee1a21.5s ease-in-out infinite, spin-rotate-\_382ee1a22s
			linear infinite;
}
@keyframes spin-dash-\_382ee1a2 {
	0% {
		stroke-dasharray: 1, 150;
		stroke-dashoffset: 0;
	}
	50% {
		stroke-dasharray: 90, 150;
		stroke-dashoffset: -35;
	}
	to {
		stroke-dasharray: 90, 150;
		stroke-dashoffset: -124;
	}
}
@keyframes spin-rotate-\_382ee1a2 {
	0% {
		transform: rotate(0);
	}
	to {
		transform: rotate(1turn);
	}
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-primary\[\_382ee188-h\]
	.avp-default-icon\[\_382ee188\] {
	stroke-width: 1.5;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary\[\_382ee188-h\]
	.avp-default-icon\[\_382ee188\] {
	stroke-width: 2.5;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee187-h\] {
	position: relative;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-x-sec-value\[\_382ee187\] {
	font-size: 12px;
	font-weight: 600;
	left: 50%;
	position: absolute;
	top: 50%;
	transform: translate(-50%, -50%);
	-webkit-user-select: none;
	user-select: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-secondary
	.avp-x-sec-value\[\_382ee187\] {
	font-size: 10px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1c2-h\] {
	position: relative;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active\[\_382ee1c2-h\]
	avp-icon\[\_382ee1c2\]:first-of-type,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active\[\_382ee1c2-h\]
	avp-icon\[\_382ee1c2\]:last-of-type {
	transform: rotate(30deg);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active\[\_382ee1c2-h\]
	avp-icon\[\_382ee1c2\]:first-of-type {
	opacity: 0;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-active\[\_382ee1c2-h\]
	avp-icon\[\_382ee1c2\]:last-of-type {
	opacity: 1;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-hd-quality-badge\[\_382ee1c2-h\]:after {
	background: red;
	border-radius: 1px;
	color: #fff;
	content: 'HD';
	font-family: Verdana, sans-serif;
	font-size: 7px;
	font-weight: 700;
	height: 9px;
	line-height: 1.4;
	position: absolute;
	right: 5px;
	text-align: center;
	top: 10px;
	width: 13px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =l\]
	.avp-hd-quality-badge\[\_382ee1c2-h\]:after {
	border-radius: 1.5px;
	font-size: 10px;
	height: auto;
	line-height: normal;
	padding: 2px;
	right: 6px;
	text-shadow: 0 2px 0 #0009;
	top: 15px;
	width: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee1c2\]:first-of-type,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee1c2\]:last-of-type {
	transform: translateZ(0);
	transition: transform var(--avp-transition-duration), opacity var(--avp-transition-duration);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	avp-icon\[\_382ee1c2\]:last-of-type {
	height: calc(
		var(--avp-secondary-control-size) - var(--avp-secondary-control-padding)
			\* 2
	);
	left: var(--avp-secondary-control-padding);
	opacity: 0;
	position: absolute;
	top: var(--avp-secondary-control-padding);
	width: calc(
		var(--avp-secondary-control-size) - var(--avp-secondary-control-padding)
			\* 2
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1c1-h\] {
	align-items: flex-end;
	bottom: 0;
	display: flex;
	font-size: 16px;
	justify-content: flex-end;
	left: 0;
	pointer-events: auto;
	position: absolute;
	right: 0;
	z-index: 6;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	\[\_382ee1c1-h\] {
	left: auto;
	right: calc(
		var(--avp-secondary-control-padding) + var(--avp-edge-row-indent)
	);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =l\]
	\[\_382ee1c1-h\] {
	font-size: 20px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a9-h\]\[\_382ee1a9\]::-webkit-scrollbar-thumb,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a9-h\]\[\_382ee1a9\]::-webkit-scrollbar-track {
	background-color: initial;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a9-h\]\[\_382ee1a9\]::-webkit-scrollbar-corner {
	background-color: initial;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1a9-h\] {
	bottom: 0;
	display: flex;
	flex-direction: column;
	max-height: calc(var(--avp-view-height) - var(--avp-bottom-height));
	overflow-y: auto;
	position: absolute;
	right: 0;
	scrollbar-color: auto;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	\[\_382ee1a9-h\] {
	border-radius: var(--avp-border-radius);
	width: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a9-h\]::-webkit-scrollbar {
	height: 4px;
	width: 4px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a9-h\]::-webkit-scrollbar-thumb {
	background: #ffffff4d;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a9-h\]::-webkit-scrollbar-track {
	background: #000000bf;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1a7-h\] {
	background-color: #000000bf;
	border-top: 1px solid #2e2e2ebf;
	cursor: pointer;
	display: flex;
	flex-shrink: 0;
	justify-content: space-between;
	padding: 0.75em;
	position: relative;
	-webkit-user-select: none;
	user-select: none;
	white-space: nowrap;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1a7-h\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a7-h\]:after {
	transition: background-color var(--avp-transition-duration);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a7-h\]:after {
	background-color: initial;
	bottom: 0;
	content: '';
	left: 0;
	position: absolute;
	top: 0;
	width: 0.125em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a7-h\]:first-of-type {
	border-top: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a7-h\]:hover {
	background-color: #2e2e2ebf;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a7-h\]:hover:after {
	background-color: var(--avp-brand-color);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a7-h\].avp-disabled {
	color: #fff9;
	pointer-events: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-left\[\_382ee1a7\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-right\[\_382ee1a7\] {
	align-items: center;
	display: flex;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-right\[\_382ee1a7\] {
	margin-left: 1em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-icon-left\[\_382ee1a7\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-icon-right\[\_382ee1a7\] {
	display: flex;
	flex-shrink: 0;
	height: 1em;
	width: 1em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-icon-left
	avp-icon\[\_382ee1a7\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-icon-right
	avp-icon\[\_382ee1a7\] {
	fill: currentColor;
	stroke: currentColor;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-icon-left\[\_382ee1a7\] {
	margin-left: 0.25em;
	margin-right: 0.75em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-icon-right\[\_382ee1a7\] {
	margin-left: 0.5em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-secondary-title\[\_382ee1a7\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-selected-secondary\[\_382ee1a7\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-selected\[\_382ee1a7\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-title\[\_382ee1a7\] {
	font-size: 0.75em;
	line-height: 1em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-selected\[\_382ee1a7\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-title\[\_382ee1a7\] {
	overflow: hidden;
	text-overflow: ellipsis;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-secondary-title\[\_382ee1a7\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-selected-secondary\[\_382ee1a7\] {
	color: #fff9;
	margin-left: 0.25em;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-secondary-title\[\_382ee1a7\]:empty,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-item-selected-secondary\[\_382ee1a7\]:empty {
	display: none;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1ab-h\]\[\_382ee1ab\]::-webkit-scrollbar-thumb,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1ab-h\]\[\_382ee1ab\]::-webkit-scrollbar-track {
	background-color: initial;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1ab-h\]\[\_382ee1ab\]::-webkit-scrollbar-corner {
	background-color: initial;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1ab-h\] {
	bottom: 0;
	display: flex;
	flex-direction: column;
	max-height: calc(var(--avp-view-height) - var(--avp-bottom-height));
	overflow-y: auto;
	position: absolute;
	right: 0;
	scrollbar-color: auto;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	\[\_382ee1ab-h\] {
	border-radius: var(--avp-border-radius);
	width: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1ab-h\]::-webkit-scrollbar {
	height: 4px;
	width: 4px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1ab-h\]::-webkit-scrollbar-thumb {
	background: #ffffff4d;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1ab-h\]::-webkit-scrollbar-track {
	background: #000000bf;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a8-h\]\[\_382ee1a8\]::-webkit-scrollbar-thumb,
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a8-h\]\[\_382ee1a8\]::-webkit-scrollbar-track {
	background-color: initial;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a8-h\]\[\_382ee1a8\]::-webkit-scrollbar-corner {
	background-color: initial;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1a8-h\] {
	bottom: 0;
	display: flex;
	flex-direction: column;
	max-height: calc(var(--avp-view-height) - var(--avp-bottom-height));
	overflow-y: auto;
	position: absolute;
	right: 0;
	scrollbar-color: auto;
	width: 100%;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	\[\_382ee1a8-h\] {
	border-radius: var(--avp-border-radius);
	width: auto;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a8-h\]::-webkit-scrollbar {
	height: 4px;
	width: 4px;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a8-h\]::-webkit-scrollbar-thumb {
	background: #ffffff4d;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[\_382ee1a8-h\]::-webkit-scrollbar-track {
	background: #000000bf;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#) \[\_382ee1c3-h\] {
	align-items: center;
	display: flex;
	flex-shrink: 0;
	font-size: 12px;
	height: var(--avp-secondary-control-size);
	justify-content: center;
	padding: 0 var(--avp-secondary-control-padding);
	pointer-events: auto;
	white-space: nowrap;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xxs\]
	\[\_382ee1c3-h\] {
	font-size: calc(var(--avp-secondary-control-size) \* 0.325);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	\[w
	~ =xs\]
	\[\_382ee1c3-h\] {
	font-size: calc(var(--avp-secondary-control-size) \* 0.381);
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-bound-time-left\[\_382ee1c3\],
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-bound-time-right\[\_382ee1c3\] {
	text-align: center;
}
#aniplayer_AV643fa7d1a678bff9f906ba97-1714177690017:not(#\\#)
	.avp-time-separator\[\_382ee1c3\] {
	text-align: center;
	width: 2ch;
}
```

Top VS Code Extensions for Web Developer in 2024!! GeeksforGeeks

55

Playback speed

1x Normal

Quality

Auto

Back

360p

240p

144p

Auto

Back

0.25x

0.5x

1x Normal

1.5x

2x

/

![](https://content1.avplayer.com/63f61879c01d725811007616/videos/66055a389f59458c0c088b72/6b3bcbf4-fbef-48ca-ba0d-4a3b87474fd4.webp)

```css
#nonl-container \* {
	display: block;
}
#av-caption #av-close-btn:hover,
#av-container #av-inner #gui #av-close-btn:hover,
#av-container.av-desktop #av-inner #gui #close-btn:hover,
#av-container.av-desktop #av-inner #gui #skip-btn:hover {
	background-color: #000;
	background-color: rgba(0, 0, 0, 0.7);
	cursor: pointer;
}
#av-caption #av-close-btn,
#av-container #av-inner #gui #av-close-btn,
#av-container #av-inner #gui #close-btn {
	background-color: #323232;
	background-color: rgba(0, 0, 0, 0.4);
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27%23fff%27 fill-rule=%27evenodd%27 d=%27m19.346 5.421-2.09-2.089-5.918 5.918L5.42 3.332 3.332 5.421l5.918 5.917-5.918 5.919 2.088 2.088 5.918-5.918 5.918 5.918 2.09-2.088-5.918-5.919z%27 clip-rule=%27evenodd%27/%3E%3C/svg%3E');
	background-position: 50%;
	background-repeat: no-repeat;
	background-size: 60%;
	border-color: #fff;
	border-style: solid;
	border-width: 0 1px 1px 0;
	height: 28px;
	left: 0;
	position: absolute;
	top: 0;
	-webkit-transition: all 0.15s ease-in-out;
	-moz-transition: all 0.15s ease-in-out;
	-o-transition: all 0.15s ease-in-out;
	transition: all 0.15s ease-in-out;
	width: 28px;
	z-index: 9999999;
}
#av-caption #av-close-btn,
#av-container #av-inner #gui #av-close-btn {
	border: none;
	height: 18px;
	position: static;
	width: 18px;
}
#av-caption {
	line-height: 18px;
	position: relative;
	text-align: center;
}
#av-caption #av-close-btn-overlay {
	display: inline-block;
	position: relative;
	vertical-align: top;
	z-index: 9999999;
}
#av-label {
	color: #bbb;
	display: inline-block;
	font-family: Helvetica, Arial, fallback, sans-serif;
	font-size: 9px;
	line-height: 10px;
	margin: 0;
	padding: 4px;
	text-align: center;
	text-transform: uppercase;
	vertical-align: top;
	z-index: 83;
}
#av-container {
	height: 360px;
	margin: 0;
	overflow: hidden;
	pointer-events: auto;
	position: relative;
	text-align: initial;
	width: 640px;
}
#av-container ::-webkit-media-controls-panel {
	-webkit-appearance: none;
	display: none !important;
}
#av-container ::--webkit-media-controls-play-button {
	-webkit-appearance: none;
	display: none !important;
}
#av-container ::-webkit-media-controls-start-playback-button {
	-webkit-appearance: none;
	display: none !important;
}
#av-container div {
	position: static;
}
#av-container #av-inner {
	height: 100%;
	left: 0;
	position: absolute;
	top: 0;
	width: 100%;
}
#av-container #av-inner #slot {
	-webkit-box-shadow: inset 0 0 0 1px rgba(0, 0, 0, 0.1);
	-moz-box-shadow: inset 0 0 0 1px rgba(0, 0, 0, 0.1);
	box-shadow: inset 0 0 0 1px rgba(0, 0, 0, 0.1);
	height: 100%;
	position: absolute;
	width: 100%;
}
#av-container #av-inner #slot #preloader {
	bottom: 0;
	height: 0;
	left: 0;
	margin: auto;
	outline: none;
	position: absolute;
	right: 0;
	top: 0;
	width: 0;
}
#av-container #av-inner #slot #preloader svg {
	left: 50%;
	position: absolute;
	top: 50%;
}
#av-container #av-inner #slot #preloader svg.avicon {
	fill: #fff;
	height: 50px;
	margin-left: -25px;
	margin-top: -25px;
	width: 50px;
}
#av-container #av-inner #slot #preloader svg.avcircle {
	fill: transparent;
	stroke: hsla(0, 0%, 100%, 0.2);
	stroke-width: 3;
	height: 70px;
	margin-left: -35px;
	margin-top: -35px;
	width: 70px;
}
#av-container #av-inner #slot #preloader svg.avcircle.active {
	stroke: #fff;
	stroke-linecap: round;
	animation: av-loading-dash 2s ease infinite, av-loading-rotate 2.5s linear
			infinite;
	color: red;
}
#av-container #av-inner #slot #videoslot {
	bottom: 0;
	filter: alpha(opacity=0);
	left: 0;
	object-fit: fill;
	opacity: 0;
	position: absolute;
	right: 0;
	text-align: left;
	top: 50%;
	-webkit-transform: translateY(-50%);
	-ms-transform: translateY(-50%);
	transform: translateY(-50%);
	width: 100%;
}
#av-container #av-inner #slot #videoslot.loaded {
	-webkit-animation: fade-in 0.5s ease;
	-moz-animation: fade-in 0.5s ease;
	-o-animation: fade-in 0.5s ease;
	animation: fade-in 0.5s ease;
	filter: alpha(opacity=100);
	opacity: 1;
}
#av-container #av-inner #slot #videoslot div {
	all: initial;
	background: initial;
	position: static;
	z-index: auto;
}
#av-container #av-inner #gui:before {
	background: -webkit-linear-gradient(top, transparent, rgba(0, 0, 0, 0.5));
	background: -moz-linear-gradient(
		top,
		transparent 0,
		rgba(0, 0, 0, 0.5) 100%
	);
	background: linear-gradient(180deg, transparent 0, rgba(0, 0, 0, 0.5));
	bottom: 0;
	content: '';
	filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#00000000",endColorstr="#80000000",GradientType=0);
	height: 15%;
	left: 0;
	pointer-events: none;
	width: 100%;
}
#av-container #av-inner #gui #timeline,
#av-container #av-inner #gui:before {
	position: absolute;
	-webkit-transition: all 0.15s ease-in-out;
	-moz-transition: all 0.15s ease-in-out;
	-o-transition: all 0.15s ease-in-out;
	transition: all 0.15s ease-in-out;
}
#av-container #av-inner #gui #timeline {
	cursor: pointer;
	height: 10px;
	overflow: hidden;
}
#av-container #av-inner #gui #timeline #timeline-buffer,
#av-container #av-inner #gui #timeline #timeline-moveto,
#av-container #av-inner #gui #timeline #timeline-progress,
#av-container #av-inner #gui #timeline:before {
	height: 2px;
	left: 0;
	position: absolute;
}
#av-container #av-inner #gui #timeline:before {
	background: #646464;
	background: hsla(0, 0%, 100%, 0.3);
	content: '';
	width: 100%;
}
#av-container #av-inner #gui #timeline #timeline-buffer,
#av-container #av-inner #gui #timeline:before {
	-webkit-box-shadow: 0 0 3px 0 rgba(0, 0, 0, 0.1);
	-moz-box-shadow: 0 0 3px 0 rgba(0, 0, 0, 0.1);
	box-shadow: 0 0 3px 0 rgba(0, 0, 0, 0.1);
}
#av-container #av-inner #gui #timeline #timeline-buffer {
	background: #b4b4b4;
	background: hsla(0, 0%, 100%, 0.5);
	width: 0;
}
#av-container #av-inner #gui #timeline #timeline-moveto {
	background: #fff;
	background: hsla(0, 0%, 100%, 0.8);
	opacity: 0;
	width: 0;
}
#av-container #av-inner #gui #timeline #timeline-progress {
	background: red;
	width: 0;
}
#av-container #av-inner #gui #timeline.av-overlay {
	bottom: 41px;
	left: 10px;
	right: 10px;
}
#av-container #av-inner #gui #timeline.av-overlay #timeline-buffer,
#av-container #av-inner #gui #timeline.av-overlay #timeline-moveto,
#av-container #av-inner #gui #timeline.av-overlay #timeline-progress,
#av-container #av-inner #gui #timeline.av-overlay:before {
	margin-top: -1px;
	top: 50%;
}
#av-container #av-inner #gui #timeline.av-bottom {
	bottom: 0;
	left: 0;
	right: 0;
}
#av-container #av-inner #gui #timeline.av-bottom #timeline-buffer,
#av-container #av-inner #gui #timeline.av-bottom #timeline-moveto,
#av-container #av-inner #gui #timeline.av-bottom #timeline-progress,
#av-container #av-inner #gui #timeline.av-bottom:before {
	bottom: 0;
	top: auto;
}
#av-container #av-inner #gui #timeline.av-top {
	left: 0;
	right: 0;
	top: 0;
}
#av-container #av-inner #gui #timeline.av-top #timeline-buffer,
#av-container #av-inner #gui #timeline.av-top #timeline-moveto,
#av-container #av-inner #gui #timeline.av-top #timeline-progress,
#av-container #av-inner #gui #timeline.av-top:before {
	bottom: auto;
	top: 0;
}
#av-container #av-inner #gui #timeline.av-top ~ #skip-btn {
	top: 2px;
}
#av-container #av-inner #gui #timeline.av-top ~ #aniview-credit {
	top: 4px;
}
#av-container #av-inner #gui #timeline.av-none {
	display: none !important;
	opacity: 0 !important;
}
#av-container #av-inner #gui #buttons {
	bottom: 0;
	display: flex;
	justify-content: space-between;
	left: 0;
	padding: 0 13px 11px;
	position: absolute;
	right: 0;
	-webkit-transition: all 0.15s ease-in-out;
	-moz-transition: all 0.15s ease-in-out;
	-o-transition: all 0.15s ease-in-out;
	transition: all 0.15s ease-in-out;
}
#av-container #av-inner #gui #buttons.av-left {
	justify-content: flex-start;
	right: auto;
}
#av-container #av-inner #gui #buttons.av-left #play-pause {
	margin-right: 0;
}
#av-container #av-inner #gui #buttons #play-pause:after,
#av-container #av-inner #gui #buttons #sound:after {
	bottom: -10px;
	content: '';
	left: -10px;
	position: absolute;
	right: -10px;
	top: -10px;
}
#av-container #av-inner #gui #buttons #fullscreen,
#av-container #av-inner #gui #buttons #phone,
#av-container #av-inner #gui #buttons #play-pause,
#av-container #av-inner #gui #buttons #share,
#av-container #av-inner #gui #buttons #sound {
	background-repeat: no-repeat;
	background-size: cover;
	height: 24px;
	width: 24px;
}
#av-container #av-inner #gui #buttons #left,
#av-container #av-inner #gui #buttons #right {
	height: 24px;
}
#av-container #av-inner #gui #buttons #left > div {
	float: left;
	margin-right: 14px;
	position: relative;
}
#av-container #av-inner #gui #buttons #left #play-pause.play {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27%23fff%27 d=%27M19.343 11.251c-.035-.439-.334-.874-.902-1.207L7.536 3.641c-1.211-.712-2.203-.138-2.203 1.275v7.463c5.85-2.36 13.783-1.163 14.01-1.128zM5.333 17v.762c0 1.412.992 1.985 2.203 1.273l10.904-6.402c.643-.377.941-.882.902-1.379-8.65.696-12.404 3.614-14.009 5.746z%27/%3E%3C/svg%3E');
}
#av-container #av-inner #gui #buttons #left #play-pause.pause {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27%23fff%27 d=%27M4.338 19.339h5v-16h-5v16zm9.001-16.001v16h5v-16h-5z%27/%3E%3C/svg%3E');
}
#av-container #av-inner #gui #buttons #left #play-pause.replay {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27%23fff%27 d=%27M16.672 11.339a5.334 5.334 0 0 1-10.668 0 5.334 5.334 0 0 1 5.326-5.333v2.336l7.016-3.503-7.016-3.503V3.34a8 8 0 0 0 .008 15.999 8 8 0 0 0 8-8h-2.666z%27/%3E%3C/svg%3E');
}
#av-container #av-inner #gui #buttons #left #phone {
	font-size: 0;
	width: auto;
}
#av-container #av-inner #gui #buttons #left #phone .avicon {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27%23fff%27 fill-rule=%27evenodd%27 d=%27M20.154 17.236c.299-.298.254-.921-.236-1.188-.492-.267-4.518-2.602-4.982-2.138-.463.465-1.447 1.498-2.135 1.188s-2.289-1.816-2.846-2.375c-.559-.557-2.064-2.159-2.377-2.847-.31-.687.725-1.67 1.188-2.134.464-.465-1.87-4.491-2.137-4.982-.266-.489-.889-.534-1.188-.237s-2.18 2.176-2.85 2.847c-.671.671-.279 5.415 4.514 10.202 4.787 4.792 9.531 5.185 10.203 4.514.671-.671 2.549-2.551 2.846-2.85z%27 clip-rule=%27evenodd%27/%3E%3C/svg%3E');
	background-repeat: no-repeat;
	background-size: cover;
	display: inline-block;
	height: 24px;
	vertical-align: top;
	width: 24px;
}
#av-container #av-inner #gui #buttons #left #phone #phone-num {
	color: #fff;
	display: inline-block;
	font-family: Helvetica, Arial, fallback, sans-serif;
	font-size: 12px;
	font-weight: 400;
	height: 24px;
	line-height: 24px;
	margin-left: 4px;
}
#av-container #av-inner #gui #buttons #right > div {
	float: right;
	margin-left: 14px;
	position: relative;
}
#av-container #av-inner #gui #buttons #right #sound {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.68 22.68%27%3E%3Cpath fill=%27%23fff%27 fill-rule=%27evenodd%27 d=%27M7.247 7.34H1.761v8h5.486l5.496 4.006V3.334z%27 clip-rule=%27evenodd%27/%3E%3C/svg%3E');
}
#av-container #av-inner #gui #buttons #right #sound div {
	background-repeat: no-repeat;
	background-size: cover;
	height: 100%;
	left: 0;
	position: absolute;
	top: 0;
	width: 100%;
}
#av-container #av-inner #gui #buttons #right #sound div.on {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27%23fff%27 d=%27m17.808 4.757-1.705 1.881c1.357 1.146 2.221 2.824 2.221 4.7s-.863 3.556-2.221 4.701l1.705 1.881c1.902-1.605 3.109-3.955 3.109-6.582 0-2.626-1.207-4.975-3.109-6.581z%27/%3E%3C/svg%3E');
}
#av-container #av-inner #gui #buttons #right #sound div.off {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27red%27 fill-rule=%27evenodd%27 d=%27m20.009 11.337 2.662-2.663-1.328-1.329-2.664 2.662-2.664-2.662-1.33 1.329 2.664 2.663-2.668 2.666 1.334 1.328 2.664-2.665 2.664 2.665 1.334-1.328z%27 clip-rule=%27evenodd%27/%3E%3C/svg%3E');
}
#av-container #av-inner #gui #buttons #right #share {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27%23fff%27 fill-rule=%27evenodd%27 d=%27M17.338 14.339a2.97 2.97 0 0 0-1.838.645l-7.17-3.567c0-.026.008-.051.008-.078 0-.026-.008-.052-.008-.078l7.17-3.566c.51.397 1.143.645 1.838.645a3 3 0 1 0-3-3c0 .188.023.372.057.552L7.531 9.304a2.982 2.982 0 0 0-2.193-.966 3 3 0 0 0 0 6c.869 0 1.645-.375 2.193-.965l6.863 3.412a3.05 3.05 0 0 0-.057.553 3.001 3.001 0 0 0 6 0 3 3 0 0 0-2.999-2.999z%27 clip-rule=%27evenodd%27/%3E%3C/svg%3E');
}
#av-container #av-inner #gui #buttons #right #fullscreen.off {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27%23fff%27 d=%27M4.339 15.339h-2v5h5v-2h-3v-3zm-2-8.001h2v-3h3v-2h-5v5zm13-5v2h3v3h2v-5h-5zm3 16.001h-3v2h5v-5h-2v3z%27/%3E%3C/svg%3E');
}
#av-container #av-inner #gui #buttons #right #fullscreen.on {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27%23fff%27 d=%27M6.338 6.338h-3v2h5v-5h-2v3zm-3 10.001h3v3h2v-5h-5v2zm11 3h2v-3h3v-2h-5v5zm2-13.001v-3h-2v5h5v-2h-3z%27/%3E%3C/svg%3E');
}
#av-container #av-inner #gui #big-play {
	background-color: #323232;
	background-color: rgba(0, 0, 0, 0.4);
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27%23fff%27 d=%27M19.343 11.251c-.035-.439-.334-.874-.902-1.207L7.536 3.641c-1.211-.712-2.203-.138-2.203 1.275v7.463c5.85-2.36 13.783-1.163 14.01-1.128zM5.333 17v.762c0 1.412.992 1.985 2.203 1.273l10.904-6.402c.643-.377.941-.882.902-1.379-8.65.696-12.404 3.614-14.009 5.746z%27/%3E%3C/svg%3E');
	background-position: 16px;
	background-repeat: no-repeat;
	background-size: 62% 64%;
	border: 3px solid #fff;
	border-radius: 50%;
	display: none;
	height: 68px;
	left: 50%;
	margin-left: -34px;
	margin-top: -34px;
	position: absolute;
	top: 50%;
	-webkit-transition: all 0.15s ease-in-out;
	-moz-transition: all 0.15s ease-in-out;
	-o-transition: all 0.15s ease-in-out;
	transition: all 0.15s ease-in-out;
	width: 68px;
}
#av-container #av-inner #gui #timer {
	background-color: #000;
	background-color: rgba(0, 0, 0, 0.7);
	border-color: #fff;
	border-style: solid;
	border-width: 0 1px 1px 0;
	font-size: 12px;
	height: 28px;
	left: 0;
	line-height: 28px;
	top: 0;
	width: 28px;
}
#av-container #av-inner #gui #skip-btn,
#av-container #av-inner #gui #timer {
	color: #fff;
	font-family: Helvetica, Arial, fallback, sans-serif;
	position: absolute;
	text-align: center;
	-webkit-transition: all 0.15s ease-in-out;
	-moz-transition: all 0.15s ease-in-out;
	-o-transition: all 0.15s ease-in-out;
	transition: all 0.15s ease-in-out;
}
#av-container #av-inner #gui #skip-btn {
	background-color: #323232;
	background-color: rgba(0, 0, 0, 0.4);
	border: 1px solid #fff;
	border-right-width: 0;
	bottom: 60px;
	font-size: 14px;
	height: 32px;
	line-height: 32px;
	min-width: 30px;
	padding: 0 12px;
	right: 0;
	text-transform: uppercase;
}
#av-container #av-inner #gui #aniview-credit {
	color: #fff;
	font-family: Helvetica, Arial, fallback, sans-serif;
	font-size: 11px;
	font-weight: 500;
	height: 24px;
	line-height: 24px;
	position: absolute;
	right: 2px;
	top: 2px;
}
#av-container #av-inner #gui #aniview-credit span {
	background-image: url('data:image/svg+xml;charset=utf-8,%3Csvg xmlns=%27http://www.w3.org/2000/svg%27 xml:space=%27preserve%27 width=%2723%27 height=%2723%27 viewBox=%270 0 22.677 22.677%27%3E%3Cpath fill=%27red%27 d=%27M19.343 11.251c-.035-.439-.334-.874-.902-1.207L7.536 3.641c-1.211-.712-2.203-.138-2.203 1.275v7.463c5.85-2.36 13.783-1.163 14.01-1.128zM5.333 17v.762c0 1.412.992 1.985 2.203 1.273l10.904-6.402c.643-.377.941-.882.902-1.379-8.65.696-12.404 3.614-14.009 5.746z%27/%3E%3C/svg%3E');
	background-repeat: no-repeat;
	background-size: cover;
	display: inline-block;
	height: 24px;
	vertical-align: top;
	width: 24px;
}
#av-container.av-desktop #av-inner #gui #big-play {
	border-color: #ccc;
}
#av-container.av-desktop #gui:before {
	bottom: -15%;
}
#av-container.av-desktop #gui #buttons,
#av-container.av-desktop #gui #timeline,
#av-container.av-desktop #gui:before {
	filter: alpha(opacity=0);
	opacity: 0;
}
#av-container.av-desktop:hover #av-inner #gui #big-play {
	background-color: #000;
	background-color: rgba(0, 0, 0, 0.7);
	border-color: #fff;
}
#av-container.av-desktop:hover #gui:before {
	bottom: 0;
}
#av-container.av-desktop #av-inner #gui #timeline:hover #timeline-moveto,
#av-container.av-desktop:hover #gui #buttons,
#av-container.av-desktop:hover #gui #timeline,
#av-container.av-desktop:hover #gui:before {
	filter: alpha(opacity=100);
	opacity: 1;
}
#av-container.av-responsive {
	height: 520px;
	width: 100%;
}
#av-container.hide-controls #av-inner #gui:before,
#av-container.hide-controls #buttons,
#av-container.hide-controls #timeline {
	display: none;
}
#av-container.buttons-below #av-inner #slot #videoslot {
	top: 0;
	-webkit-transform: none;
	transform: none;
}
#av-container #videoslot video {
	max-width: none;
}
#av-container #slot video {
	object-fit: contain;
}
@-webkit-keyframes "fade-in" {
	0% {
		filter: alpha(opacity=0);
		opacity: 0;
	}
	to {
		filter: alpha(opacity=100);
		opacity: 1;
	}
}
@-moz-keyframes "fade-in" {
	0% {
		filter: alpha(opacity=0);
		opacity: 0;
	}
	to {
		filter: alpha(opacity=100);
		opacity: 1;
	}
}
@-o-keyframes fade-in {
	0% {
		filter: alpha(opacity=0);
		opacity: 0;
	}
	to {
		filter: alpha(opacity=100);
		opacity: 1;
	}
}
@keyframes "fade-in" {
	0% {
		filter: alpha(opacity=0);
		opacity: 0;
	}
	to {
		filter: alpha(opacity=100);
		opacity: 1;
	}
}
@-webkit-keyframes "av-loading-dash" {
	0% {
		stroke-dasharray: 1, 210;
		stroke-dashoffset: 0;
	}
	50% {
		stroke-dasharray: 130, 220;
		stroke-dashoffset: -50;
	}
	to {
		stroke-dasharray: 170, 220;
		stroke-dashoffset: -210;
	}
}
@-moz-keyframes "av-loading-dash" {
	0% {
		stroke-dasharray: 1, 210;
		stroke-dashoffset: 0;
	}
	50% {
		stroke-dasharray: 130, 220;
		stroke-dashoffset: -50;
	}
	to {
		stroke-dasharray: 170, 220;
		stroke-dashoffset: -210;
	}
}
@-o-keyframes av-loading-dash {
	0% {
		stroke-dasharray: 1, 210;
		stroke-dashoffset: 0;
	}
	50% {
		stroke-dasharray: 130, 220;
		stroke-dashoffset: -50;
	}
	to {
		stroke-dasharray: 170, 220;
		stroke-dashoffset: -210;
	}
}
@keyframes "av-loading-dash" {
	0% {
		stroke-dasharray: 1, 210;
		stroke-dashoffset: 0;
	}
	50% {
		stroke-dasharray: 130, 220;
		stroke-dashoffset: -50;
	}
	to {
		stroke-dasharray: 170, 220;
		stroke-dashoffset: -210;
	}
}
@-webkit-keyframes "av-loading-rotate" {
	0% {
		stroke: #fff;
		-webkit-transform: rotate(0deg);
		transform: rotate(0deg);
	}
	to {
		stroke: currentColor;
		-webkit-transform: rotate(1turn);
		transform: rotate(1turn);
	}
}
@-moz-keyframes "av-loading-rotate" {
	0% {
		stroke: #fff;
		-webkit-transform: rotate(0deg);
		transform: rotate(0deg);
	}
	to {
		stroke: currentColor;
		-webkit-transform: rotate(1turn);
		transform: rotate(1turn);
	}
}
@-o-keyframes av-loading-rotate {
	0% {
		stroke: #fff;
		-webkit-transform: rotate(0deg);
		transform: rotate(0deg);
	}
	to {
		stroke: currentColor;
		-webkit-transform: rotate(1turn);
		transform: rotate(1turn);
	}
}
@keyframes "av-loading-rotate" {
	0% {
		stroke: #fff;
		-webkit-transform: rotate(0deg);
		transform: rotate(0deg);
	}
	to {
		stroke: currentColor;
		-webkit-transform: rotate(1turn);
		transform: rotate(1turn);
	}
}
```

Skip

Ads by

![](https://content1.avplayer.com/63f61879c01d725811007616/videos/66055a389f59458c0c088b72/3a5fe1f1-db8a-418d-abf8-fae1c176816e.webp)

Top VS Code Extensions for Web Developer in 2024!! GeeksforGeeks

Now Playing

![](https://content1.avplayer.com/63f61879c01d725811007616/videos/660559566921560ba5045a72/7e3dd383-d7f9-4b10-bea6-7be86c0f59fc.webp)

All Your Queries Answered | DSA to Development Program | GeeksforGeeks

Now Playing

![](https://content1.avplayer.com/63f61879c01d725811007616/videos/66055a6915ce8cc918062e43/56582be2-727b-444b-9244-1ba15f573280.webp)

Guided tour of GeeksforGeeks | Features and Overview

Now Playing

## Javascript

```html
<table border="0" cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<td class="code">
				<div class="container">
					<div class="line number1 index0 alt2">
                        ```typescript
						class="keyword">function
						class="plain"
						approach1Fn(obj: Recordstring, any):
							boolean {
                        ```
					</div>
					<div class="line number2 index1 alt1">
						<code class="undefined spaces">&nbsp;&nbsp;</code
						><code class="keyword">return</code>
						<code class="plain"
							>Object.keys(obj).length === 0;</code
						>
					</div>
					<div class="line number3 index2 alt2">
						<code class="plain">}</code>
					</div>
					<div class="line number4 index3 alt1">
						<code class="plain"
							>const obj: Record&lt;string, any&gt; = {};</code
						>
					</div>
					<div class="line number5 index4 alt2">
						<code class="plain"
							>const res: boolean = approach1Fn(obj);</code
						>
					</div>
					<div class="line number6 index5 alt1">
						<code class="plain">console.log(res);</code>
					</div>
				</div>
			</td>
		</tr>
	</tbody>
</table>
```

#### Output:

true

## Using for…in Loop

In this approach, we are using a [for…in loop](https://www.geeksforgeeks.org/javascript-for-in-loop/) in TypeScript to iterate through the properties of the object (\***\*obj\*\***). The loop checks if any property is present, and if it is present, it returns false, indicating that the object is not empty. If no properties are found, the function returns true, indicating that the object is empty.

### Syntax:

for (const variable in object) {  
 // code  
}

\***\*Example:\*\*** The below example uses for…in Loop to check if an Object is empty in TypeScript.

## Javascript

```html
<table border="0" cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<td class="code">
				<div class="container">
					<div class="line number1 index0 alt2">
						<code class="keyword">function</code>
						<code class="plain"
							>approach2Fn(obj: Record&lt;string, any&gt;):
							boolean {</code
						>
					</div>
					<div class="line number2 index1 alt1">
						<code class="undefined spaces"
							>&nbsp;&nbsp;&nbsp;&nbsp;</code
						><code class="keyword">for</code>
						<code class="plain">(const key </code
						><code class="keyword">in</code>
						<code class="plain">obj) {</code>
					</div>
					<div class="line number3 index2 alt2">
						<code class="undefined spaces"
							>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code
						><code class="keyword">if</code>
						<code class="plain">(obj.hasOwnProperty(key)) {</code>
					</div>
					<div class="line number4 index3 alt1">
						<code class="undefined spaces"
							>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code
						><code class="keyword">return</code>
						<code class="keyword">false</code
						><code class="plain">;</code>
					</div>
					<div class="line number5 index4 alt2">
						<code class="undefined spaces"
							>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code
						><code class="plain">}</code>
					</div>
					<div class="line number6 index5 alt1">
						<code class="undefined spaces"
							>&nbsp;&nbsp;&nbsp;&nbsp;</code
						><code class="plain">}</code>
					</div>
					<div class="line number7 index6 alt2">
						<code class="undefined spaces"
							>&nbsp;&nbsp;&nbsp;&nbsp;</code
						><code class="keyword">return</code>
						<code class="keyword">true</code
						><code class="plain">;</code>
					</div>
					<div class="line number8 index7 alt1">
						<code class="plain">}</code>
					</div>
					<div class="line number9 index8 alt2">
						<code class="plain"
							>const obj: Record&lt;string, any&gt; = {};</code
						>
					</div>
					<div class="line number10 index9 alt1">
						<code class="plain"
							>const res: boolean = approach2Fn(obj);</code
						>
					</div>
					<div class="line number11 index10 alt2">
						<code class="plain">console.log(res);</code>
					</div>
				</div>
			</td>
		</tr>
	</tbody>
</table>
```

#### Output:

true

## Using JSON.stringify() function

In this approach, we are using the [JSON.stringify()](https://www.geeksforgeeks.org/javascript-json-stringify-method/) function in TypeScript to convert the object (obj) into a JSON string. The equality check \***\*JSON.stringify(obj) === ‘{}’\*\*** checks if the resulting string represents an empty object. If true, it indicates that the original object is empty, printing in the function returning true as output.

### Syntax:

JSON.stringify(value, replacer?, space?)

\***\*Example:\*\*** The below example uses JSON.stringify() function to check if an Object is empty in TypeScript.

## Javascript

```html
<table border="0" cellpadding="0" cellspacing="0">
	<tbody>
		<tr>
			<td class="code">
				<div class="container">
					<div class="line number1 index0 alt2">
						<code class="keyword">function</code>
						<code class="plain"
							>approach3Fn(obj: Record&lt;string, any&gt;):
							boolean {</code
						>
					</div>
					<div class="line number2 index1 alt1">
						<code class="undefined spaces">&nbsp;&nbsp;</code
						><code class="keyword">return</code>
						<code class="plain">JSON.stringify(obj) === </code
						><code class="string">'{}'</code
						><code class="plain">;</code>
					</div>
					<div class="line number3 index2 alt2">
						<code class="plain">}</code>
					</div>
					<div class="line number4 index3 alt1">
						<code class="plain"
							>const obj: Record&lt;string, any&gt; = {};</code
						>
					</div>
					<div class="line number5 index4 alt2">
						<code class="plain"
							>const res: boolean = approach3Fn(obj);</code
						>
					</div>
					<div class="line number6 index5 alt1">
						<code class="plain">console.log(res);</code>
					</div>
				</div>
			</td>
		</tr>
	</tbody>
</table>
```

#### Output:

true

“This course was packed with amazing and well-organized content! The project-based approach of this course made it even better to understand concepts faster. Also the instructor in the live classes is really good and knowledgeable.”- **Tejas | Deutsche Bank**

With our revamped [Full Stack Development Program](https://www.geeksforgeeks.org/courses/full-stack-node?utm_source=geeksforgeeks&utm_medium=article_bottom_text_fullstacktags&utm_campaign=courses): **master Node.js and React that enables you to create dynamic web applications**.

So get ready for salary hike only with our [Full Stack Development Course](https://www.geeksforgeeks.org/courses/full-stack-node?utm_source=geeksforgeeks&utm_medium=article_bottom_text_fullstacktags&utm_campaign=courses).

Like Article

Suggest improvement

[Previous](https://www.geeksforgeeks.org/how-to-check-if-a-set-is-empty-in-swift/?ref=previous_article)

[How to check if a set is empty in Swift?](https://www.geeksforgeeks.org/how-to-check-if-a-set-is-empty-in-swift/?ref=previous_article)

[Next](https://www.geeksforgeeks.org/how-to-get-an-object-value-by-key-in-typescript/?ref=next_article)

[How to Get an Object Value By Key in TypeScript](https://www.geeksforgeeks.org/how-to-get-an-object-value-by-key-in-typescript/?ref=next_article)

Share your thoughts in the comments

Add Your Comment

### Please Login to comment...

### Similar Reads

[

How to Check if an Object is Empty in TypeScript ?

](https://www.geeksforgeeks.org/how-to-check-if-an-object-is-empty-in-typescript/)[

Check if an Array is Empty or not in TypeScript

](https://www.geeksforgeeks.org/check-if-an-array-is-empty-or-not-in-typescript/)[

How to Initialize a TypeScript Object with a JSON-Object ?

](https://www.geeksforgeeks.org/how-to-initialize-a-typescript-object-with-a-json-object/)[

How to check an object is empty using JavaScript?

](https://www.geeksforgeeks.org/how-to-check-an-object-is-empty-using-javascript/)[

How to Avoid Inferring Empty Array in TypeScript ?

](https://www.geeksforgeeks.org/how-to-avoid-inferring-empty-array-in-typescript/)[

How to Return an Empty Promise in TypeScript ?

](https://www.geeksforgeeks.org/how-to-return-an-empty-promise-in-typescript/)[

How to Check if an Array Includes an Object in TypeScript ?

](https://www.geeksforgeeks.org/how-to-check-if-an-array-includes-an-object-in-typescript/)[

How to Check the Type of an Object in Typescript ?

](https://www.geeksforgeeks.org/how-to-check-the-type-of-an-object-in-typescript/)[

How to Check if all Enum Values Exist in an Object in TypeScript ?

](https://www.geeksforgeeks.org/how-to-check-if-all-enum-values-exist-in-an-object-in-typescript/)[

How to handle empty object before mount in ReactJS ?

](https://www.geeksforgeeks.org/how-to-handle-empty-object-before-mount-in-reactjs/)

Like

[

G

](https://auth.geeksforgeeks.org/user/gauravgandal/articles?utm_source=geeksforgeeks&utm_medium=article_author&utm_campaign=auth_user)

[gauravgandal](https://auth.geeksforgeeks.org/user/gauravgandal/articles?utm_source=geeksforgeeks&utm_medium=article_author&utm_campaign=auth_user)
