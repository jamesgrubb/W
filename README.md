W 1.2.3
=======

CSS media queries are a powerful tool to deal with responsive designs : the browser handles design updates by itself. Unfortunately, in the javascript environment it's not the same. Browsers return different values for their viewport and no simple events exist to know when the user has resized his window or zoomed your site's contents. Moreover, media queries computing is based on the screen resolution and not the inner size of the window : design and content should rely to the window to keep consistent, not the screen (per example, on iOS8, on an iPad2, returns `768x1024` in portrait and lanscape).

W aims to solve these problems.

Install
-------

You can pick the minified library or install it with :

```
jam install pyrsmk-w
bower install pyrsmk-w
npm install pyrsmk-w --save-dev
```

Hey, that's new!
----------------

My routines have been coded from scratch and I can detect much more devices than before. And I can detect device orientation too! Thanks a lot to all the people that have participated to the recent wide tests ;)

Syntax
------

```javascript
// Get the orientation of the device (return 'portrait' or 'landscape')
W.getOrientation();
// Get the current viewport width
W.getViewportWidth();
// Get the current viewport height
W.getViewportHeight();
// Convert pixels to ems (based on the current browser text size)
W.px2em(768);
// Add a listener to catch responsive events
W.addListener(function(){});
```

If needed, when you register a listener you can chain `W` to reuse that very same function :

```javascript
$(window).listen('scroll',W.addListener(function(){
    console.log("Hi! I'm the one who detects scroll and responsive events!");
}));
```

For those who want to base W on the screen resolution (to unify JS and CSS behaviors, per example), you can toggle the following flag :

```javascript
W.setAbsoluteMode(true); // false by default
```

Caveats
-------

- under iOS5 (and maybe 6), W will always return `portrait` as device orientation; the values that iOS return are really weird and I found no way to guess the orientation
- zoom events won't change `em` unit in pixels; to be clear, `1em` will always equal to `16px` with zooms, the only way to have a change of this unit is by changing the global text size in the parameters of user's browser; that caveat just affect `px2em()`

With IE6-8, please consider waiting for DOM readiness before using W because of these issues (but it's not really important...) :

- IE6-7 will report a [zero offsetWidth](https://github.com/pyrsmk/W/issues/1), so W will fallbacks to a `16px` default value for `em` calculation (and it won't return a realistic `em` value when text size has been changed)
- IE8 could [throw an error telling that the parent element can't be modified while a child element is not closed](https://github.com/pyrsmk/W/issues/3)

License
-------

W is licensed under the [MIT license](http://dreamysource.mit-license.org).
