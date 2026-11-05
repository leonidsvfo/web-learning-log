

## Flexbox

### `display: flex`

The main idea behind the flex layout is to give the container the ability to alter its items' width/height (and order) to best fill the available space (mostly to accommodate all kinds of display devices and screen sizes). We use flexbox to organize items into rows or columns. These items will grow or shrink based on rules that you define. Adding a `<div>` will show another box alongside the others, and everything will flex to fit within the available area.

```html
<div class="flex-container">
  <div class="one"></div>
  <div class="two"></div>
  <div class="three"></div>
  <div class="four"></div>
</div>
```

```css
.flex-container {
  display: flex;
}

/* this selector selects all divs inside of .flex-container */
.flex-container div {
  background: peachpuff;
  border: 4px solid brown;
  height: 100px;
  width: 100px;
  /* flex: 1; */
}
```

### Flex containers and flex items

Flex is more than just a property; it is a toolbox of properties where some of them belong on the flex container and some go on the flex items. A **flex container** is any element that has `display: flex` on it. A **flex item** is any element that is inside of that container.

```css
.container {
  background-color: aqua;
  padding: 12px;
  border: 4px solid blue;
  display: flex;
}

.item {
  background-color: peachpuff;
  border: 4px solid salmon;
  height: 48px;
  flex: 1;
  margin: 4px;
}
```

Any element can be at the same time a flex container and a flex item, when you code `display: flex` inside them.

### Flex shorthand

The `flex` declaration is a shorthand for 3 properties that you can set on a flex item; they affect how flex items size themselves within their container, in this case: `flex-grow`, `flex-shrink` and `flex-basis` (`flex: 1 1 0`). So basically these values are needed when you resize your browser window, so that your boxes are going to resize equally.

#### `flex-grow`

By default, elements in a Flexbox context will shrink down to their minimum comfortable size along the primary axis. `flex-grow` is a single number value; that value is the grow factor. If you apply `flex: 1` to the divs inside a container, every div will grow the same amount. If you add `flex: 3` to just one div, then that div would grow to 3× the size of the others. The default value is 0. `flex-grow` controls how the **extra space is distributed** when the items are smaller than their container.

#### `flex-shrink`

Similar to `flex-grow`, but sets the shrink factor of a flex element. `flex-shrink` only ends up being applied if the size of all flex items is larger than their parent container. The default value is 1. `flex-shrink` controls how **space is removed** when the items are bigger than their container. When you don't want some of your items to shrink, you can set `flex-shrink: 0` on those flex children.

#### `flex-basis`

`flex-basis` sets the initial size of a flex item, so any sort of `flex-grow` or `flex-shrink` starts from that baseline width, pegged to the **primary axis**. The initial value of the property is `auto`, which tells the item to check for a width declaration. When you use the `flex` shorthand with a single number (like `flex: 1`), the basis becomes 0%: if you don't set it to `auto`, those items would ignore the item's width, and everything would be sized evenly.

`flex: auto` sets your flex values like this: `flex: 1 1 auto`. `flex: 1` = `1 1 0%`. In practice you will likely not be using complex values for `flex-grow`, `flex-shrink` or `flex-basis`. Generally, you're most likely to use declarations like `flex: 1;` to make divs grow evenly and `flex-shrink: 0` to keep certain divs from shrinking.

### `flex-direction`

The `flex-direction` property enables you to define how flex items are placed in a flex container. The default direction for a flex container is horizontal, or `row`; you can change it to vertical, or `column`, with `flex-direction: column`. This link explores more: <https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/flex-direction>.

```css
.container {
  display: flex;
  flex-direction: column; /* default: row */
}
```

### Alignment

So, putting `display: flex` in the container and `flex: 1` on the items makes each of the elements grow and shrink equally. But if you want them to stay at the same width, with space between them, you should delete `flex: 1` and add `justify-content: space-between` to the container.

If you want them united in the center you can use `justify-content: center`.

```css
.container {
  display: flex;
  justify-content: space-between; /* or: center */
}
```

Setting `gap` on a flex container adds a specified space between flex items, similar to adding a margin to the items themselves.

