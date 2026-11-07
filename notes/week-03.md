
## The difference between classes, variables and objects

### 1. Variable (recap)

A variable is a name that points to a value:

```javascript
let firstName = "Leo";
```

- `let` is the declaration. It creates a new name.
- `firstName` is the variable, the name itself.
- `=` is the assignment operator. It connects the name to a value.
- `"Leo"` is the value. Because it is surrounded by quotes, its type is a string.

### 2. Classes

A class is a blueprint. It describes what every item built from it will have (properties) and what it can do (methods). A class does not create anything by itself.

```javascript
class House {
  constructor(color, rooms) {
    this.color = color;
    this.rooms = rooms;
  }
  describe() {
    return `A ${this.color} house with ${this.rooms} rooms`;
  }
}
```

### 3. Objects

An object is a real thing built from the blueprint, created with the keyword `new`. Many objects can be built from the same class, and each one lives in its own place in memory.

```javascript
new House("blue", 3);
```

The variable syntax is the same as before. The only difference is that the value on the right side of `=` is now an object instead of a string:

```javascript
const elliotsHouse = new House("blue", 3);
const annasHouse = new House("green", 5);
```

## Strings: a closer look

A JavaScript string is zero or more characters written inside quotes:

```javascript
let str = "Hello";
```

- Double quotes: `"Hello"`
- Single quotes: `'Hello'`
- Backticks: `` `Hello` ``

There is no difference between using single or double quotes. Backticks are "extended functionality" quotes. They allow us to embed variables and expressions into a string by wrapping them in `${...}`, for example:

```javascript
let name = "John";

// embed a variable
alert( `Hello, ${name}!` ); // Hello, John!

// embed an expression
alert( `the result is ${1 + 2}` ); // the result is 3
```

The expression inside `${...}` is evaluated and the result becomes a part of the string. We can put anything in there: a variable like `name`, an arithmetical expression like `1 + 2`, or something more complex.

## Using string methods

