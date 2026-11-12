# Events vs Properties in JavaScript

## Core Difference

| | Event | Property |
|---|---|---|
| What it is | Something that happens over time (a user action) | A piece of data stored inside an object |
| Answers | *"When?"* | *"Which / how much / what is it like?"* |
| Example | `"keydown"` | `event.key` |
| Where it is used | As an argument of `addEventListener` | After the dot, on an object |

**Summary:** An event (`"keydown"`) is a string name that tells the browser **when** to act. A property (`event.key`) is information the browser has already written into an object, and you **read** it.

---

## Events Are Strings

`"keydown"` is always a plain string. It never turns into an action by itself. It is just text that `addEventListener` knows how to interpret as the name of an event.

The action is not in the string. It is in the **method that receives it**. The meaning depends on who receives the string, not on the string itself.

```js
console.log("keydown");
// prints the text "keydown", nothing else happens

textBox.addEventListener("keydown", logKey);
// addEventListener recognizes "keydown" as an event name and listens for it
```

### Storing the event name in a variable

A variable holding an event name is still a string. It works because `addEventListener` receives the same text.

```js
let patata = "keydown";
textBox.addEventListener(patata, logKey);   // identical to using "keydown"
```

If the variable held an unknown name such as `"pippo"`, nothing would happen, because the browser does not know that event. JavaScript does not raise an error in this case.

### Common events

| Event name | When it fires |
|---|---|
| `"keydown"` | A key is pressed |
| `"keyup"` | A key is released |
| `"click"` | The element is clicked |
| `"mouseover"` | The mouse moves over the element |
| `"submit"` | A form is submitted |

---

## Properties

A property is a labelled piece of data inside an object. It is read with the dot and **without parentheses**.

- `event` is the box (the object).
- `key` is a **label** inside the box.
- The value under that label (`"a"`, `"Enter"`) is the pressed key.

The browser creates the `event` object and fills in `key`. The programmer does not assign it, only reads it with `event.key`.

Note: `key` is the name of the label, not the key itself. In this context "key" means a **keyboard key**.

### Examples of properties

**Keyboard event object:**

```js
event.key        // "a"        the character/key pressed
event.code       // "KeyA"     the physical key
event.shiftKey   // true/false whether Shift was held
```

**String:**

```js
"ciao".length    // 4
```

**Page element (like `textBox`):**

```js
textBox.value    // the text typed inside the box
textBox.id       // the element's id
```

**Mouse event (`"click"`):**

```js
event.clientX    // horizontal position of the click
event.clientY    // vertical position of the click
```

---

## How `"keydown"` and `event.key` Relate

Nothing is transferred from `"keydown"` to `event.key`. They are linked by the fact that the event happened.

1. `addEventListener("keydown", logKey)` tells the browser: *when a keydown happens, call `logKey`*. The job of `"keydown"` ends here: it only says **when**.
2. The user presses a key.
3. The browser creates an `event` object describing that keydown, with `key` already filled in.
4. The browser calls `logKey` and passes the object into the `event` parameter.
5. Inside the function, `event.key` reads the pressed key.

**Analogy:** `"keydown"` is telling the doorman *"call me when the doorbell rings"*. `event.key` is the note the doorman brings saying **who** rang.

---

## Quick Reference

| Term | Definition | Example |
|---|---|---|
| Variable | A name that points to a value | `textBox` |
| Function | A block of code with a name that runs when called | `logKey` |
| Parameter | Placeholder name for what a function receives (written in the definition) | `event` in `function logKey(event)` |
| Argument | The actual value passed to a function (given at the call) | `"keydown"` and `logKey` in `addEventListener(...)` |
| Object | A container grouping properties and methods | `event`, `console`, `textBox` |
| Property | A data value inside an object, read without parentheses | `event.key` |
| Method | A function inside an object, called with parentheses | `console.log()`, `textBox.addEventListener()` |
| Event | A situation the browser recognizes, referred to by name as a string | `"keydown"` |

## RECAP: Line-by-Line Walkthrough

```js
const textBox = document.querySelector("input");

function logKey(event) {
  console.log(`You pressed "${event.key}".`);
}

textBox.addEventListener("keydown", logKey);
```

## Line 1: `const textBox = document.querySelector("input");`

**When it runs:** immediately, when the page loads the script.

| Part | What it is | Who chose the name |
|---|---|---|
| `const` | Keyword that creates a variable that can't be reassigned | JavaScript (fixed) |
| `textBox` | **Variable**: a name that points to a value | **Me** |
| `=` | Stores the value on the right into the variable on the left | JavaScript (fixed) |
| `document` | **Object** provided by the browser, representing the whole page | Browser (fixed) |
| `.` | "Enter the object and take this thing" | JavaScript (fixed) |
| `querySelector` | **Method** of `document`: searches the page for an element | Browser (fixed) |
| `"input"` | **Argument**: a string telling `querySelector` what to look for | The tag name is fixed by HTML |

