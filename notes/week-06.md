# DOM Manipulation and Events in JavaScript

## 1. The DOM: trees, nodes, elements

The **DOM** (Document Object Model) is a tree-like representation of a webpage. When the browser reads your HTML, it converts it into a tree of **nodes**, which are JavaScript objects with properties and methods. There are many types of nodes, but here we focus on **element nodes** (the HTML tags).

```html
<div id="container">
  <div class="display"></div>
  <div class="controls"></div>
</div>
```

The relationships work like a family tree:

- `#container` is the **parent**.
- `.display` and `.controls` are its **children**.
- `.display` and `.controls` are **siblings** of each other.

**Important:** JavaScript changes the DOM, **not your HTML file**. The file stays the same; only what the browser renders changes.

---

## 2. Selecting nodes

Before you can change a node, you have to "target" it. There are two ways.

### 2.1 CSS-style selectors

For the `<div class="display">` in the example above, all of these work: `div.display`, `.display`, `#container > .display`, `div#container > div.display`.

| Method | What it returns |
|---|---|
| `element.querySelector(selector)` | the **first** matching element |
| `element.querySelectorAll(selector)` | a **NodeList** with **all** matching elements |

### 2.2 Relationships between nodes

You start from one node and use its properties to move around:

```javascript
const container = document.querySelector("#container");
const display = container.firstElementChild;   // <div class="display">
```

```javascript
const controls = document.querySelector(".controls");
const display = controls.previousElementSibling; // <div class="display">
```

The dot in `container.firstElementChild` is normal object notation. `firstElementChild` is a **key** of the `container` object, and its **value** is the first child node.

### 2.3 NodeList ≠ array

`querySelectorAll` returns a **NodeList**. It looks like an array and you can loop over it, but **several array methods are missing**. If needed, convert it:

```javascript
const items = document.querySelectorAll(".item");
const arr1 = Array.from(items);
const arr2 = [...items]; // spread operator
```

---

## 3. Creating, inserting and removing elements

### 3.1 Creating

```javascript
const div = document.createElement("div");
```

`createElement` does **not** put the element on the page: it only creates it in memory. This lets you prepare it (classes, text, style) before placing it in the DOM.

### 3.2 Inserting

| Method | Effect |
|---|---|
| `parentNode.appendChild(childNode)` | adds `childNode` as the **last child** of `parentNode` |
| `parentNode.insertBefore(newNode, referenceNode)` | inserts `newNode` into `parentNode`, **before** `referenceNode` |

### 3.3 Removing

```javascript
parentNode.removeChild(child); // removes it from the DOM and returns a reference to the child
```

### 3.4 Full example

```html
<body>
  <h1>THE TITLE OF YOUR WEBPAGE</h1>
  <div id="container"></div>
</body>
```

```javascript
const container = document.querySelector("#container");

const content = document.createElement("div");
content.classList.add("content");
content.textContent = "This is the glorious text-content!";

container.appendChild(content);
```

The resulting DOM:

```html
<div id="container">
  <div class="content">This is the glorious text-content!</div>
</div>
```

To nest several elements, **fill the created element first** (add its children) and **then** append it to the container.

---

## 4. Altering an element

With a reference to an element you can change its style, attributes, classes and content.

### 4.1 Inline style

```javascript
div.style.color = "blue";
div.setAttribute("style", "color: blue; background: white;"); // replaces ALL inline style
```

CSS properties containing a hyphen (`background-color`) need different syntax:

```javascript
div.style.background-color;     // ❌ read as "div.style.background - color"
div.style.backgroundColor;      // ✅ camelCase with dot notation
div.style["background-color"];  // ✅ bracket notation with kebab-case (string)
div.style["backgroundColor"];   // ✅ bracket notation with camelCase (string)
```

### 4.2 Attributes

```javascript
div.setAttribute("id", "theDiv");  // updates it if it exists, creates it otherwise
div.getAttribute("id");            // "theDiv"
div.removeAttribute("id");         // removes it
```

### 4.3 Classes

```javascript
div.classList.add("new");
div.classList.remove("new");
div.classList.toggle("active"); // adds it if missing, removes it if present
```

It is usually cleaner to **toggle a CSS class** than to add and remove inline styles.

### 4.4 Content

```javascript
div.textContent = "Hello World!";               // inserts plain text
div.innerHTML = "<span>Hello World!</span>";    // interprets the string as HTML
```

**Security risk:** `innerHTML` should be used sparingly because it can allow code injection (XSS attacks). For plain text, prefer `textContent`.

---

## 5. When your JavaScript runs