JavaScript has two ways to hold a string. Strings can be created as **primitives**, from string literals, or as **objects**, using the [`String()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/String) constructor:

```javascript
const string1 = "A string primitive"; // primitive string: just the value
const string2 = new String("A String object"); // string object: container built from blueprint
```

Primitives have no methods, because they're not objects. But you can still write this:

```javascript
"hello".toUpperCase(); // "HELLO"
```

How does that work if `"hello"` isn't an object? When you call a method on a primitive, JavaScript quietly does this behind the scenes:

1. Builds a temporary String object around your value (the "wrapper").
2. Calls the method on that temporary object.
3. Throws the wrapper away and gives you the result.

It's like walking into a shop with a loose item, and the shopkeeper briefly puts it in a box to use their tools on it, then hands you back the result and recycles the box. You never see the box.

- Almost always, use plain strings: `"hello"`. Don't use `new String(...)`.
- Plain strings still have methods because of the automatic wrapping, so you don't need to think about it.
- The same is true for numbers and booleans.

### Basic string methods

All string methods produce a new string without altering the original string. A **method** is a bit of functionality built into the language or specific data types.

| | |
|:-----------------------|:-----------------------|
| String `length`        | String `isWellFormed()` |
| String `charAt()`      | String `toWellFormed()` |
| String `charCodeAt()`  | String `trim()`         |
| String `codePointAt()` | String `trimStart()`    |
| String `concat()`      | String `trimEnd()`      |
| String `at()`          | String `padStart()`     |
| String `[ ]`           | String `padEnd()`       |
| String `slice()`       | String `repeat()`       |
| String `substring()`   | String `replace()`      |
| String `substr()`      | String `replaceAll()`   |
| String `toUpperCase()` | String `split()`        |
| String `toLowerCase()` |                         |

#### `length`

The `length` property returns the length of a string:

```javascript
let text = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
let length = text.length; // 26
```

#### `charAt()`

The `charAt()` method returns the character at a specified index (position) in a string:

```javascript
let text = "HELLO WORLD";
let char = text.charAt(0); // H
```

#### `charCodeAt()`

The `charCodeAt()` method returns the code of the character at a specified index in a string. The method returns a UTF-16 code (an integer between 0 and 65535).

```javascript
let text = "HELLO WORLD";
let char = text.charCodeAt(0); // 72
```

#### `codePointAt()`

Get the code point value at the first position in a string:

```javascript
let text = "HELLO WORLD";
let code = text.codePointAt(0); // 72
```

#### `concat()`

Joins two or more strings:

```javascript
let text1 = "Hello";
let text2 = "World!";
let text3 = text1.concat(" ", text2); // Hello World!
```

#### `at()`

The `at()` method returns the character at a specified index (position) in a string. It allows the use of negative indexes, while `charAt()` does not.

```javascript
const name = "W3Schools";

let letter = name.at(2);  // S
letter = name.at(-5);     // h
```

#### Property access `[ ]`

```javascript
let text = "HELLO WORLD";
let char = text[0]; // H
```

Property access might be a little unpredictable:

- It makes strings look like arrays (but they are not).
- If no character is found, `[ ]` returns `undefined`, while `charAt()` returns an empty string.
- Property access is read only, but `str[0] = "A"` gives no error in "sloppy mode".

#### `slice(start, end)`

Extracts a part of a string and returns the extracted part in a new string.

```javascript
let text = "Apple, Banana, Kiwi";
let part = text.slice(7, 13); // Banana
```

If you omit the second parameter, the method will slice out the rest of the string. If a parameter is negative, the position is counted from the end of the string.

#### `substring(start, end)`

`substring()` is similar to `slice()`. The difference is that start and end values less than 0 are treated as 0 in `substring()`.

#### `substr(start, length)`

`substr()` is similar to `slice()`. The difference is that the second parameter specifies the length of the extracted part.

**WARNING:** You are strongly advised to use `substring()` or `slice()` instead.

#### `toUpperCase()`

A string is converted to upper case:

```javascript
let text1 = "Hello World!";
let text2 = text1.toUpperCase();
```

#### `toLowerCase()`

A string is converted to **lower** case:

```javascript
let text1 = "Hello World!";       // String
let text2 = text1.toLowerCase();  // text2 is text1 converted to lower
```

#### `isWellFormed()`

The `isWellFormed()` method returns `true` if a string is well formed. Otherwise it returns `false`. A string is not well formed if it contains lone surrogates.

```javascript
let text = "Hello world!";
let result = text.isWellFormed(); // true
```

```javascript
let text = "Hello World \uD800";
let result = text.isWellFormed(); // false
```

#### `toWellFormed()`

The String method `toWellFormed()` returns a new string where all "lone surrogates" are replaced with the Unicode replacement character (U+FFFD).

```javascript
let text = "Hello World \uD800";
let result = text.toWellFormed(); // Hello World �
```

#### `trim()`

The `trim()` method removes whitespace from both sides of a string:

```javascript
let text1 = "      Hello World!      ";
let text2 = text1.trim();
```

#### `trimStart()`

The `trimStart()` method works like `trim()`, but removes whitespace only from the start of a string.

#### `trimEnd()`

The `trimEnd()` method works like `trim()`, but removes whitespace only from the end of a string.

#### `padStart()`

The `padStart()` method pads a string from the start. It pads a string with another string (multiple times) until it reaches a given length.

Pad a string with "0" until it reaches the length 4:

```javascript
let text = "5";
let padded = text.padStart(4, "0"); // 0005
```

```javascript
let text = "5";
let padded = text.padStart(4, "x"); // xxx5
```

#### `padEnd()`

Same as `padStart()` but starts from the end:

```javascript
let text = "5";
let padded = text.padEnd(4, "0"); // 5000
```

#### `repeat()`

The `repeat()` method returns a string with a number of copies of a string.

```javascript
let text = "Hello world!";
let result = text.repeat(2); // Hello world!Hello world!
```

#### `replace()`

```javascript
let text = "Please visit Microsoft!";
let newText = text.replace("Microsoft", "W3Schools"); // Please visit W3Schools!
```

By default, the `replace()` method replaces **only the first** match.

To replace case insensitively, use a **regular expression** with an `/i` flag (insensitive):

```javascript
text.replace(/MICROSOFT/i, "W3Schools");
```

To replace all matches, use a **regular expression** with a `/g` flag (global match):

```javascript
text.replace(/Microsoft/g, "W3Schools");
```

#### `replaceAll()`

The `replaceAll()` method allows you to specify a regular expression instead of a string to be replaced. If the parameter is a regular expression, the global flag (`g`) must be set, otherwise a `TypeError` is thrown.

```javascript
text = text.replaceAll("Cats", "Dogs");
text = text.replaceAll(/Cats/g, "Dogs");
text = text.replaceAll("cats", "dogs");
text = text.replaceAll(/cats/g, "dogs");
```

#### `split()`

A string can be converted to an array with the `split()` method:

```javascript
text.split("")     // Split on characters
text.split(",")    // Split on commas
text.split(" ")    // Split on spaces
text.split("|")    // Split on pipe
```

Using `split("")` is unsafe for strings containing emojis or complex characters. The method splits by UTF-16 code units and will break surrogate pairs.

`split("")` is always **unsafe for emojis**. It will slice right through them and create broken, corrupt code fragments. `split(" ")` is usually safe for words, even if they have emojis inside them, as long as the emoji is not glued right next to a space you are splitting on.

## Comparisons

In JavaScript they are written like this:

- Greater/less than: `a > b`, `a < b`.
- Greater/less than or equals: `a >= b`, `a <= b`.
- Equals: `a == b`; please note the double equality sign `==` means the equality test, while a single one `a = b` means an assignment.
- Not equals: In maths the notation is `≠`, but in JavaScript it's written as `a != b`.

### [Boolean is the result](https://javascript.info/comparison#boolean-is-the-result)

All comparison operators return a boolean value:

- `true` — means "yes", "correct" or "the truth".
- `false` — means "no", "wrong" or "not the truth".

```javascript
alert( 2 > 1 );  // true (correct)
alert( 2 == 1 ); // false (wrong)
alert( 2 != 1 ); // true (correct)
```

A comparison result can be assigned to a variable, just like any value:

```javascript
let result = 5 > 4; // assign the result of the comparison
alert( result ); // true
```

### Comparing strings

To see whether a string is greater than another, JavaScript uses the so-called "dictionary" or "lexicographical" order. In other words, strings are compared letter by letter. For example:

```javascript
alert( 'Z' > 'A' );    // true
alert( 'Glow' > 'Glee' ); // true
alert( 'Bee' > 'Be' ); // true
```

1. Compare the first character of both strings.
2. If the first character from the first string is greater (or less) than the other string's, then the first string is greater (or less) than the second. We're done.
3. Otherwise, if both strings' first characters are the same, compare the second characters the same way.
4. Repeat until the end of either string.
5. If both strings end at the same length, then they are equal. Otherwise, the longer string is greater.

`'Glow'` and `'Glee'`, for example, are compared character by character:

1. `G` is the same as `G`.
2. `l` is the same as `l`.
3. `o` is greater than `e`. Stop here. The first string is greater.

### [Comparison of different types](https://javascript.info/comparison#comparison-of-different-types)

When comparing values of different types, JavaScript converts the values to numbers.

For example:

```javascript
alert( '2' > 1 );   // true, string '2' becomes a number 2
alert( '01' == 1 ); // true, string '01' becomes a number 1
```

For boolean values, `true` becomes `1` and `false` becomes `0`.

```javascript
alert( true == 1 );  // true
alert( false == 0 ); // true
```

### [Strict equality](https://javascript.info/comparison#strict-equality)

A regular equality check `==` has a problem. It cannot differentiate `0` from `false`:

```javascript
alert( 0 == false ); // true
```

The same thing happens with an empty string:

```javascript
alert( '' == false ); // true
```

This happens because operands of different types are converted to numbers by the equality operator `==`. An empty string, just like `false`, becomes a zero.

What to do if we'd like to differentiate `0` from `false`?

A strict equality operator `===` checks the equality without type conversion.

In other words, if `a` and `b` are of different types, then `a === b` immediately returns `false` without an attempt to convert them.

Let's try it:

```javascript
alert( 0 === false ); // false, because the types are different
```

There is also a "strict non-equality" operator `!==`, analogous to `!=`.

## Conditionals

Conditional statements allow us to represent decisions, from the choice that must be made to the resulting outcome of those choices.

### `if ... else`

If the **condition** returns `true`, run code A, **else** run code B.

```javascript
if (condition) {
  /* code to run if condition is true */
} else {
  /* run some other code instead */
}
```

The keyword `if` is followed by some parentheses, then:

- A condition to test, placed inside the parentheses (typically "is this value bigger than this other value?", or "does this value exist?"). The condition makes use of the comparison operators and returns `true` or `false`.
- A set of curly braces, inside which we have some code — this can be any code we like, and it only runs if the condition returns `true`.
- The keyword `else`.
- Another set of curly braces, inside which we have some more code — this can be any code we like, and it only runs if the condition is not `true` — or in other words, the condition is `false`.

You don't have to include the `else` and the second curly brace block — the following is also perfectly legal code:

```javascript
if (condition) {
  /* code to run if condition is true */
}

/* run some other code */
```

In this case, the second block of code is not controlled by the conditional statement, so it **always** runs, regardless of whether the condition returns `true` or `false`.

If you have multiple `if`s, then the code checks the conditions **one after another**, and the first one that is true wins.

```javascript
let weather = "rainy";
let advice;

if (weather === "sunny") {
  advice = "Wear shorts!";
} else if (weather === "rainy") {
  advice = "Take an umbrella.";
} else if (weather === "snowing") {
  advice = "Stay in with hot chocolate.";
}

console.log(advice);
```

**How it runs, step by step** (with `weather = "rainy"`):

1. Is `weather === "sunny"`? No, skip that block.
2. Is `weather === "rainy"`? Yes, so `advice` becomes `"Take an umbrella."`.
3. JavaScript stops here. It does not check the remaining conditions.
4. `console.log(advice)` prints `Take an umbrella.`

### Default false values

When a value is placed inside `if ( )`, JavaScript asks: "is this value **truthy** or **falsy**?"

There are only a few values that are, by default, false:

- `false`
- `0`
- `""` (empty string)
- `null`
- `undefined`
- `NaN`

Everything else is treated as `true`. So you don't have to write an explicit form for every value:

```javascript
if (shoppingDone === true) // explicit
if (shoppingDone)          // shorter, same result
```

### Nesting `if ... else`

You can put an `if ... else` statement inside another one:

```javascript
if (choice === "sunny") {
  if (temperature < 30) {
    para.textContent = `It is ${temperature} degrees outside — nice and sunny. Let's go out to the beach, or the park, and get an ice cream.`;
  } else if (temperature >= 30) {
    para.textContent = `It is ${temperature} degrees outside — REALLY HOT! If you want to go outside, make sure to put some sunscreen on.`;
  }
}
```

1. First, JavaScript checks whether the chosen weather is sunny. If it isn't, everything inside the block is skipped.

   ```javascript
   if (choice === "sunny") { ... }
   ```

2. Only when the weather **is** sunny, JavaScript goes inside and asks a second question: how hot is it?

   ```javascript
   if (temperature < 30) {         // under 30 degrees
   } else if (temperature >= 30) { // 30 degrees or more
   }
   ```

3. Text inside backticks (`` ` ``) is a **template string**. Anything inside `${ }` is replaced by the value of that variable. If `temperature` is 28, the result is: *It is 28 degrees outside — nice and sunny. Let's go out to the beach, or the park, and get an ice cream.*

   ```javascript
   "It is " + temperature + " degrees outside — nice and sunny."
   ```