**How it works:** `querySelector("input")` finds the text box on the page and returns it as an **object**. That object is stored in the variable `textBox`. From then on, `textBox` is the text box in the code.

---

## Line 2: `function logKey(event) {`

**When it runs:** the definition is read at load, but **the code inside does not run yet**. It runs only when the function is called.

| Part | What it is | Who chose the name |
|---|---|---|
| `function` | Keyword: "I am declaring a function" | JavaScript (fixed) |
| `logKey` | **Function** name | **Me** |
| `(event)` | **Parameter**: placeholder name for what the function will receive | **Me** (could be `pippo`) |
| `{` | Opens the function body | JavaScript (fixed) |

**How it works:** this is a recipe with a name. `event` is an empty box with a label. It gets filled **only when the function is called**.

---

## Line 3: `` console.log(`You pressed "${event.key}".`); ``

**When it runs:** every time `logKey` is called, never before.

### `console.log(...)`

| Part | What it is |
|---|---|
| `console` | **Object** provided by the browser (the developer console) |
| `.` | Enter the object |
| `log` | **Method** of `console`: a function stored inside the object |
| `( ... )` | "Execute now", holds the **argument** |

A method is **a function stored inside an object**. It is recognized by **dot + parentheses**.

### The backticks

Backticks create a **template literal**: a string that allows values to be inserted inside it. Normal quotes do not allow this.

### `${event.key}`

| Part | What it is |
|---|---|
| `${ }` | JavaScript syntax: "calculate what's inside and insert the result into the string" |
| `event.key` | The thing being calculated |

### `event.key`

| Part | What it is | Who decides the name |
|---|---|---|
| `event` | **Object**: the parameter, holding information about what happened | I chose the parameter name |
| `.` | Enter the object | Fixed |
| `key` | **Property**: a labelled data value inside the object, holding the pressed key (`"a"`, `"Enter"`, `"5"`) | **The browser** (must be written exactly) |

- No parentheses, so it is a property: a value is **read**, nothing is executed.
- "key" means a **keyboard key**.
- Nobody assigns `key`. **The browser creates the `event` object and fills in `key` before calling the function.** The code only reads it.

### The rest of the string

`You pressed "` and `".` are plain text, printed as they are.

**Result:** if the user pressed `a`, the console prints `You pressed "a".`

---

## Line 4: `}`

Closes the function body. Everything between `{` and `}` runs when the function is called.

---

## Line 5: `textBox.addEventListener("keydown", logKey);`

**When it runs:** once, at page load. It **registers** the function and prints nothing.

| Part | What it is | Who chose the name |
|---|---|---|
| `textBox` | The **object** (the text box) stored in the variable | Me (variable name) |
| `.` | Enter the object | Fixed |
| `addEventListener` | **Method** of `textBox`: "start listening for something on me" | Browser (fixed) |
| `"keydown"` | **Argument 1**: a **string** that is the **name of an event** | Browser (fixed, must exist) |
| `,` | Separates the two arguments, nothing else | Fixed |
| `logKey` | **Argument 2**: the **function** to call when the event happens | Me (name from line 2) |

### Key details

- **`"keydown"` is just a string.** `addEventListener` interprets it as an event name because it is the method that receives it. It answers only **"when?"**. A typo (`"keydwon"`) gives no error: it simply never fires.
- **`logKey` has no parentheses.** Without them, the function itself is passed ("call it yourself later"). With `logKey()` it would run immediately, which is wrong here.
- **Nothing is transferred from `"keydown"` to `event.key`.** They are linked only by the fact that the event happened.

---

## What Happens Over Time

| Step | When | What happens |
|---|---|---|
| 1 | Page load | `textBox` points to the text box object |
| 2 | Page load | `logKey` is defined but not run |
| 3 | Page load | `addEventListener` registers: "on keydown in this box, call `logKey`". Nothing is printed |
| 4 | User presses `a` | The browser notices the **event** `keydown` |
| 5 | Immediately | The browser **creates a new `event` object** with `key: "a"` and other properties |
| 6 | Immediately | The browser **calls `logKey`** and passes the object into the parameter `event` (argument → parameter) |
| 7 | Inside the function | `event.key` reads `"a"` |
| 8 | Inside the function | `console.log` prints `You pressed "a".` |
| 9 | User presses another key | Steps 4 to 8 repeat with a **new** `event` object |

**Analogy:** `"keydown"` is telling the doorman *"call me when the doorbell rings"*. `event.key` is the note the doorman brings saying **who** rang.