We can bunch all the items up in a particular spot (with `flex-start`, `center`, and `flex-end`), or we can spread them apart (with `space-between`, `space-around`, and `space-evenly`).

#### `align-self`

Unlike `justify-content` and `align-items`, `align-self` is applied to the *child element*, not the container. It allows us to change the alignment of a specific child along the cross axis.

#### Vocabulary

- **justify** — to position something along the **primary axis**.
- **align** — to position something along the *cross axis*.
- **content** — a group of "stuff" that can be distributed.
- **items** — single items that can be positioned individually.

#### `min-width`

By setting `min-width: 0px` directly on the Flexbox child, we tell the Flexbox algorithm to overwrite the "built-in" minimum width.

#### `flex-wrap`

- `flex-wrap: wrap` gives us two rows of stuff.
- Within each row, `align-items` lets us slide each individual child up or down.
- Zooming out, however, we have these two rows within a single Flexbox context! The cross axis will now intersect **two** rows, not one. And so, we can't move the rows individually; we need to distribute them *as a group*.
- Using our definitions from above, we're dealing with **content**, not **items**. But we're also still talking about the cross axis! And so the property we want is `align-content`.

---

# Chapter IV – What Is JavaScript?

## How the code works

A computer's processor understands only machine code: sequences of 0s and 1s (binary). Each 0 or 1 is a bit, representing an electrical signal that is off or on. Every instruction and every piece of data, whether text, images or programs, is ultimately stored and processed in this form.

Humans can't write programs comfortably in binary, so we write code in programming languages that are readable to us. This code must be translated into machine code before the processor can act on it.

### What a compiler is

A compiler is a program that translates source code (written in a programming language) into machine code, or into another lower-level form that can be executed. Depending on the language, this translation can happen ahead of time, before the program runs (as in C), or during execution, as in just-in-time (JIT) compilation (as in modern JavaScript engines).

### Compiled vs interpreted

**Compiled (C, C++)**

A program called a compiler translates all your code into machine code once, ahead of time. The result is an executable binary file. Whoever uses it receives only that file, and the processor runs it directly. The source code is no longer needed.

**Interpreted (e.g. JavaScript)**