Your script runs at the moment the browser encounters it. If it sits in the `<head>` and the DOM hasn't been built yet, selection methods **find nothing**.

Two solutions:

```html
<!-- 1. Script at the bottom of body, after the elements -->
<body>
  ...
  <script src="js-file.js"></script>
</body>
```

```html
<!-- 2. Script in head with defer: runs after the HTML has been parsed -->
<head>
  <script src="js-file.js" defer></script>
</head>
```

---

## 6. Callbacks

Callbacks are needed to understand events, so we cover them first.

**A callback is a function passed into another function as an argument.** Functions in JavaScript are "first class citizens": they can be assigned to variables and passed around.

### 6.1 The parts of a function

```javascript
function funkyFunction(music, isWhiteBoy) {   // function declaration
  if (isWhiteBoy) {
    console.log('Play: ' + music);
  }
}
funkyFunction('that funky music', true);       // call
```

1. the `function` keyword
2. the **name** (used to call it, and shown in stack traces)
3. the **parameters** inside `( )`, separated by commas (the parentheses are always required)
4. the **body** `{ }`

When you **call** it, the values you pass are called **arguments**.

### 6.2 Anonymous functions

Functions without a name, often assigned to a variable or passed directly as a callback:

```javascript
const funkyFunction = function (music, isWhiteBoy) { /* ... */ };
const funkyFunction = (music, isWhiteBoy) => { /* ... */ };  // arrow function
```

### 6.3 Arrow functions: the two rules

- With **only one parameter**, the parentheses can be omitted.
- If the body is **a single expression**, the braces can be omitted, and the result is **returned without `return`**.

```javascript
const playThe = (funky) => { return funky + " music"; };
const playThe = funky => { return funky + " music"; };
const playThe = funky => funky + " music";

const playThat = () => "funky music";   // with no parameters the () are required
```

### 6.4 Callbacks in action: `forEach`

```javascript
const notes = ['do', 're', 'me'];

notes.forEach((note) => console.log(note));
notes.forEach((note) => { console.log(note); });
notes.forEach(function (note) { console.log(note); });
notes.forEach(console.log); // passes the console.log function directly
```

### 6.5 Where does `item` come from?

Here is how `forEach` might work "under the hood":

```javascript
function myForEach(array, callback) {
  for (let i = 0; i < array.length; i++) {
    callback(array[i]); // the callback gets CALLED here
  }
}

myForEach([2, 3, 4, 2], (item) => {
  console.log(item + 2);
});
```

`item` doesn't appear from nowhere: **the receiving function (`myForEach`) calls the callback and passes it the argument**. You only declare the parameter you want to name `item`.

Another example, `map`: the callback returns a value and the function collects it into a new array.

```javascript
function myMap(array, callback) {
  const myNewArray = [];
  for (let i = 0; i < array.length; i++) {
    const callbackResult = callback(array[i]);
    myNewArray.push(callbackResult);
  }
  return myNewArray;
}

const addedArray = myMap([1, 2, 3], (arrayNum) => arrayNum + 2); // [3, 4, 5]
```

### 6.6 Passing a function declared elsewhere

```javascript
function printItemPlusTwo(item) {
  console.log(item + 2);
}
myForEach([2, 3, 4, 2], printItemPlusTwo); // no () after the name!
```

**Golden rule:** pass the function **by name, without parentheses**. With `printItemPlusTwo()` the function would run immediately and you'd pass its **result** (`undefined`), not the function.

### 6.7 A note on arrow functions and `this`

The article says to ignore `this` behavior in arrow functions for now. The comments add that arrow functions **have no `this` of their own**: they inherit it from the scope where they are defined. This makes them handy as callbacks inside object methods, whereas a regular function loses that `this`. When starting out, this is not a problem.

---

## 7. Events: three ways to handle them

An **event** is something that happens in the browser (a click, the mouse moving, a page loading). You can react by running a function, called an **event handler** or **listener**. The sources show three ways, from least to most recommended.

### Method 1: HTML attribute

```html
<button onclick="alert('Hello World')">Click Me</button>
```

It mixes JS into HTML, and each element can only have **one** `onclick`.

### Method 2: `on<event>` property in JavaScript

```javascript
const btn = document.querySelector("#btn");
btn.onclick = () => alert("Hello World");
```

The JS is out of the HTML, but you're still limited to **one handler per event**.

### Method 3: `addEventListener` (the preferred one)

```javascript
const btn = document.querySelector("#btn");
btn.addEventListener("click", () => {
  alert("Hello World");
});
```

It keeps HTML and JS separate and allows **multiple listeners** on the same element.

### With named functions

All three methods also work with functions declared elsewhere, which is useful if the same function is needed in several places:

```javascript
function alertFunction() {
  alert("YAY! YOU DID IT!");
}
btn.onclick = alertFunction;                    // method 2
btn.addEventListener("click", alertFunction);   // method 3
// method 1: <button onclick="alertFunction()">
```

### Multiple listeners on the same element

With `addEventListener` you can register different listeners:

```javascript
let btn = document.querySelector('#btn');

function handleClick() { alert('It was clicked!'); }
btn.addEventListener('click', handleClick);
```

### Listeners on a group of nodes

To add a listener to several elements, loop over the NodeList:

```javascript
const buttons = document.querySelectorAll("button");

buttons.forEach((button) => {
  button.addEventListener("click", () => {
    alert(button.id);
  });
});
```

(Later, event delegation will show an alternative that needs only one listener.)

### Useful events

`click`, `dblclick`, `keydown`, `keyup`. The full list is on the W3Schools JavaScript Event Reference page.

---

## 8. The `event` object

When an event happens, the browser passes an **Event** object to the callback. The parameter name (`e`, `event`) is free: JavaScript knows it is an event because **a listener's callback receives an `Event` object by definition**.

```javascript
btn.addEventListener("click", function (e) {
  console.log(e);          // the event object
  console.log(e.target);   // the DOM node where the event happened
  e.target.style.background = "blue";
});
```

The object only exists **inside the handler**: once all handlers have run, it is destroyed.

| Property / method | Meaning |
|---|---|
| `type` | the event type (`'click'`) |
| `target` | the element the event started on |
| `currentTarget` | the element the listener is currently running on |
| `bubbles` | `true` if the event bubbles |
| `cancelable` | `true` if the default behavior can be canceled |
| `defaultPrevented` | `true` if `preventDefault()` has been called |
| `detail` | extra information about the event |
| `eventPhase` | 1 = capturing, 2 = target, 3 = bubbling |
| `preventDefault()` | cancels the default behavior (only if `cancelable`) |
| `stopPropagation()` | stops further capturing/bubbling (only if `bubbles`) |

---

## 9. Event flow

Given this HTML:

```html
<body>
  <div id="container">
    <button id="btn">Click Me!</button>
  </div>
</body>
```

when you click the button, the event doesn't stay there: it travels through the page.

### Bubbling (bottom to top)

The event starts at the **most specific** element and **rises** toward the least specific:

`button → div#container → body → html → document` (modern browsers go up to `window`)

### Capturing (top to bottom)

The opposite path: `document → html → body → div#container → button`.

### The DOM Level 2 model: three phases

1. **Capturing phase**: from the top of the page down to the element.
2. **Target phase**: the event reaches the clicked element.
3. **Bubbling phase**: the event rises back up.

This lets you catch the event **early** (capturing), **late** (bubbling), or **stop it** in either phase with `stopPropagation()`.

---

## 10. `preventDefault()` and `stopPropagation()`

These are two **different** things, and they are often confused.

### `preventDefault()`: cancels the default action

```html
<a href="https://www.javascripttutorial.net/">JS Tutorial</a>
```

```javascript
let link = document.querySelector('a');

link.addEventListener('click', function (event) {
  console.log('clicked');
  event.preventDefault(); // the browser does NOT navigate to the href
});
```

It does **not** stop propagation: the event keeps rising. It only works if `cancelable` is `true`.

### `stopPropagation()`: stops the flow

```javascript
let btn = document.querySelector('#btn');

btn.addEventListener('click', function (event) {
  console.log('The button was clicked!');
  event.stopPropagation();
});

document.body.addEventListener('click', function (event) {
  console.log('The body was clicked!'); // NEVER runs
});
```

Without `stopPropagation()` you would see two messages in the console. It does **not** cancel the browser's default behavior.

---

## 11 Mouse events

### 11.1 The events

DOM Level 3 defines these events: `mousedown`, `mouseup`, `click`, `dblclick`, `mousemove`, `mouseover`, `mouseout`, `mouseenter`, `mouseleave`, `wheel`.

### 11.2 Sequence of a click

A click fires three events in order:

1. `mousedown` (you press the button on the element)
2. `mouseup` (you release it on the element)
3. `click` (one `mousedown` and one `mouseup` were detected on the same element)

If you press on an element, move the cursor off it and release, only `mousedown` fires and `click` **never** fires. The reverse also holds (only `mouseup`).

### 11.3 `dblclick`

Rarely used. The full sequence is `mousedown, mouseup, click, mousedown, mouseup, click, dblclick`. The `click` events **always** come before `dblclick`, so if you register both on the same element you can't tell a single click from a double click.