**Example – the name of JavaScript.** Using the `if..else` construct, write the code which asks: "What is the 'official' name of JavaScript?". If the visitor enters "ECMAScript", then output "Right!", otherwise output: "You don't know? ECMAScript!"

```html
<!DOCTYPE html>
<html>

<body>
  <script>
    'use strict';

    let value = prompt('What is the "official" name of JavaScript?', '');

    if (value == 'ECMAScript') {
      alert('Right!');
    } else {
      alert("You don't know? ECMAScript!");
    }
  </script>
</body>

</html>
```

## Logical operators: AND, OR and NOT

Logical operators are needed when you want to test multiple conditions.

### `&&` — AND

In classical programming, AND returns `true` if both (or more) operands are truthy and `false` otherwise:

```javascript
alert( true && true );   // true
alert( false && true );  // false
alert( true && false );  // false
alert( false && false ); // false
```

```javascript
if (hour == 12 && minute == 30) {
  alert( 'The time is 12:30' );
}
```

```javascript
result = value1 && value2 && value3;
```

The AND `&&` operator does the following:

- Evaluates operands from left to right.
- For each operand, converts it to a boolean. If the result is **false**, stops and returns the original value of that operand.
- If all operands have been evaluated (i.e. all were truthy), returns the last operand.

```javascript
// if the first operand is truthy,
// AND returns the second operand:
alert( 1 && 0 ); // 0
alert( 1 && 5 ); // 5
```

