# JSX Synonym

## Getting started

### Code embedding

```html
<script src="program.js"></script>
```

```html
<!-- # need compiling
    $ jsx --execute web --output program.jsx.js program.jsx
-->
<script src="program.jsx.js"></script>
```

### Entry point

```javascript
// not required
// all the top level statements run immediately

// or to run after content loaded
jQuery(function ($) {
    // ...
});
```

```jsx
// _Main.main(:string[]):void is called
// after content loaded when it compiled with --execute web
class _Main {
    static function main(args : string[]) : void {
        // ...
    }
}
```

### Printing to the console

```javascript
console.log("Hello, world!");
```

```jsx
// use the log statement
log "Hello, world!";
```

### Modal alerts

```javascript
alert("Clicked on the button.");
```

```jsx
import "js/web.jsx";

dom.window.alert("Clicked on the button.");
```

### Assertions

```javascript
console.assert(x >= 0);
```

```jsx
// use the assert statement,
// which is removed by optimizations
assert x >= 0;
```

## Code modularity

### Define a library

```javascript
// No native implementation.
// Consider require.js and AMD
```

```jsx
// a JSX module may have multiple classes

// public class, exported by default
class Dog {
    function noise() : string {
        return _DogHelper.NOISE;
    }
}

// private class, not exported by default
class _DogHelper {
    static const NOISE = "BARK!";
}
```

## Variables

WIP

## Collections

WIP

## Strings

### Encoding a string as an URI component

```javascript
var s = encodeURIComponent("foo&bar");
console.assert(s === "foo%26bar");
```

```jsx
var s = String.encodeURIComponent("foo&bar");
assert s == "foo%26bar";
```

## Numbers

## Converting a string to an integer

```javascript
var n = parseInt("10", 8);
console.assert(n === 8);
```

```jsx
var n = Number.parseInt("10", 8);
assert n == 8;
```

## Converting a string to a number

```javascript
var n = +"10";
console.assert(n === 10);
```

```jsx
var n = 10 as number;
assert n == 10;
```

## Booleans

WIP

## Functions

WIP

## Classes

WIP

## Finding elements in DOM

Note that all the JSX code requires `import "js/web.jsx";` at the head of the program.

### Find one element by ID

```javascript
document.getElementById("main");

document.querySelector("#main");
```

```jsx
dom.document.getElementById("main"); // is Element
dom.getElementById("main");          // is HTMLElement
dom.id("main");                      // is HTMLElement

dom.document.querySelector("#main");
```

### Find one element by class

```javascript
document.getElementsByClassName("visible")[0];

document.querySelector(".visible");
```

```jsx
dom.document.getElementsByClassName(".visible")[0];

dom.document.querySelector(".visible");
```

### Find one element by tag

```javascript
document.getElementsByTagName("div")[0];

document.querySelector("div");
```

```jsx
dom.document.getElementsByTagName("div")[0];

dom.document.querySelector("dive");
```

### Find one element by name

```javascript
document.getElementsByName("form")[0];

document.querySelector("[name='div']");
```

```jsx
dom.document.getElementsByTagName("div")[0];

dom.document.querySelector("dive");
```

### Find elements by combination of above

```javascript
document.getElementById("main").getElementsByTagName("dive")[0].getElementsByClassName("visible");

document.querySelectorAll("#main div:first-of-type .visible");
```

```jsx
dom.id("main").getElementsByTagName("dive")[0].getElementsByClassName("visible");

dom.document.querySelectorAll("#main div:first-of-type .visible");
```

### Access the first child

```javascript
elem.firstChild();
```

```jsx
elem.firstChild();
```

### Find out whether an element has children elements

```javascript
elem.hasChildNodes();
```

```jsx
elem.hasChildNodes();
```

## Manipulationg DOM

### Creating an element

```javascript
var element = document.createElement("div");
```

```jsx
var element = dom.document.createElement("dive"); // is Element
var element = dom.createElement("div");           // is HTMLElement
```

## Event handling

## Adding an event listener

```javascript
element.addEventListener("click", function (event) {
    // ...
});
```

```jsx
element.addEventListener("click", function (event) {
    // ...
});
```

## Adding a mouse event listener

```javascript
element.addEventListener("mousedown", function (event) {
    var x = event.clientX;
    var y = event.clientY;
    var rect = event.target.getBoundingClientRect();

    x -= rect.left;
    y -= rect.top;
    // ...
});
```

```jsx
// need casting for event and event.target
element.addEventListener("mousedown", function (event) {
    assert event instanceof MouseEvent;
    var e = event as MouseEvent;
    var x = e.clientX;
    var y = e.clientY;
    assert event.target instanceof HTMLElement;
    var element = event.target as HTMLElement;
    var rect = element.getBoundingClientRect();

    x -= rect.left;
    y -= rect.top;
    // ...
});
```

## Schedule a future event

```javascript
window.setTimeout(function () {
    // ...
}, 1000);
```

```jsx
dom.window.setTimeout(function () {
    /// ...
}, 1000);
```

## Graphics

### Getting rendering context for 2D

```javascript
var canvas = document.getElementById("world");
var cx     = canvas.getContext("2d");
```

```jsx
var canvas = document.getElementById("world") as HTMLCanvasElement;
var cx     = canvas.getContext("2d") as CanvasRenderingContext2D;
```

### Getting rendering context for 3D

Note that WebGL is experimental.

```javascript
var canvas = document.getElementById("world");
var gl     = canvas.getContext("webgl-experimental");
```

```jsx
var canvas = document.getElementById("world") as HTMLCanvasElement;
var gl     = canvas.getContext("webgl-experimental") as WebGLRenderingContext;
```

# SEE ALSO

Thanks for [synonym.dartlang.org](http://synonym.dartlang.org/) for inspirations.