No binary is produced in advance. The browser already contains a program called a JavaScript engine (Chrome's is called V8), which is itself compiled into machine code. When the browser receives your JavaScript as text, the engine reads it and carries out the corresponding actions as it goes. Your code never becomes a binary of its own: the engine, already in 0s and 1s, does the things your code describes.

**An analogy:** you need someone who only speaks Japanese to follow instructions.

- *Compiled:* you translate the whole instruction manual into Japanese beforehand and hand it over. They read it directly.
- *Interpreted:* you hire an interpreter who stands next to them and translates sentence by sentence while they work. The instructions stay in Italian, but the interpreter turns them into Japanese on the fly.

**So how does the browser understand JavaScript?** The JavaScript engine is already installed in the browser and is made of 0s and 1s. Your JavaScript travels over the network as plain text (which is also 0s and 1s, but only as data, like any text file). The engine then interprets its meaning and turns it into actions the processor can perform.

**Why is JavaScript called "not compiled"?** Because the distinction is about workflow, not physics:

- In C: write, compile, distribute the binary, someone runs it.
- In JavaScript: write, distribute the text, and the engine translates and runs it on the spot, every time.

## JavaScript

JavaScript is a scripting or programming language that allows you to implement complex features on web pages. Without JavaScript, your webpage, with only HTML and CSS, would be a static information page. JavaScript is what makes your website interactive: content updates, interactive maps, animated 2D/3D graphics, scrolling systems, etc. The three layers build on top of one another:

- [HTML](https://developer.mozilla.org/en-US/docs/Glossary/HTML) is the markup language that we use to structure and give meaning to our web content, for example defining paragraphs, headings, and data tables, or embedding images and videos in the page.
- [CSS](https://developer.mozilla.org/en-US/docs/Glossary/CSS) is a language of style rules that we use to apply styling to our HTML content, for example setting background colors and fonts, and laying out our content in multiple columns.
- [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript) is a scripting language that enables you to create dynamically updating content, control multimedia, animate images, and pretty much everything else. (Okay, not everything, but it is amazing what you can achieve with a few lines of JavaScript code.)

### Application Programming Interfaces (APIs)

APIs are ready-made sets of code blocks that allow a developer to implement programs that would otherwise be hard or impossible to implement. They work like IKEA ready-made furniture kits: you have already cut panels that you can screw together to make a bookshelf; you don't need to find the wood yourself, get measures, cut all the panels to the right size and shape, etc.

**Browser APIs** are built into your web browser, and are able to expose data from the surrounding computer environment and do useful things for the developer:

- The **DOM (Document Object Model) API** allows you to manipulate HTML and CSS, creating, removing and changing HTML;
- The **Geolocation API** retrieves geographical information, like in Google Maps;
- The **Canvas** and **WebGL** APIs allow you to create animated 2D and 3D graphics;
- **Audio** and **Video APIs** like **HTMLMediaElement** and **WebRTC** allow you to customize things with multimedia, like playing audio and video in the webpage, or showing your webcam and displaying it on someone else's PC.

**Third-party APIs** are not built into the browser by default; you can grab their code from somewhere, like:

- The **Bluesky API** allows you to do things like displaying your latest posts on your website;
- The **Google Maps API** and **OpenStreetMap API** allow you to embed custom maps into your website, and other functionality.

### What is JavaScript doing on your page: brief recap

When you load a web page in a browser, you are running your code (HTML, CSS, JavaScript) inside an execution environment (the browser tab). It takes raw materials (the code) and outputs a product: the web page. It is a common habit to use JavaScript to modify HTML and CSS via the DOM API.

### Browser security

Each browser tab has its own separate blocks of code called "execution environments". So each tab runs separately, and they can't affect each other. This is a good security measure; if this were not the case, then pirates could start writing code to steal information from other websites.

### JavaScript running order

When the browser encounters a block of JavaScript, it generally runs it in order, from top to bottom. This means that you need to be careful about what order you put things in.

## Adding JavaScript to a page

### Internal JavaScript

For the foundations of JavaScript, it is recommended to use internal JavaScript, through the browser. To start, you need to put this at the end of your `<body>`:

```html
<script>
  console.log("Hello, World!")
</script>
```

Your code won't work if the JavaScript is loaded and parsed before the HTML, and errors could happen if you put it before the end of the body.

Save and open it in a live browser, so to begin you should write your code directly in your browser:

- Press F12;
- Find and select the "Console" tab, where you should see the output of our `console.log` statement.

`console.log` is the command to print something to the developer console in your browser.

### External JavaScript

Another way to include JavaScript in a webpage is through an external script:

```html
<script src="javascript.js"></script>
```

External scripts are used for more complex scripts, but for now it is recommended to use the internal method, through the browser.

### Comments

Before you start learning to code, it is good practice to remember to leave comments in your code. Comments do not affect how the code runs, but they can be very useful for giving instructions to other developers and for yourself. To write a comment you will use this form:

```javascript
// I am a comment

/* I am also a comment */
```

---

# Chapter V – Variables Foundations

Variables are the building blocks of any program: they are storage containers for data in your code.

```javascript
let firstName = "John";
```

- `let` is the declaration. It creates a new name;
- `firstName` is the name of the variable;
- `=` is the assignment operator. It connects the name to a value;
- `"John"` is the value. Because it is surrounded by quotes, its type is a string.

Using `console.log()` you ask a program for an output; in this case it would be:

```javascript
console.log(firstName); // John
```

You can also re-assign variables:

```javascript
firstName = "Ethan";
console.log(firstName); // Ethan
```

We can also declare two variables and copy data from one into the other:

```javascript
let hello = 'Hello world!';
let message;

message = hello;
```

Since the variable has already been declared earlier, we don't need to use `let` again.

If we want a constant variable which will never need to be re-assigned, we can use the `const` keyword:

```javascript
const pi = 3.14;
pi = 10; // TypeError: Assignment to constant variable.
```

If you try to re-assign the constant, an error is going to pop up. In old-school code you will quite probably find `var` instead of `let`, but they are very similar, with some different quirks.

## Variable naming

There are limitations on variable names in JavaScript:

1. The name must contain only letters, digits, or the symbols `$` and `_`.
2. The first character must **not** be a digit.
3. There is a list of reserved words, which cannot be used as variable names, like: `let`, `class`, `return`, `function`.

## Write clean code

A variable name should have a clean, obvious meaning, describing the data that it stores. Variable naming is one of the most important skills in programming. In a real project, most of the time is spent modifying and extending an existing code base, so it is always recommended to make it clear for everybody.

Some good-to-follow rules are:

- Use human-readable names like `userName` or `shoppingCart`.
- Stay away from abbreviations or short names like `a`, `b`, and `c`, unless you know what you're doing.
- Make names maximally descriptive and concise. Examples of bad names are `data` and `value`. Such names say nothing. It's only okay to use them if the context of the code makes it exceptionally obvious which data or value the variable is referencing.
- Agree on terms within your team and in your mind. If a site visitor is called a "user", then we should name related variables `currentUser` or `newUser` instead of `currentVisitor` or `newManInTown`.

For the sake of better readability you should use a single line per variable, and not something like this (that would still run the code):

```javascript
let user = 'John', age = 25, message = 'Hello';
```

You should use one of these multiline variants:

```javascript
let user = 'John';
let age = 25;
let message = 'Hello';
```

```javascript
let user = 'John',
  age = 25,
  message = 'Hello';
```

```javascript
let user = 'John'
  , age = 25
  , message = 'Hello';
```

## Operators

An operator is a special symbol or keyword used to perform operations on values and variables (called **operands**). The most common operators in JavaScript are:

### Arithmetic (math)

- `+` add: `5 + 2 = 7`
- `-` subtract: `5 - 2 = 3`
- `*` multiply: `5 * 2 = 10`
- `/` divide: `5 / 2 = 2.5`
- `%` remainder (modulo): `5 % 2 = 1`
- `**` power: `5 ** 2 = 25`
- `++` add 1: `x++` (x becomes x + 1)
- `--` subtract 1: `x--` (x becomes x - 1)

Numbers in JavaScript use the standard mathematical order of operations, **PEMDAS**: parentheses, exponentiation, multiplication and division, addition and subtraction. Number values are typed in without quote marks.

### Assignment (put a value in a variable)

- `=` : `x = 5` (set x to 5)
- `+=` : `x += 3` (same as `x = x + 3`)
- `-=` : `x -= 3` (same as `x = x - 3`)
- `*=` : `x *= 3` (same as `x = x * 3`)
- `/=` : `x /= 3` (same as `x = x / 3`)

### Comparison (give back true or false)

- `===` strictly equal: `5 === 5 // true`, `"5" === 5 // false`
- `!==` strictly not equal: `5 !== 3 // true`
- `>` greater than: `5 > 3 // true`
- `<` less than: `5 < 3 // false`
- `>=` greater or equal: `5 >= 5 // true`
- `<=` less or equal: `3 <= 5 // true`

### Assignment operators

Assignment operators are operators that assign a value to a variable.

```javascript
let x = 3; // x contains the value 3
let y = 4; // y contains the value 4

x = y;     // x now contains the same value y contains, 4
```

#### Chaining assignments

```javascript
let a, b, c;

a = b = c = 2 + 2;

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

### Increment / decrement

The operators `++` and `--` can be placed either before or after a variable.

- When the operator goes after the variable, it is in "postfix form": `counter++`.
- The "prefix form" is when the operator goes before the variable: `++counter`.

Both of these statements do the same thing: increase `counter` by `1`.

If we'd like to increase a value **and** immediately use the result of the operator, we need the prefix form:

```javascript
let counter = 0;
alert( ++counter ); // 1
```

If we'd like to increment a value but use its previous value, we need the postfix form:

```javascript
let counter = 0;
alert( counter++ ); // 0
```

### [Remainder `%`](https://javascript.info/operators#remainder)

The remainder operator `%`, despite its appearance, is not related to percents.

```javascript
alert( 8 % 3 ); // 2, the remainder of 8 divided by 3
```

### [Exponentiation `**`](https://javascript.info/operators#exponentiation)

The exponentiation operator `a ** b` raises `a` to the power of `b`.

```javascript
alert( 2 ** 2 ); // 2² = 4
```

### String concatenation with binary `+`

If the binary `+` is applied to strings, it merges (concatenates) them:

```javascript
let s = "my" + "string";
alert(s); // mystring
```

Note that if any of the operands is a string, then the other one is converted to a string too.

```javascript
alert( '1' + 2 );     // "12"
alert( 2 + '1' );     // "21"
alert( 2 + 2 + '1' ); // "41" and not "221"
alert( '1' + 2 + 2 ); // "122" and not "14"
```

If the first operand is a string, the compiler treats the other two operands as strings too. The 2 gets concatenated to '1', so it's like '1' + 2 = "12" and "12" + 2 = "122".

The binary `+` is the **only** operator that supports strings in such a way. Other arithmetic operators work only with numbers and always convert their operands to numbers.

The need to convert strings to numbers arises very often. For example, if we are getting values from HTML form fields, they are usually strings. What if we want to sum them?

The binary plus would add them as strings:

```javascript
let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23", the binary plus concatenates strings
```

If we want to treat them as numbers, we need to convert and then sum them:

```javascript
let apples = "2";
let oranges = "3";

alert( +apples + +oranges ); // 5
```

#### Concatenation using `+`

You can concatenate normal strings using the `+` operator:

```javascript
const greeting2 = "Hello";
const name2 = "Bob";
console.log(greeting2 + ", " + name2); // "Hello, Bob"
```

However, template literals (using `${}`) usually give you more readable code:

```javascript
const greeting3 = "Howdy";
const name3 = "Ramesh";
console.log(`${greeting3}, ${name3}`); // "Howdy, Ramesh"
```

### Bitwise operators (mostly used in cryptography)

- AND (`&`)
- OR (`|`)
- XOR (`^`)
- NOT (`~`)
- LEFT SHIFT (`<<`)
- RIGHT SHIFT (`>>`)
- ZERO-FILL RIGHT SHIFT (`>>>`)

### Comma operator

The comma operator allows us to evaluate several expressions, dividing them with a comma `,`. Each of them is evaluated but only the result of the last one is returned.

```javascript
let a = (1 + 2, 3 + 4);

alert( a ); // 7 (the result of 3 + 4)
```

**Comma has a very low precedence!** Please note that the comma operator has very low precedence, lower than `=`, so parentheses are important in the example above. Without them: `a = 1 + 2, 3 + 4` evaluates `+` first, summing the numbers into `a = 3, 7`, then the assignment operator `=` assigns `a = 3`, and the rest is ignored. It's like `(a = 1 + 2), 3 + 4`.

---

# Chapter VI – Data Types and Conditionals

A data type is a collection or grouping of data **values**, usually specified by a set of possible values, a set of allowed operations on these values, and/or a representation of these values as machine types. The most common types of data are numbers and strings.

## Number type

In JavaScript, the number type cannot safely represent integers larger than (2<sup>53</sup> − 1) or less than −(2<sup>53</sup> − 1). But sometimes, for cryptography perhaps, we would need larger numbers. For that we have the ***BigInt*** type, which goes even further.

## String type

A string, as we said before, is information surrounded by quotes:

```javascript
let str = "Hello";
```

**NOTE:** In some languages, there is a special "character" type for a single character. For example, in the C language and in Java it is called "char". In JavaScript, there is no such type. There's only one type: *string*. A string may consist of zero characters (be empty), one character or many of them.

## Logical type: Boolean

The boolean type has only two values: `true` and `false`.

```javascript
let isGreater = 4 > 1;
alert( isGreater ); // true (the comparison result is "yes")
```

```javascript
let nameFieldChecked = true; // yes, name field is checked
let ageFieldChecked = false; // no, age field is not checked
```

## Special values

### `undefined`

The special value `undefined` means "value is not assigned":

```javascript
let age;

alert(age); // shows "undefined"
```

### `null`

It's a special value which represents "nothing", "empty" or "value unknown".

### Symbol

The `symbol` type is used to create unique identifiers for objects.

## The `typeof` operator

The `typeof` operator returns the type of the operand:

```javascript
typeof undefined // "undefined"
typeof 0 // "number"
typeof 10n // "bigint"
typeof true // "boolean"
typeof "foo" // "string"
typeof Symbol("id") // "symbol"
```