```javascript
// if the first operand is falsy,
// AND returns it. The second operand is ignored
alert( null && 5 ); // null
alert( 0 && "no matter what" ); // 0
```

### `||` — OR

OR allows you to chain together two or more expressions so that one or more of them have to individually evaluate to **true** for the whole expression to return **true**.

```javascript
result = a || b;
```

There are four possible logical combinations:

```javascript
alert( true || true );   // true
alert( false || true );  // true
alert( true || false );  // true
alert( false || false ); // false
```

You can pass multiple conditions with this logic:

```javascript
let hour = 12;
let isWeekend = true;

if (hour < 10 || hour > 18 || isWeekend) {
  alert( 'The office is closed.' ); // it is the weekend
}
```

The OR `||` operator does the following:

- Evaluates operands from left to right.
- For each operand, converts it to boolean. If the result is **true**, stops and returns the original value of that operand.
- If all operands have been evaluated (i.e. all were **false**), returns the last operand.

### `!` (NOT)

The boolean NOT operator is represented with an exclamation sign `!`.

```javascript
result = !value;
```

The operator accepts a single argument and does the following:

1. Converts the operand to boolean type: `true`/`false`.
2. Returns the inverse value.

A double NOT `!!` is sometimes used for converting a value to boolean type:

```javascript
alert( !!"non-empty string" ); // true
alert( !!null ); // false
```

