<p align="center">
	<a href="https://zengabor.github.io/zenscroll/">
		<img src="https://zengabor.github.io/zenscroll/zenscroll.png" alt="Zenscroll">
	</a>
</p>


#### [**Demo**](https://zengabor.github.io/zenscroll/) &nbsp; &nbsp; &nbsp; &nbsp; [**Download**](https://github.com/zengabor/zenscroll/archive/latest.zip) &nbsp; &nbsp; &nbsp; &nbsp; [**About**](#about) &nbsp; &nbsp; &nbsp; &nbsp; [**Install**](#install) &nbsp; &nbsp; &nbsp; &nbsp; [**How to use**](#how-to-use) &nbsp; &nbsp; &nbsp; &nbsp; [**License**](#license)


# One JavaScript to Smooth-Scroll Them All

Smooth animated scrolling. No&nbsp;more abrupt jumps on your page.
Move&nbsp;elements into view, center them, or scroll to any Y&nbsp;position.

870 bytes of pure JavaScript. No&nbsp;dependencies.

## About

Zenscroll is a vanilla JavaScript module that enables animated vertical scrolling to any element or any position within your document or within a DIV or other scrollable container.

Features:

- Animated scrolling to anchors on the same page.
- Scroll to the top of a specific element.
- Scrolling an element into view, making sure both top & bottom are visible, if possible.
- Scroll to an element while centering it on the screen.
- Customize the duration.
- Specify the spacing between the element and the edge of the screen (required for fixed navigation bars and footers).
- No dependencies.
- Small size: 870 bytes (minimized & gzipped).

Full support tested and works under:

- Android Browser 2.2+
- Chrome for Android
- Chrome 14+ (probably earlier too)
- Edge
- Firefox 9+
- Internet Explorer 9+
- iOS Safari 4+
- Opera 10.6+ (probably earlier too)
- Safari 4+ (including Safari 9 on OS X 10.11 beta)
- Windows Phone 8.1
- Yandex 14.12

Basic support (animated scroll in document) tested and works under:

- Firefox 3+
- Internet Explorer 6+
- iOS Safari 3+

## Install