---

## Who Decided Each Name

**Invented by me (can be changed, but everywhere they appear):**
- `textBox` (variable)
- `logKey` (function)
- `event` (parameter)
- the text `You pressed ...`

**Decided by JavaScript or the browser (must be exact):**
- `const`, `function`
- `document`, `querySelector`
- `console`, `log`
- `addEventListener`
- `"keydown"` (event name)
- `key` (property of the event object)

**Test:** if renaming a word still works (as long as it is renamed everywhere), it was invented. If it breaks, it has a fixed meaning.

---

## Property vs Method

| | Property | Method |
|---|---|---|
| Contains | A **data value** | A **function** |
| Used with | Dot, **no** parentheses | Dot, **with** parentheses |
| Meaning | Read a piece of information (a noun) | Execute an action (a verb) |
| Examples | `event.key`, `"ciao".length`, `textBox.value` | `console.log()`, `textBox.addEventListener()`, `"ciao".toUpperCase()` |

The dot always means "enter the object and take this thing". The parentheses decide whether that thing is also executed.

---

## Parameter vs Argument

- **Parameter** = the empty box with a label, written in the **definition**.
- **Argument** = what is put inside the box, given at the **call**.

```js
function saluta(nome) {      // "nome" = parameter
  console.log("Ciao " + nome);
}

saluta("Marco");             // "Marco" = argument
```

In the main example, the parameter is `event`. The argument (the object with the key info) is passed by the browser when the user presses a key.

---

## Vocabulary Summary

| Term | Definition | In this code |
|---|---|---|
| Variable | A name that points to a value | `textBox` |
| Object | A container grouping properties and methods | `document`, `textBox`, `console`, `event` |
| Function | A named block of code that runs when called | `logKey` |
| Parameter | Placeholder for what a function receives | `event` |
| Argument | The actual value passed to a function | `"input"`, `"keydown"`, `logKey` |
| Method | A function stored inside an object | `querySelector`, `log`, `addEventListener` |
| Property | A data value stored inside an object | `key` |
| Event | A situation the browser recognizes, named by a string | `"keydown"` |

---

# Important function info

## Function scope and conflicts

When you create a function, the variables and other things defined inside the function are inside their own separate scope. This means that they are locked away in their own separate compartment, unreachable from code outside the function.

The top-level outside all your functions is called the **global scope**. Values defined in the global scope are accessible from everywhere in the code.

JavaScript works like this mainly for security and organization. Sometimes you don't want variables to be accessible from everywhere in the code. External scripts called in from elsewhere could mess with your code and cause problems if they use the same variable names, causing conflicts. This might be done maliciously or just by accident.

## Return value

Return values are the values that a function returns when it completes. A return value is used where the function is an intermediate step in a calculation of some kind. You want to get to a final result, which involves some values that need to be calculated by a function. After the function calculates the value, it can return the result so it can be stored in a variable; and you can use this variable in the next stage of the calculation.

To return a value from a custom function, you need to use the return keyword.

```javascript
function random(number) {
  return Math.floor(Math.random() * number);
}
```

or 

```javascript
function random(number) {
  const result = Math.floor(Math.random() * number);
  return result;
}
```

The first version is quicker to write, because it does not include a new variable and therefore is more compact.

We are returning the result of the calculation Math.floor(Math.random() * number) each time the function is called. This return value appears at the point the function was called, and the code continues.

## Function expressions 

A function expression allows us to create a new function in the middle of any expression.

```javascript
let sayHi = function() {
  alert( "Hello" );
};
```

Here we can see a variable sayHi getting a value, the new function, created as function() { alert("Hello"); }.

As the function creation happens in the context of the assignment expression (to the right side of =), this is a Function Expression.

Please note, there’s **no name after the `function` keyword**. Omitting a name is allowed for Function Expressions.

Here we immediately assign it to the variable, so the meaning of these code samples is the same: “create a function and put it into the variable `sayHi`”.

In more advanced situations, that we’ll come across later, a function may be created and immediately called or scheduled for a later execution, not stored anywhere, thus remaining anonymous.

### Callback functions

Callback functions is when you use functions as arguments in other functions:

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

function showOk() {
  alert( "You agreed." );
}

function showCancel() {
  alert( "You canceled the execution." );
}

// usage: functions showOk, showCancel are passed as arguments to ask
ask("Do you agree?", showOk, showCancel);
```

The arguments `showOk` and `showCancel` of `ask` are called callback functions or just callbacks.
We can use Function Expressions to write an equivalent, shorter function:

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
);
```

## Function Expression vs Function Declaration

1. Function Declaration: a function, declared as a separate statement, in the main code flow:

```javascript
// Function Declaration
function sum(a, b) {
  return a + b;
}
```