### Precedence

```javascript
alert( null || 2 && 3 || 4 );
```

The precedence of AND `&&` is higher than `||`, so it executes first.

The result of `2 && 3 = 3`, so the expression becomes:

```javascript
null || 3 || 4 // 3
```

### Short-circuit evaluation

Sometimes, people use this feature to execute commands only if the condition on the left part is falsy.

```javascript
true || alert("not printed");
false || alert("printed");
```

```javascript
if (choice === "sunny" && temperature < 86)
if (iceCreamVanOutside || houseStatus === "on fire")
```

You can combine as many logical statements together as you want, in whatever structure:

```javascript
if ((x === 5 || y > 3 || z <= 10) && (loggedIn || userName === "Steve")) {
  // run the code
}
```

A common mistake when using the logical OR operator in conditional statements is to try to state the variable whose value you are checking once, and then give a list of values it could be to return true, separated by `||` (OR) operators. In English you say: "if x is 5 or 7 or 10 or 20". Writing that literally gives:

```javascript
if (x === 5 || 7 || 10 || 20) {
  // run my code
}
```

#### Why it's wrong

The `||` operator splits the line into separate pieces, and each piece is checked **on its own**:

```javascript
x === 5 // a real comparison: true or false
7       // just the number 7, no comparison at all
10      // just the number 10
20      // just the number 20
```

Only the first piece compares anything with `x`. The other three are just numbers sitting alone. And remember truthy and falsy from earlier: the number `7` is not in the falsy list, so JavaScript treats it as **true**. Since `7` is always true, the whole condition is **always true**.

This is the right way:

```javascript
if (x === 5 || x === 7 || x === 10 || x === 20) {
  // run my code
}
```

## `switch`

---

A `switch` does the same job as a long `if / else if` chain, but it's tidier when you compare **one value against many possible choices**.

```javascript
if (weather === "sunny") {
  advice = "Wear shorts!";
} else if (weather === "rainy") {
  advice = "Take an umbrella.";
} else if (weather === "snowing") {
  advice = "Stay in with hot chocolate.";
} else {
  advice = "No idea, look out the window.";
}
```

With `switch`:

```javascript
let weather = "rainy";
let advice;

switch (weather) {
  case "sunny":
    advice = "Wear shorts!";
    break;
  case "rainy":
    advice = "Take an umbrella.";
    break;
  case "snowing":
    advice = "Stay in with hot chocolate.";
    break;
  default:
    alert( "I don't know such values" );
}

console.log(advice);
```

Let's emphasize that the equality check for `case` is always strict.

**The parts**

- `switch (weather)` is the value being checked. You write it once, instead of repeating `weather ===` every time.
- `case "sunny":` means "if `weather` is exactly `"sunny"`, run the code below". It uses strict comparison, like `===`.
- `break;` means "stop here and leave the switch". Without it, JavaScript keeps running the next cases too, even if they don't match.
- `default:` is the fallback, like the final `else`. It runs only if no case matched. It doesn't need a `break` because it's last.

**How it runs** (with `weather = "rainy"`)

1. Is it `"sunny"`? No, skip.
2. Is it `"rainy"`? Yes, so `advice` becomes `"Take an umbrella."`.
3. `break` makes JavaScript jump out of the switch.
4. `console.log(advice)` prints `Take an umbrella.`

### Grouping of `case`

Several variants of `case` which share the same code can be grouped. For example, if we want the same code to run for `case 3` and `case 5`:

```javascript
let a = 3;

switch (a) {
  case 4:
    alert('Right!');
    break;

  case 3: // (*) grouped two cases
  case 5:
    alert('Wrong!');
    alert("Why don't you take a math class?");
    break;

  default:
    alert('The result is strange. Really.');
}
```

## Ternary operator (or "question mark" operator)

The ternary operator is a **short if/else** on one line. You will use it only when you have **two choices** and the code is short. For more choices, use `if / else if` or `switch`.

```javascript
condition ? valueIfTrue : valueIfFalse
```

Read the `?` as "then" and the `:` as "otherwise".

With `if / else`:

```javascript
let isBirthday = true;
let greeting;

if (isBirthday) {
  greeting = "Happy birthday!";
} else {
  greeting = "Good morning!";
}
```

With the ternary, same result:

```javascript
let isBirthday = true;
let greeting = isBirthday ? "Happy birthday!" : "Good morning!";

console.log(greeting); // Happy birthday!
```

## JavaScript Developer Tools 