### 11.4 `mousemove`

Fires **many times per second** (even for a single pixel). If the handler is heavy it can cause performance problems. Two strategies:

```javascript
element.onmousemove = mouseMoveEventHandler;
// ...when no longer needed:
element.onmousemove = null;
```

or, if you need it continuously, use **throttling or debouncing**.

### 11.5 `wheel`

Fires when you scroll the mouse wheel or touchpad:

```javascript
element.addEventListener('wheel', e => console.log(e.deltaY));
```

### 11.6 `mouseover/mouseout` vs `mouseenter/mouseleave`

| Event | Fires when... | Bubbles |
|---|---|---|
| `mouseover` | the pointer enters the element **or any of its children** | yes |
| `mouseout` | the pointer leaves the element **or any of its children** | yes |
| `mouseenter` | the pointer enters **the element itself only** | no |
| `mouseleave` | the pointer leaves **the element itself only** | no |

If you don't want repeated events while the mouse moves over child elements, use `mouseenter/mouseleave`. All the other mouse events (`click`, `dblclick`, `mousedown`, `mouseup`, `mousemove`, `wheel`) bubble.

### 11.7 Which button was pressed: `event.button`

| Value | Button |
|---|---|
| 0 | main (usually left) |
| 1 | auxiliary (wheel / middle) |
| 2 | secondary (usually right) |
| 3 | fourth (usually browser Back) |
| 4 | fifth (usually browser Forward) |

```html
<button id="btn">Click me with any mouse button</button>
<p id="message"></p>

<script>
  let btn = document.querySelector('#btn');

  // disable the context menu on right click
  btn.addEventListener('contextmenu', (e) => {
    e.preventDefault();
  });

  btn.addEventListener('mouseup', (e) => {
    let msg = document.querySelector('#message');
    switch (e.button) {
      case 0: msg.textContent = 'Left mouse button clicked.'; break;
      case 1: msg.textContent = 'Middle mouse button clicked.'; break;
      case 2: msg.textContent = 'Right mouse button clicked.'; break;
      default: msg.textContent = `Unknown mouse button code: ${e.button}`;
    }
  });
</script>
```

> In the original example, the `default` case uses `event.button` instead of `e.button`: `event` is not defined at that point. I fixed it here.

### 11.8 Modifier keys

During a click you can hold Shift, Ctrl, Alt, Meta (the Windows key on Windows, Command on Mac). The event object has four booleans: `shiftKey`, `ctrlKey`, `altKey`, `metaKey`.

```javascript
btnKeys.addEventListener('click', (e) => {
  let keys = [];
  if (e.shiftKey) keys.push('shift');
  if (e.ctrlKey)  keys.push('ctrl');
  if (e.altKey)   keys.push('alt');
  if (e.metaKey)  keys.push('meta');

  document.querySelector('#messageKeys').textContent = `Keys: ${keys.join('+')}`;
});
```

### 11.9 Mouse coordinates

- `screenX` / `screenY`: position relative to the **entire screen**.
- `clientX` / `clientY`: position relative to the **application's visible area** (the viewport).

```javascript
track.addEventListener('mousemove', (e) => {
  log.innerText = `
    Screen X/Y: (${e.screenX}, ${e.screenY})
    Client X/Y: (${e.clientX}, ${e.clientY})`;
});
```

---

## 12. Keyboard events

### 12.1 The three events

- `keydown`: when you press a key; repeats while the key is held down.
- `keyup`: when you release the key.
- `keypress`: when you press a **character** key (`a`, `b`, `c`), not arrows, Home, End and the like; this one repeats too.

They are usually listened for on a text box, but all elements support them.

### 12.2 Firing order

- **Character key:** `keydown → keypress → keyup`. `keydown` and `keypress` fire **before** the text changes; `keyup` fires **after**.
- **Non-character key:** only `keydown → keyup`.

### 12.3 Registering listeners

```html
<input type="text" id="message">
```

```javascript
let msg = document.getElementById('message');

msg.addEventListener("keydown", (event) => { /* ... */ });
msg.addEventListener("keypress", (event) => { /* ... */ });
msg.addEventListener("keyup", (event) => { /* ... */ });
```

> The original example has `getElementById('#message')`: with the `#` it would find nothing. `getElementById` wants the id **without** `#` (unlike `querySelector`).

### 12.4 `key` and `code`

- `event.key`: the **character** produced by the key.
- `event.code`: the **physical key** on the keyboard.

Pressing `z`: `key=z, code=KeyZ`.

```javascript
textBox.addEventListener('keydown', (event) => {
  console.log(`key=${event.key},code=${event.code}`);
});
```

