# Smooth anchor scrolling

jQuery script which checks the page URI for an anchor and scrolls to the target element smoothly.

## Usage

* Add an `id=` attribute to the element to which you want to scroll, which must match the location hash in the browser. e.g. `id="comments"`.
* Link to this element as usual: e.g. `<a href="#comments">Scroll to comments</a>`.
* Initialize the JavaScript.

### Initialize the JavaScript

```javascript
$('a[href*="#"]').anchorAnimate();
```

### Scrolling manually

```javascript
$('#comments').scrollToMe();
```

### Adding an offset

e.g. if you have a fixed toolbar. Update the value of the JavaScript variable `window.anchorAnimateOffset`.

```javascript
// General offset
window.anchorAnimateOffset = 16;

// Extend window.anchorAnimateOffset variable with your fixed elements
var setAnchorOffset = function(){
	$('.nav.toolbar').each(function(){
		if ( $(this).outerHeight() && $(this).css("position") === "fixed"){
			window.anchorAnimateOffset += $(this).outerHeight();
		}
	});
	window.anchorAnimateOffset = Math.floor(window.anchorAnimateOffset) - 1;
};

// Initialize the functionality
$(document).on('ready.anchoranimate', function(){
	$('a[href*="#"]').anchorAnimate();
});

// Update window.anchorAnimateOffset value
$(window).on('load.anchoranimate resize.anchoranimate', setAnchorOffset);

```

### Following events are triggered

```javascript
$(window).trigger('ct-hashscroll/scroll-start', window.anchorAnimateOffset, destinationTop);
```

### Example of responding to a custom event

```javascript
$(window).on('ct-hashscroll/scroll-start', function(event, anchorAnimateOffset, destinationTop){
    window.console.log([anchorAnimateOffset, destinationTop]);
});
```

## Changelog

### 2.0.1 2019-11-15

* Initial @markhowellsmead version at Github.

### 1.0.0 2019-01-18

* Initial @sayhellogmbh version.