DevTools is a suite of debugging and diagnostic software built directly into modern web browsers. The Developer Tools are useful for running JavaScript code, editing HTML and CSS styles without having to refresh the page, and viewing performance data. In this case we are using the Chrome browser. There are some differences between DevTools browsers but after you learn one, the others would be much easy to understand. 

**Opening DevTools**

1. Keyboard shortcut `F12` or `Ctrl + Shift + c`;
2. Right-click on a webpage and select `Inspect`;
3. `Chrome Menu` > `More Tools` > `Developer Tools`.

### Debugging in the browser

Debugging is the process of finding and fixing errors within a script. All modern browsers and most other environments support debugging tools – a special UI in developer tools that makes debugging much easier. 

#### The "Sources panel" in DevTools

**The Sources panel has 3 parts:**

1. The File Navigator pane lists HTML, JavaScript, CSS and other files, including images that are attached to the page. Chrome extensions may appear here too.
2. The Code Editor pane shows the source code.
3. The JavaScript Debugging pane is for debugging.

### Console and Breakpoints

If we press `Esc`, then a console opens below. You can try to write your code here. On the left, in the `Page` section you can open a `.js` file, within that file you should see the lines of the code, and each line with its own number. If you select one of this numbers you create a **breakpoint**. 
A *breakpoint* is a point of code where the debugger will automatically pause the JavaScript execution (from the point).

We can also use the `debugger` command to pause the code:

```javascript
function hello(name) {
  let phrase = `Hello, ${name}!`;

  debugger;  // <-- the debugger stops here

  say(phrase);
}
```

There are multile methods to make a breakpoints. While the code is paused, we can examine current variables, execute commands in the console etc. In other words, we can debug it.

You can select multiple section to break lines, for example: from number 1 to 5. We can always find a list of breakpoints in the right panel. That’s useful when we have many breakpoints in various files. It allows us to:

- Quickly jump to the breakpoint in the code (by clicking on it in the right panel).
- Temporarily disable the breakpoint by unchecking it.
- Remove the breakpoint by right-clicking and selecting Remove.
- …And so on.

### Pause amd look around

After you selected a function, for example, reload the page `(F5)`. As the breakpoint is set, the execution pauses for that lines. 
The informational dropdowns to the right (labeled with arrows). They allow you to examine the current code state:

1. **`Watch` – shows current values for any expressions.**
You can click the plus + and input an expression. The debugger will show its value, automatically recalculating it in the process of execution.

2. **`Call Stack` – shows the nested calls chain.**
If you click on a stack item the debugger jumps to the corresponding code, and all its variables can be examined as well.

3. **`Scope` – current variables.**
`Local` shows local function variables. You can also see their values highlighted right over the source.
`Global` has global variables (out of any functions).
There’s also `this` keyword there that we didn’t study yet, but we’ll do that soon.

### Tracing the execution

There are buttons for it at the top of the right panel:

- **“Resume”: continue the execution, hotkey `F8`.**
  Resumes the execution. If there are no additional breakpoints, then the execution just continues and the debugger loses control.

- **“Step”: run the next command, hotkey `F9`.**
  Run the next statement. If we click it now, alert will be shown.
  Clicking this again and again will step through all script statements one by one.

- **“Step over”: run the next command, but don’t go into a function, hotkey `F10`.**
  Similar to the previous “Step” command, but behaves differently if the next statement is a function call (not a built-in, like alert, but a function of our own).
  If we compare them, the “Step” command goes into a nested function call and pauses the execution at its first line, while “Step over” executes the nested function call invisibly to us, skipping the function internals.
  The execution is then paused immediately after that function call.
  That’s good if we’re not interested to see what happens inside the function call.

- **“Step into”, hotkey `F11`.**
  That’s similar to “Step”, but behaves differently in case of asynchronous function calls. If you’re only starting to learn JavaScript, then you can ignore the difference, as we don’t have asynchronous calls yet.

  For the future, just note that “Step” command ignores async actions, such as setTimeout (scheduled function call), that execute later. The “Step into” goes into their code, waiting for them if necessary. See DevTools manual for more details.

- **“Step out”: continue the execution till the end of the current function, hotkey   `Shift+F11`.**
  Continue the execution and stop it at the very last line of the current function. That’s handy when we accidentally entered a nested call using *step*, but it does not interest us, and we want to continue to its end as soon as possible.

- **`enable/disable` all breakpoints.**
  That button does not move the execution. Just a mass on/off for breakpoints.

- **`enable/disable` automatic pause in case of an error.**
  When enabled, if the developer tools is open, an error during the script execution automatically pauses it. Then we can analyze variables in the debugger to see what went wrong. So if our script dies with an error, we can open debugger, enable this option and reload the page to see where it dies and what’s the context at that moment.

### CSS inspector

To understand how you can change the CSS of the page start with whis:

