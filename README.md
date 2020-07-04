# ![ripplet.js](https://luncheon.github.io/ripplet.js/logo.gif)

Fully controllable vanilla-js material design ripple effect generator.  
This can be used with any JavaScript framework and/or any CSS framework.

[Demo](https://luncheon.github.io/ripplet.js/demo/)  


## Installation

### via npm

```bash
$ npm install ripplet.js
```

```javascript
import ripplet from 'ripplet.js';

element.addEventListener('mousedown', ripplet);
```

### via CDN

```html
<script src="https://cdn.jsdelivr.net/npm/ripplet.js@0.2.1"></script>
<button onmousedown="ripplet(arguments[0])">Click me!</button>
```

### Download directly

<a target="_blank" download="ripplet.min.js" href="https://cdn.jsdelivr.net/npm/ripplet.js@0.2.1/umd/ripplet.min.js">Download ripplet.min.js</a>


## API

### ripplet(targetSuchAsMouseEvent[, options]) => HTMLElement

Generate a ripplet immediately.  
In particular, create two elements (one is a circular enlarging element representing ripplet, and the other is a container element to restrict visible area) and remove them when the animation ends. Do nothing else.

#### Parameters

* targetSuchAsMouseEvent: Object (required) (in most cases, pass the received MouseEvent object)

| Property name           | Description                              |
| ----------------------- | ---------------------------------------- |
| currentTarget           | Target element                           |
| clientX                 | Client x-coordinate of center of ripplet |
| clientY                 | Client y-coordinate of center of ripplet |

* options: Object (optional)

| Property name           | Default        | Description           |
| ----------------------- | -------------- | --------------------- |
| className               | ""             | Class name to be set for the ripplet element (not for this library to use, but for user to style that element) |
| color                   | "currentColor" | Ripplet color that can be interpreted by browsers. Specify `null` if the color or image of the ripple effect is based on the CSS className above.<br>If the special value `"currentColor"` is specified, the text color of the target element (`getComputedStyle(currentTarget).color`) is used. |
| opacity                 | 0.1            | Ripplet opacity between 0 and 1. |
| spreadingDuration       | ".4s"          | As its name suggests. |
| spreadingDelay          | "0s"           | As its name suggests. |
| spreadingTimingFunction | "linear"       | As its name suggests. See https://developer.mozilla.org/docs/Web/CSS/transition-timing-function |
| clearingDuration        | "1s"           | As its name suggests. |
| clearingDelay           | "0s"           | As its name suggests. |
| clearingTimingFunction  | "ease-in-out"  | As its name suggests. See https://developer.mozilla.org/docs/Web/CSS/transition-timing-function  |
| centered                | false          | Whether to force the origin centered (and ignore `clientX` and `clientY`). |
| appendTo                | "body"         | Either `"body"` or `"parent"`. Consider specifying `"parent"` if there are scrollable ancestors or `position: fixed` ancestors.<br>If the parent treats children as special (e.g. the parent is a flexbox on IE), specifying `"parent"` may cause the ripplet to be placed incorrectly. |

#### Return value

Generated container element (having one child element representing ripplet)


### defaultOptions

You can change the default ripplet options for your app.  
For example:

```javascript
import { defaultOptions } from 'ripplet';

defaultOptions.color = 'rgb(64, 128, 255)';
```

or

```html
<script src="https://cdn.jsdelivr.net/npm/ripplet.js@0.2.1"></script>
<script>
  ripplet.defaultOptions.color = 'rgb(64, 128, 255)';
</script>
```


## Declarative Edition

If you don't need detailed control, you can use declarative edition that captures mousedown events.  
Load `"ripplet-declarative.js"` and add `data-ripplet` attribute to html elements with/without options.  
Elements dynamically appended also have the ripple effect if `data-ripplet` attribute is available.


### Example Usage

```html
<script src="https://cdn.jsdelivr.net/npm/ripplet.js@0.2.1/umd/ripplet-declarative.min.js"></script>
<!-- <script>ripplet.defaultOptions.color = 'rgb(0, 255, 0)';</script> -->

<button data-ripplet>Default</button>
<button data-ripplet="color: rgb(64, 192, 255); spreading-duration: 2s; clearing-delay: 1.8s;">Sky Blue Slow</button>
```

or

```javascript
import 'ripplet.js/es/ripplet-declarative';
// require(ripplet.js/umd/ripplet-declarative.min');

// import { defaultOptions } from 'ripplet.js/es/ripplet-declarative';
// defaultOptions.color = 'rgb(255, 128, 0)';
```

or

<a target="_blank" download="ripplet-declarative.min.js" href="https://cdn.jsdelivr.net/npm/ripplet.js@0.2.1/umd/ripplet-declarative.min.js">Download ripplet-declarative.min.js</a>


## Tips

I recommend applying following styles to the ripple target elements:

1. Erase tap highlight effect for iOS
2. Disable tap-to-hover behavior and double-tap-to-zoom behavior for iOS

```css
/* Example for the declarative edition */
[data-ripplet] {
  -webkit-tap-highlight-color: transparent; /* 1 */
  touch-action: manipulation; /* 2 */
}
```

## License

WTFPL