2. Function Expression: a function, created inside an expression or inside another syntax construct. Here, the function is created on the right side of the “assignment expression” `=`:

```javascript
// Function Expression
let sum = function(a, b) {
  return a + b;
};
```

**A Function Expression is created when the execution reaches it and is usable only from that moment.**

- Function expression: the function only exists once the execution reaches that line. Calling it before that line gives an error, so the order matters.

- Function declaration: JavaScript creates it in a preparation stage, before running any code, so you can call it even if it’s written lower down in the file.

**When a Function Declaration is within a code block, it’s visible everywhere inside that block. But not outside of it.**

```javascript
let age = prompt("What is your age?", 18);

// conditionally declare a function
if (age < 18) {

  function welcome() {
    alert("Hello!");
  }

} else {

  function welcome() {
    alert("Greetings!");
  }

}

// ...use it later
welcome(); // Error: welcome is not defined
```

That’s because a Function Declaration is only visible inside the code block in which it resides.

```javascript
let age = 16; // take 16 as an example

if (age < 18) {
  welcome();               // \   (runs)
                           //  |
  function welcome() {     //  |
    alert("Hello!");       //  |  Function Declaration is available
  }                        //  |  everywhere in the block where it's declared
                           //  |
  welcome();               // /   (runs)

} else {

  function welcome() {
    alert("Greetings!");
  }
}

// Here we're out of curly braces,
// so we can not see Function Declarations made inside of them.

welcome(); // Error: welcome is not defined
```

The correct approach to make `welcome` visible outside of `if` is to use a Function Expression and assign welcome to the variable that is declared outside of if and has the proper visibility.

```javascript
let age = prompt("What is your age?", 18);

let welcome;

if (age < 18) {

  welcome = function() {
    alert("Hello!");
  };

} else {

  welcome = function() {
    alert("Greetings!");
  };

}

welcome(); // ok now
```

Or we could simplify it even further using a question mark operator ?:

```javascript
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  function() { alert("Hello!"); } :
  function() { alert("Greetings!"); };

welcome(); // ok now
```

## Arrow funtions 

```javascript
let func = (arg1, arg2, ..., argN) => expression;
```

This creates a function func that accepts arguments arg1..argN, then evaluates the expression on the right side with their use and returns its result.

```javascript
let sum = (a, b) => a + b;

/* This arrow function is a shorter form of:

let sum = function(a, b) {
  return a + b;
};
*/

alert( sum(1, 2) ); // 3
```
If we have only one argument, then parentheses around parameters can be omitted, making that even shorter.

```javascript
let double = n => n * 2;
// roughly the same as: let double = function(n) { return n * 2 }

alert( double(3) ); // 6
```

If there are no arguments, parentheses are empty, but they must be present:

```javascript
let sayHi = () => alert("Hello!");

sayHi();
```

Arrow functions can be used in the same way as Function Expressions.

```javascript


let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  () => alert('Hello!') :
  () => alert("Greetings!");

welcome();
```

# JavaScript Call Stack

The **Call Stack** is a mechanism that the JavaScript engine uses to keep track of function calls. It tells the engine what function is currently being run and what functions are invoked from within it.

## Key Concepts

* **Single-Threaded:** JavaScript has a single call stack, meaning it executes one task at a time (synchronous execution).
* **LIFO Principle:** It operates on a **LIFO** (*Last In, First Out*) data structure. The last function pushed into the stack is the first one popped out upon completion.
* **Execution Contexts:** It manages both the *Global Execution Context* and individual *Function Execution Contexts*.

---

## Code Example

```javascript
function add(a, b) {
    return a + b;
}

function average(a, b) {
    return add(a, b) / 2;
}

let result = average(10, 20);
console.log(result); // 15
```

### Execution Flow

1. **Global Context:** When the script starts, the global execution context (`main()`) is pushed onto the stack.
2. **Push `average()`:** `average(10, 20)` is invoked and pushed to the top of the stack.
3. **Push `add()`:** Inside `average()`, `add(10, 20)` is invoked and pushed above `average()`.
4. **Pop `add()`:** `add()` finishes, returns `30`, and is popped off the stack.
5. **Pop `average()`:** `average()` resumes, computes `30 / 2`, returns `15`, and is popped off the stack.
6. **Empty Stack:** Once the script ends, the global context is removed and the stack is empty.

---

## Stack Overflow

A **Stack Overflow** occurs when the number of execution contexts exceeds the maximum size allocated for the call stack, typically caused by infinite recursion without a base condition:

```javascript
function recursiveFunction() {
    recursiveFunction(); // Infinite self-invocation
}

recursiveFunction(); 
// Uncaught RangeError: Maximum call stack size exceeded
```