1. Open the DevTool;
2. Select the `Inspector` on the top of the DevTool;
3. Select a random `<dev>`;
4. in `Elements`>`Styles` you can find every proprieties applied to your element, change it, see the layouts, box model etc.

There are many instructions of how to use the DevTools, you do not need to memorize these as this is just to gain awareness of how to debug on the browser. I reccomend to look at the ufficial Chrome DevTools docs, whenever you need to look up something, from this link: `https://developer.chrome.com/docs/devtools/css/reference/`

# Chapter V – Function Basics

## Function

A function holds a piece of code that does a specific task.

A function takes some data as input, the code inside the function does something with the data, and then the result is returned.

```javascript 
function favoriteAnimal(animal) {
    return animal + " is my favorite animal!"
}

const message = favoriteAnimal('Goat')
console.log(message)  

//Goat is my favorite animal!
```

1. `function`: the keyword to call a function, the declaration;
2. `favoriteAnimal`: the name of the function;
3. `(animal)`: the parameter;
4. `{return animal + " is my favorite animal!"}` the function body, code of the function;
5. `(Goat)`: the argument.

### How does it work?

In JavaScript, paramaters are the items listed between the parentheses `()` in the function declaration. Function arguments are the actual values we decide to pass to the function.

In the example above, the function definition is written on the first line: function `favoriteAnimal(animal)`. The parameter, `animal`, is found inside the parentheses. We could just as easily replace `animal` with `pet`, `x`, or `blah`. But in this case, naming the parameter `animal` gives someone reading our code a bit of context so that they don’t have to guess what `animal` may eventually contain.

By putting `animal` inside the parentheses of the `favoriteAnimal` function declaration, we are telling JavaScript that we will send some value *(an argument)* to our `favoriteAnimal` function. This means that `animal` is just a placeholder for some future value.

In the fifth line, `favoriteAnimal('Goat')` is where we are calling our `favoriteAnimal` function and passing the value `'Goat'` inside that function call. Here, `'Goat'` is our **argument**. We are telling the `favoriteAnimal` function, “Please send `'Goat'` to the `favoriteAnimal` function and use `'Goat'` wherever the `animal` placeholder is.”

Make note that, while we are storing the outcome of `favoriteAnimal('Goat')` inside the message variable, and later passing message as an argument for `log()`, it is also possible to pass in a function call as an argument in a different function call.

```javascript
function favoriteAnimal(animal) {
    return animal + " is my favorite animal!"
}

console.log(favoriteAnimal('Goat'))
```

In the example above, we pass in `favoriteAnimal('Goat')` as an argument in `log()`. When doing so, the return value of the `favoriteAnimal('Goat')` function call (the string "Goat is my favorite animal!") is used as the argument for `log()`, without first storing it in a separate variable.

Keep this possibility in mind because you’ll be passing in function calls as arguments somewhat often. If we just called `favoriteAnimal('Goat')` on its own without passing it as an argument for `console.log` to print it’s return value, it would still return that string… to nowhere. Nothing would appear in the console, nor would the string get stored in a variable.

### Local variables

A variable declared inside a function is only visible inside that function.

```javascript
function showMessage() {
  let message = "Hello, I'm JavaScript!"; // local variable

  alert( message );
}

showMessage(); // Hello, I'm JavaScript!

alert( message ); // <-- Error! The variable is local to the function
```

### Outer variables

A function can access an outer variable as well, for example:

```javascript 
let userName = 'John';

function showMessage() {
  let message = 'Hello, ' + userName;
  alert(message);
}

showMessage(); // Hello, John
```

### Outer and local variables

A function can access an outer variable as well, for example:

```javascript 
let userName = 'John';

function showMessage() {
  let message = 'Hello, ' + userName; 
  alert(message);
}

showMessage(); // Hello, John
```

The function has full access to the outer variable. It can modify it as well.

```javascript
let userName = 'John';

function showMessage() {
  userName = "Bob"; // (1) changed the outer variable

  let message = 'Hello, ' + userName;
  alert(message);
}

alert( userName ); // John before the function call

showMessage();    // we are calling the function

alert( userName ); // Bob, the value was modified by the function
```

**The outer variable is only used if there’s no local one.**

If a same-named variable is declared inside the function then it shadows the outer one. For instance, in the code below the function uses the local userName. The outer one is ignored:

```javascript
let userName = 'John';

function showMessage() {
  let userName = "Bob"; // declare a local variable. This local userName is different from the first that we declared. They are not the same anymore.

  let message = 'Hello, ' + userName; // Bob
  alert(message);
}

// the function will create and use its own userName
showMessage();

alert( userName ); // John, unchanged, the function did not access the outer variable
```