[Download Zenscroll](https://github.com/zengabor/zenscroll/archive/latest.zip) and include it into your page. A good place is at the very bottom, just before the closing `</body>` tag. For&nbsp;example:

````html
    ...
    <script src="zenscroll-min.js"></script>
</body>
````

You can also use npm to install Zenscroll:

````
npm install zenscroll
````

## How to use

### 1. Smooth scroll within your page

If Zenscroll is included in your page it will automatically animate the scrolling to anchors on the same page. This works even with content you dynamically load via ajax, as Zenscroll uses a generic click handler.

Since this is implemented a progressive enhancement, all internal links still work even in very old browsers. Note that internal links are intentionally not added to the history to save the users from having to hit the Back button too many times afterwards.

If you want some links to be excluded from this, then start with the path of the page. E.g., instead of writing `<a href="#about">` write  `<a href="/#about">`. 

You can also disable this automatic smoothing for all internal links by executing:

````js
zenscroll.setup(null, null, true)
````


### 2. Scroll to the top of an element

````js
var about = document.getElementById("about")
zenscroll.to(about)
````

Note that Zenscroll intentionally leaves a few pixels (by default 9px) from the edges of the screen or scolling container. If you have a fixed navigation bar or footer bar then you probably need more than that. Or you may want to set it to zero. You can globally override the default value by calling `zenscroll.setup()` (see below) or with the `edgeOffset` parameter of the constructor when you create a scroller for a DIV.

### 3. Scroll to a specific vertical position

````js
zenscroll.toY(123)
````

### 4. Scroll an element into view 

If the element is already fully visible then no scroll is performed. Otherwise Zenscroll will try to make both top & bottom of element visible, if possible. If the element is higher than the visible viewport then it will simply scroll to the top of the element. 

````js
zenscroll.intoView(image1)
````

Tip: If you resize an element with a transition of 500ms, you can postpone calling zenscroll with that amount of time:

````js
image.classList.remove("is-small")
setTimeout(function () { 
    zenscroll.intoView(image2) 
}, 500)
````


### 5. Scrolls the element to the center of the screen

````js
zenscroll.center(image2)
````

If you want you can also define an offset. The top of the element will be upwards from the center of the screen by this amount of pixels. (By default offset is the half of the element’s height.)

````js
var duration = 500 // miliseconds
var offset = 200 // pixels
zenscroll.center(image2, duration, offset)
````

Note that a zero value for offset is ignored. You can work around this by using `zenscroll.toY()`.

### 6. Set the duration of the scroll

The default duration is 999 which is ~1 second. The duration is automatically reduced for elements that are very close. You can specifically set the duration via an optional second parameter. (Note that a value of zero for duration is ignored.)

Examples:

````js
zenscroll.toY(70, 100) // 100ms == 0.1 second
````

````js
zenscroll.to(about, 500) // 500ms == half a second
````

````js
zenscroll.center(image2, 2000) // 2 seconds
````

### 7. Scroll inside a scrollable DIV

Anything you can do within the document you can also do inside a scrollable element. You just need to instantiate a new scoller for that element.

Example:

````html
<div id="container">
  <div id="item1">ITEM 1</div>
  <div id="item2">ITEM 2</div>
  <div id="item3">ITEM 3</div>
  <div id="item4">ITEM 4</div>
  <div id="item5">ITEM 5</div>
  <div id="item6">ITEM 6</div>
  <div id="item7">ITEM 7</div>
</div>

<script>
  var c = document.getElementById("container")
  var defaultDuration = 500
  var edgeOffset = 4
  var cScroll = zenscroll.newFor(c, defaultDuration, edgeOffset)
  var target = document.getElementById("item4")
  cScroll.center(target)
</script>
````

Obviously you can use all other scroll methods and parameters with the scrollable container. Two more examples:

````js
cScroll.toY(35)
````

````js
cScroll.intoView(target, 750)
````

### 8. Change settings

It’s easy to change the basic parameters of scrolling:

- You can set the default value for duration. This will be valid for internal scrolls and all your direct scroll calls where you don’t specify a duration.
- Change the edge offset (the spacing between the element and the screen edge). This is very useful if you have a fixed navigation bar or footer bar: set it to at least the height of your fixed bar.
- You can also turn on or off the automatic smoothing for internal links.

````js
var defaultDuration = 777
var edgeOffset = 42
var disableInternalLinkSmoothing = false
zenscroll.setup(defaultDuration, edgeOffset, disableInternalLinkSmoothing)
````

If you don’t want to change a value just omit the parameter or pass `null`. For example, the line below sets the default duration, while leaving other settings unchanged:

````js
zenscroll.setup(500)
````

Sets the the spacing between the edge of the screen (or a DIV) and the target element you are scrolling to, while leaving the default duration unchanged:

````js
zenscroll.setup(null, 5)
````

Disable the automatic smoothing for internal links, while leaving both other settings unchanged:

````js
zenscroll.setup(null, null, true)
````


### 9. Controlling the smooth operation

To check whether a scoll is being performed right now:

````js
var isScrolling = zenscroll.moving()
````

To stop the current scrolling:

````js
zenscroll.stop()
````

## License

[Public Domain](http://unlicense.org). You can do with it whatever you want and I am not responsible for anything.


## Other projects by me:

- [Zenfonts](https://github.com/zengabor/zenfonts), a tiny JavaScript helper for @font-face loading.
- [Zentaps](https://github.com/zengabor/zentaps), a JavaScript module to kill the 300ms tap delay in mobile browsers.
- [Zenvite.com](http://zenvite.com/): Create beautiful invitation pages & get everybody on the same page.