---

## 13. Event delegation

### 13.1 The problem

```html
<ul id="menu">
  <li><a id="home">home</a></li>
  <li><a id="dashboard">Dashboard</a></li>
  <li><a id="report">report</a></li>
</ul>
```

One listener per item works, but with many elements it gets heavy:

- every handler is a function, i.e. an **object in memory**: more objects, slower performance;
- assigning all the handlers **takes time** and delays the page's interactivity.

### 13.2 The solution

You exploit **bubbling**: a single listener on the **parent** that recognizes the clicked element through `event.target`.

```javascript
let menu = document.querySelector('#menu');

menu.addEventListener('click', (event) => {
  let target = event.target;

  switch (target.id) {
    case 'home':      console.log('Home menu item was clicked'); break;
    case 'dashboard': console.log('Dashboard menu item was clicked'); break;
    case 'report':    console.log('Report menu item was clicked'); break;
  }
});
```

**Definition:** event delegation is the technique of using bubbling to handle an event at a higher level in the DOM than the element it originated on.

### 13.3 Benefits

- less memory and better performance;
- less time to set up handlers;
- if the listener is on `document`, it is available immediately: no need to wait for `DOMContentLoaded` or `load`.

---

## 14. Generating events: `Event` and `dispatchEvent()`

Events usually come from the user, but you can also create them in code in two steps: **create** the event with a constructor, then **fire** it on an element.

### 14.1 The `Event` constructor

```javascript
let event = new Event(type, [options]);
```

- `type`: a string with the type (`'click'`).
- `options`: an object with two optional properties, `bubbles` and `cancelable`. The defaults are `{ bubbles: false, cancelable: false }`.

### 14.2 `dispatchEvent()`

```html
<button class="btn">Test</button>
```

```javascript
let btn = document.querySelector('.btn');

btn.addEventListener('click', function () {
  alert('Mouse Clicked');
});

let clickEvent = new Event('click');
btn.dispatchEvent(clickEvent); // the handler runs as if you had clicked
```

### 14.3 `isTrusted`

`event.isTrusted` is `true` if the event comes from the user and `false` if it was generated by code. It is used to check an event's authenticity.

### 14.4 Specialized constructors

`Event` is the base type of `UIEvent`, from which `MouseEvent`, `TouchEvent`, `FocusEvent` and `KeyboardEvent` derive. It is good practice to use the **specific** one, because it offers extra properties:

```javascript
let clickEvent = new MouseEvent("click", {
  bubbles: true,
  cancelable: true,
  clientX: 150,
  clientY: 150
});
```

---

## 15. Custom events

Standard events (`click`, `input`, `submit`) are fired by the browser. **Custom events** are ones **you define and fire yourself**, creating a communication channel between different parts of your app.

### 15.1 The starting point: the callback

```javascript
function highlight(elem, callback) {
  elem.style.backgroundColor = 'yellow';

  if (callback && typeof callback === 'function') {
    callback(elem);
  }
}

function addBorder(elem) {
  elem.style.border = "solid 1px red";
}

highlight(note, addBorder);
```

It works, but `highlight` has to **know** who to call afterwards. With a custom event, that link disappears.

### 15.2 Creating: `CustomEvent`

```javascript
let event = new CustomEvent(eventType, options);
```

- `eventType`: the name of the event.
- `options`: an object with the `detail` property, where you put the data you want to carry.

`CustomEvent` inherits from `Event` and adds `detail`.

```javascript
let event = new CustomEvent('mark', {
  detail: { backgroundColor: 'yellow' }
});
```

### 15.3 Firing: `dispatchEvent()`

```javascript
domElement.dispatchEvent(event);
```

### 15.4 Full example

```html
<div class="note">JS Custom Event</div>
<script>
  function highlight(elem) {
    const bgColor = 'yellow';
    elem.style.backgroundColor = bgColor;

    let event = new CustomEvent('mark', {
      detail: { backgroundColor: bgColor }
    });
    elem.dispatchEvent(event);   // fires the event
  }

  let div = document.querySelector('.note');

  function addBorder(elem) {
    elem.style.border = "solid 1px red";
  }

  // listen for the custom event
  div.addEventListener('mark', function (e) {
    addBorder(this);
    console.log(e.detail);   // { backgroundColor: 'yellow' }
  });

  highlight(div);
</script>
```

`highlight()` no longer knows anything about `addBorder`: it just announces "I marked the element".

### 15.5 Why use them

They let you **decouple** code: one piece of code runs after another finishes, without the two knowing about each other. You can put the listeners in a separate file and have **multiple listeners** for the same custom event.

---