### Parameters

We can pass arbitrary data to functions using parameters.
In the example below, the function has two parameters: from and text.

```javascript
function showMessage(from, text) { // parameters: from, text
  alert(from + ': ' + text);
}

showMessage('Ann', 'Hello!'); // Ann: Hello! (*)
showMessage('Ann', "What's up?"); // Ann: What's up? (**)
```

Here’s one more example: we have a variable from and pass it to the function. Please note: the function changes from, but the change is not seen outside, because a function always gets a copy of the value:

```javascript
function showMessage(from, text) {

  from = '*' + from + '*'; // make "from" look nicer

  alert( from + ': ' + text );
}

let from = "Ann";

showMessage(from, "Hello"); // *Ann*: Hello

// the value of "from" is the same, the function modified a local copy
alert( from ); // Ann
```

When a value is passed as a function parameter, it’s also called an argument.

- A parameter is the variable listed inside the parentheses in the function declaration (it’s a declaration time term).
- An argument is the value that is passed to the function when it is called (it’s a call time term).

### Default values 

If a function is called, but an argument is not provided, then the corresponding value becomes undefined.
For instance, the aforementioned function showMessage(from, text) can be called with a single argument:

```javascript
showMessage("Ann");
```

That’s not an error. Such a call would output `"*Ann*: undefined"`. As the value for `text` isn’t passed, it becomes `undefined`.`

We can specify the so-called “default” (to use if omitted) value for a parameter in the function declaration, using =:

```javascript
function showMessage(from, text = "no text given") {
  alert( from + ": " + text );
}

showMessage("Ann"); // Ann: no text given
```

Now if the `text` parameter is not passed, it will get the value `"no text given"`.
The default value also jumps in if the parameter exists, but strictly equals `undefined`, like this:

```javascript
showMessage("Ann", undefined); // Ann: no text given
```

Here `"no text given"` is a string, but it can be a more complex expression, which is only evaluated and assigned if the parameter is missing. So, this is also possible:

```javascript
function showMessage(from, text = anotherFunction()) {
  // anotherFunction() only executed if no text given
  // its result becomes the value of text
}
```

#### Alternative default parameters

Sometimes it makes sense to assign default values for parameters at a later stage after the function declaration.

```javascript
function showMessage(text) {
  // ...

  if (text === undefined) { // if the parameter is missing
    text = 'empty message';
  }

  alert(text);
}

showMessage(); // empty message
```

…Or we could use the || operator:

```javascript
function showMessage(text) {
  // if text is undefined or otherwise falsy, set it to 'empty'
  text = text || 'empty';
  ...
}
```

### Returning a value

A function can return a value back into the calling code as the result.

```javascript
function sum(a, b) {
  return a + b;
}

let result = sum(1, 2);
alert( result ); // 3
```

The directive return can be in any place of the function. When the execution reaches it, the function stops, and the value is returned to the calling code (assigned to result above).

There may be many occurrences of return in a single function. For instance:

```javascript
function checkAge(age) {
  if (age >= 18) {
    return true;
  } else {
    return confirm('Do you have permission from your parents?');
  }
}

let age = prompt('How old are you?', 18);

if ( checkAge(age) ) {
  alert( 'Access granted' );
} else {
  alert( 'Access denied' );
}
```
 is possible to use return without a value. That causes the function to exit immediately.

For example:

```javascript
function showMovie(age) {
  if ( !checkAge(age) ) {
    return;
  }

  alert( "Showing you the movie" ); // (*)
  // ...
}
```

In the code above, if checkAge(age) returns false, then showMovie won’t proceed to the alert.
**Never add a newline between return and the value.** JavaScript assumes a semicolon after return.

### Naming a function

Functions are actions, so their name is usually a verb. It should be brief, accurate, and describe what the function does.

A common practice is to start the name with a verb prefix. The team should agree on what each prefix means:

* `show…` – shows something
* `get…` – returns a value
* `calc…` – calculates something
* `create…` – creates something
* `check…` – checks something and returns a boolean

#### One function – one action

A function should do exactly what is suggested by its name, no more. Two independent actions usually deserve two functions, even if they are usually called together (in that case we can make a 3rd function that calls those two).

### Method and functions are different

A function is a recipe that stands on its own. A method is a function that belongs to an object.

**Function:**

```javascript
function sayHi() {
  alert("Hi");
}

sayHi();
```

**Method**

```javascript
let user = {
  name: "John",
  sayHi() {
    alert("Hi");
  }
};

user.sayHi();
```

You call it with a dot, because it lives inside an object. There are many methods ready to go in your browser like: `console.clear()` it works because the browser creates the console object and puts `clear()` inside it.
