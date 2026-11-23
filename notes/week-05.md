# Clean Code

A significant amount of time is spent on reading code. This includes code written by other team members, code written by people who are no longer part of your team, and even code that you wrote two weeks ago. It is important to have an understanding of some methods to write clean code.

### camelCase

camelCase is a naming technique that allows writing multiple words together  without spaces or punctuation. So we can name our functions or variables like `timeOut`, `nextPage`, `setTimeOn`, etc. While not every language uses this convention, it’s very common in JavaScript so it’ll be a good example to follow.

## Naming functions and variables

You should always name things meaningfully. 

```javascript
const generateUserGreeting = function (name) {
  const greeting = "Hello ";
  return greeting + name;
};

generateUserGreeting("John");
```

```javascript
const x= function (z){
   const w = "Hello ";
return w +  z

 }

x("John");
```

In the first example we have a variable `greeting`, to which the parameter `name` is concatenated. The function is named `generateUserGreeting` and the function does what the name suggests. Nice, clean, and understandable.

In the second example the function is named x with variables like z, and w. Very confusing.

### Use consistent vocabulary

Variables of the same type ideally follow a consistent naming system. Consider the following examples from a game:

```javascript
// Consistent naming
function getPlayerScore();
function getPlayerName();
function getPlayerTag();
```

They all follow the same naming system of “get a thing”. Now consider the following:

```javascript
// Inconsistent naming
function getUserScore();
function fetchPlayerName();
function retrievePlayer1Tag();
```

**Variables should preferably begin with a noun or an *adjective*, as they typically represent “things”.**
**Functions represent actions so ideally begin with a *verb*.**

```javascript
// Preferable
const numberOfThings = 10;
const myName = "Thor";
const selected = true;

// Not preferable (these start with verbs, could be confused for functions)
const getCount = 10;
const showNorseGods = ["Odin", "Thor", "Loki"];

// Preferable
function getCount() {
  return numberOfThings;
}

// Not preferable (myName doesn't represent some kind of action)
function myName() {
  return "Thor";
}
```

### Use searchable and immediately understandable names

```javascript
setTimeout(stopTimer, 3600000);
```

What does the number 3600000 mean? Even if you know that javascript reads in milliseconds, you’d probably need a calculator or Google to figure out how many seconds or minutes it represents.

```javascript
const ONE_HOUR = 3600000; // Can even write as 60 * 60 * 1000;

setTimeout(stopTimer, ONE_HOUR);
```

The variable is declared with a descriptive name, and you don’t need to perform any calculations when reading this code.

### Indentation and line length

```javascript
// This line is a bit too long
let reallyReallyLongLine = something + somethingElse + anotherThing + howManyTacos + oneMoreReallyLongThing;

// You could format it like this
let reallyReallyLongLine =
  something +
  somethingElse +
  anotherThing +
  howManyTacos +
  oneMoreReallyLongThing;

// Or maybe like this
let anotherReallyReallyLongLine = something + somethingElse + anotherThing +
                                  howManyTacos + oneMoreReallyLongThing;
```

## Comments

Comments are a useful tool, but beginners tend to overuse them. Most of the time, clear code should speak for itself, and comments should only fill in what the code can’t say.

Code tells you how, comments tell you why. The code already shows what it does, so a comment that repeats it is just noise. A good comment explains the reason behind a decision, or something that isn’t obvious from reading the code

```javascript
// Bad: repeats what the code already says
// Add 1 to counter
counter = counter + 1;

// Good: explains a reason the code can't show
// The API counts pages from 1, but our array starts at 0
const pageIndex = apiPage - 1;
```

Try to make the code clear first. Before adding a comment, see if a better variable or function name removes the need for it. Add a comment only when the code can’t be made any clearer.

```javascript
// Needs a comment
// check if user is old enough
if (a >= 18) { ... }

// Doesn't need one
if (userAge >= MINIMUM_AGE) { ... }
```

Don’t use comments for things git already does.

- Don’t keep a change history in comments (who changed what, and when). Use git log.
- Don’t leave old code commented out. Delete it, since you can always get it back from your commits.
- Commenting something out while you test is fine, but clean it up afterwards.

Rules of thumb

- Don’t comment everything. More comments don’t make code more readable.
- If you feel the code is too confusing without comments, rewrite it before explaining it.
- Good comments are short, clear, and written for another person, not the computer.

---

# Loops and arrays

## Loops

Loops are a way to repeat the same code multiple times.

### `for` statement

A `for` loop repeats until a specified condition evaluates to false. 

```javascript
for (initialization; condition; afterthought)
  statement
```

When a `for` loop executes, the following occurs:

1. The initializing expression `initialization`, if any, is executed. This expression usually initializes one or more loop counters, but the syntax allows an expression of any degree of complexity. This expression can also declare variables.

2. The `condition` expression is evaluated. If the value of `condition` is true, **the loop statements execute**. Otherwise, the `for` loop terminates. (If the `condition` expression is omitted entirely, the `condition` is assumed to be true.)

3. The `statement` executes. To execute multiple statements, use a block statement (`{ }`) to group those statements.

4. If present, the update expression `afterthought` is executed. But only **after** the codintion was `true` and the statement was executed.

2. Control returns to Step 2.

**Example:**

```javascript
for (let i = 0; i < 100; i++) {
  //code to repeat
}
```

1. Initialization (let i = 0): runs once, at the start. It creates the variable i and sets it to 0.
2. Condition (i < 100): checked before every repetition. If it’s true, the code inside runs. If it’s false, the loop stops.
3. Increment (i++): runs after every repetition and adds 1 to i.
 
### `do...while` statement

The do...while statement repeats until a specified condition evaluates to false.

```javascript
do
  statement
while (condition);
```

If condition is true, the statement executes again. At the end of every execution, the condition is checked. When the condition is false, execution stops, and control passes to the statement following do...while.

**Example:**

```javascript
let i = 0;
do {
  i += 1;
  console.log(i);
} while (i < 5);
```

### `while` statement

A while statement executes its statements as long as a specified condition evaluates to true. A while statement looks as follows:

```js
while (condition)
  statement
```
If the condition becomes false, statement within the loop stops executing and control passes to the statement following the loop.

### `for...of` statement

```js
const cats = ["Leopard", "Serval", "Jaguar", "Tiger", "Caracal", "Lion"];

for (const cat of cats) {
  console.log(cat);
}
```

In this example, for (const cat of cats) says:

1. Given the collection cats, get the first item in the collection.
2. Assign it to the variable cat and then run the code between the curly braces {}.
3. Get the next item, and repeat Step 2 until you've reached the end of the collection.

We could rewrite that code like this:

```js
const cats = ["Leopard", "Serval", "Jaguar", "Tiger", "Caracal", "Lion"];

for (let i = 0; i < cats.length; i++) {
  console.log(cats[i]);
}
```

In this loop we're starting i at 0, and stopping when i reaches the length of the array. Then inside the loop, we're using i to access each item in the array in turn.

This works just fine, and in early versions of JavaScript, for...of didn't exist, so this was the standard way to iterate through an array. However, it offers more chances to introduce bugs into your code. For example:

    you might start i at 1, forgetting that the first array index is zero, not 1.
    you might stop at i <= cats.length, forgetting that the last array index is at length - 1.

For reasons like this, it's usually best to use for...of if you can.

### map() and filter()

You can use map() to do something to each item in a collection and create a new collection containing the changed items:

```js
function toUpper(string) {
  return string.toUpperCase();
}

const cats = ["Leopard", "Serval", "Jaguar", "Tiger", "Caracal", "Lion"];

const upperCats = cats.map(toUpper);

console.log(upperCats);
// [ "LEOPARD", "SERVAL", "JAGUAR", "TIGER", "CARACAL", "LION" ]
```

Here we pass a function into cats.map(), and map() calls the function once for each item in the array, passing in the item. It then adds the return value from each function call to a new array, and finally returns the new array. In this case the function we provide converts the item to uppercase, so the resulting array contains all our cats in uppercase.

You can use `filter()` to test each item in a collection, and create a new collection containing only items that match:

```js
function lCat(cat) {
  return cat.startsWith("L");
}

const cats = ["Leopard", "Serval", "Jaguar", "Tiger", "Caracal", "Lion"];

const filtered = cats.filter(lCat);

console.log(filtered);
// [ "Leopard", "Lion" ]
```

This looks a lot like map(), except the function we pass in returns a boolean: if it returns true, then the item is included in the new array. Our function tests that the item starts with the letter "L", so the result is an array containing only cats whose names start with "L".

### Exiting loops with break 

If you want to exit a loop before all the iterations have been completed, you can use the break statement.
Normally, a loop exits when its condition becomes falsy. But we can force the exit at any time using the special break directive. For example, the loop below asks the user for a series of numbers, “breaking” when no number is entered:

```js
let sum = 0;

while (true) {

  let value = +prompt("Enter a number", '');

  if (!value) break; // (*)

  sum += value;

}
alert( 'Sum: ' + sum );
```

The break directive is activated at the line (*) if the user enters an empty line or cancels the input. It stops the loop immediately, passing control to the first line after the loop. Namely, alert.

The combination “infinite loop + break as needed” is great for situations when a loop’s condition must be checked not in the beginning or end of the loop, but in the middle or even in several places of its body.

### Skipping iterations with `continue`

`continue` works like `break`, but instead of ending the loop, it skips the current iteration and moves on to the next one.

Example: The loop below uses continue to output only odd values:

```javascript
for (let i = 0; i < 10; i++) {

  // if true, skip the remaining part of the body
  if (i % 2 == 0) continue;

  alert(i); // 1, then 3, 5, 7, 9
}
```
For even values of i, the continue directive stops executing the body and passes control to the next iteration of for (with the next number). So the alert is only called for odd values.

# Arrays in JavaScript

## 1. What is an array?

An array is an **ordered list** of values. Each value has a position called an **index**, starting from **0**. Arrays can hold any type of value, even mixed.

```js
let empty = [];                                  // recommended
let colors = ["red", "green", "blue"];
let mixed = [42, "text", true, { id: 1 }, [1, 2]];
let alt = new Array("a", "b");                   // works, but rarely used
```

> Prefer `[]` over `new Array()`. The constructor has a trap: `new Array(3)` creates **3 empty slots**, not `[3]`.

A trailing comma is allowed, which makes adding lines easier:

```js
let tools = [
  "hammer",
  "saw",
  "drill",   // trailing comma is fine
];
```

## 2. Reading and changing elements

```js
let colors = ["red", "green", "blue"];

colors[0];                    // "red"
colors[2];                    // "blue"
colors[1] = "yellow";         // replace
colors[3] = "pink";           // add at the end of the list
colors.length;                // 4
```

### Getting the last element

```js
colors[colors.length - 1];    // classic way
colors.at(-1);                // modern way: negative index counts from the end
colors.at(-2);                // second to last
```

> `colors[-1]` does **not** work: it looks for a property named `"-1"` and returns `undefined`. Use `.at(-1)`.

## 3. Length

`length` is **the last index + 1**, not strictly the count of elements.

```js
let a = [];
a[99] = "x";
a.length;     // 100 (the other 99 slots are empty "holes")
```

`length` is writable:

```js
let nums = [1, 2, 3, 4, 5];

nums.length = 2;   // truncates: [1, 2]  (removed values are gone for good)
nums.length = 5;   // [1, 2, <3 empty items>]  (values do NOT come back)
nums.length = 0;   // simplest way to clear an array
```

## 4. Adding and removing: the four basic methods

| Method | Where | Action | Returns |
|--------|-------|--------|---------|
| `push(x)` | end | adds | new length |
| `pop()` | end | removes | removed element |
| `unshift(x)` | start | adds | new length |
| `shift()` | start | removes | removed element |

```js
let q = ["b", "c"];

q.push("d");       // ["b", "c", "d"]
q.pop();           // returns "d"  → ["b", "c"]
q.unshift("a");    // ["a", "b", "c"]
q.shift();         // returns "a"  → ["b", "c"]

q.push("x", "y");  // several at once: ["b", "c", "x", "y"]
```

### Stack and queue

- **Stack** (last in, first out): `push` + `pop`
- **Queue** (first in, first out): `push` + `shift`

### Why `push`/`pop` are faster than `shift`/`unshift`

Changing the **end** touches only one element. Changing the **start** forces the engine to **renumber every other element**, which gets slower as the array grows.

## 5. Looping over an array

```js
let fruits = ["apple", "orange", "plum"];

// 1. Classic for: gives you the index
for (let i = 0; i < fruits.length; i++) {
  console.log(i, fruits[i]);
}

// 2. for...of: gives you the elements (best for simple loops)
for (let fruit of fruits) {
  console.log(fruit);
}

// 3. forEach: callback with element, index, array
fruits.forEach((fruit, i) => console.log(i, fruit));
```

### How the classic `for` runs

```js
for (let i = 0; i < 3; i++) { /* body */ }
```

1. `let i = 0` runs **once**
2. check `i < 3`
3. run the body
4. run `i++` (**after** the body)
5. back to step 2

### Avoid `for...in` on arrays

```js
for (let key in fruits) { }   // works, but it's meant for object properties
```

It iterates over **all** enumerable properties (including non-index ones), it is slower, and it returns keys as strings. Use `for...of` instead.

## 6. Arrays are objects

An array is a special kind of **object**. That explains some odd behavior.

### Copy by reference

```js
let a = ["x", "y"];
let b = a;          // b points to the SAME array

b.push("z");
a;                  // ["x", "y", "z"]  ← changed too!

let copy = [...a];  // real (shallow) copy
let copy2 = a.slice();
```

### You can add named properties (but shouldn't)

```js
let list = [1, 2];
list.label = "my list";   // works, because an array is an object

list.length;              // still 2: named properties don't count
```

Doing this breaks the engine's array optimizations. Use arrays for **ordered lists**, objects for **named data**.

### Avoid these patterns

- Adding elements far beyond the end (`arr[99999] = 1`), which creates holes
- Filling the array in reverse order
- Mixing named properties and indexes

## 7. Multidimensional arrays (arrays of arrays)

```js
let grid = [
  [1, 2, 3],   // grid[0]
  [4, 5, 6],   // grid[1]
  [7, 8, 9]    // grid[2]
];

grid[0][1];    // 2  → row 0, column 1
grid[2][0];    // 7
```

Read it left to right: `grid[0]` is the first inner array, then `[1]` picks its second element.

| | col 0 | col 1 | col 2 |
|---|---|---|---|
| **row 0** | 1 | **2** | 3 |
| **row 1** | 4 | 5 | 6 |
| **row 2** | 7 | 8 | 9 |

Looping over every cell:

```js
for (let row of grid) {
  for (let cell of row) {
    console.log(cell);
  }
}
```

## 8. Arrays and strings: `toString`

Arrays convert to a comma-separated string:

```js
String([1, 2, 3]);    // "1,2,3"
[] + "";              // ""
[1] + "";             // "1"
[1, 2] + 1;           // "1,21"   (array → string, then concatenation)
```

Arrays have **no** `Symbol.toPrimitive` or useful `valueOf`, so every conversion falls back to `toString`. That's why `+` never "adds" arrays.

## 9. Comparing arrays

Arrays are objects, so comparison works by **reference**, not by content.

```js
[1] === [1];         // false (two different objects)
[] === [];           // false

let a = [1];
let b = a;
a === b;             // true (same object)
```

### Don't use `==` with arrays

```js
0 == [];             // true   (surprising!)
"0" == [];           // false
```

`[]` is converted to `""`, then to `0`, which creates confusing results.

### Comparing contents

Compare element by element:

```js
function sameArray(a, b) {
  return a.length === b.length && a.every((v, i) => v === b[i]);
}

sameArray([1, 2], [1, 2]);   // true
```

## 10. Common mistakes

1. **Expecting `length` to count real elements**: holes are included.
2. **Using `arr[-1]`**: use `arr.at(-1)`.
3. **Copying with `=`**: it copies the reference. Use `[...arr]`.
4. **Comparing arrays with `===` or `==`**: compare contents instead.
5. **Using `+` to join arrays**: it makes a string. Use `concat` or spread.
6. **Using `shift`/`unshift` in big loops**: they are slow on large arrays.
7. **Using `for...in`**: prefer `for...of`.

## Cheat sheet

| I want to... | Code |
|--------------|------|
| create | `let a = [1, 2, 3];` |
| read first / last | `a[0]` / `a.at(-1)` |
| count elements | `a.length` |
| add / remove at the end | `a.push(x)` / `a.pop()` |
| add / remove at the start | `a.unshift(x)` / `a.shift()` |
| loop over elements | `for (let x of a) { }` |
| loop with index | `for (let i = 0; i < a.length; i++) { }` |
| clear | `a.length = 0` |
| copy | `[...a]` |
| check if it's an array | `Array.isArray(a)` |

---

# Array Methods in JavaScript

## How to read this guide

Array methods fall into two families:

- **Mutating**: they change the original array (`push`, `pop`, `splice`, `sort`, `reverse`...)
- **Non-mutating**: they return a new result and leave the original untouched (`slice`, `map`, `filter`, `concat`...)

When writing code, always ask yourself: *"does this method change the array or create a new one?"*

## 1. Adding, removing, inserting

### Quick recap

| Method | Where | What it does |
|--------|-------|--------------|
| `push(x)` | end | adds |
| `pop()` | end | removes and returns |
| `unshift(x)` | start | adds |
| `shift()` | start | removes and returns |

### `splice`: the Swiss Army knife (mutating)

```js
arr.splice(start, deleteCount, ...newItems)
```

It can **remove**, **insert** and **replace**, depending on how you use it.

```js
let a = ["a", "b", "c", "d"];

a.splice(1, 2);           // removes 2 elements from index 1
// a = ["a", "d"]

a.splice(1, 0, "X", "Y"); // 0 = remove nothing, inserts X and Y
// a = ["a", "X", "Y", "d"]

a.splice(1, 2, "Z");      // replaces 2 elements with "Z"
// a = ["a", "Z", "d"]
```

- It returns an array of the **removed** elements.
- A **negative** index counts from the end: `a.splice(-1, 1)` removes the last element.

### `slice`: copy a portion (non-mutating)

```js
arr.slice(start, end)   // "end" is EXCLUDED
```

```js
let a = ["a", "b", "c", "d", "e"];

a.slice(1, 3);   // ["b", "c"]
a.slice(-2);     // ["d", "e"]  (last two)
a.slice();       // copy of the whole array
```

> **Don't mix them up:** `slice` **copies**, `splice` **modifies**.

### `concat`: join arrays (non-mutating)

```js
let a = [1, 2];

a.concat([3, 4]);        // [1, 2, 3, 4]
a.concat([3], [4, 5]);   // [1, 2, 3, 4, 5]
a.concat(3);             // [1, 2, 3]
[...a, ...[3, 4]];       // [1, 2, 3, 4]  (modern spread alternative)
```

## 2. Iterating: `forEach`

Runs a function **for every element**. It returns nothing.

```js
["Anna", "Luke"].forEach((name, index, array) => {
  console.log(`${index}: ${name}`);
});
// 0: Anna
// 1: Luke
```

The function always receives three things: **the element**, **its index**, **the whole array**. Usually only the first two are used.

> Use `forEach` to *do something* with each element (print, save...).
> If you want to *get a new array*, use `map` or `filter`.

## 3. Searching

### Searching for an exact value

```js
let a = [5, 10, 15, 10];

a.indexOf(10);        // 1   (first position, or -1 if missing)
a.lastIndexOf(10);    // 3   (last position)
a.includes(15);       // true
a.includes(99);       // false
```

### Searching with a condition

When an exact value isn't enough (for example you need to find an object by `id`), pass a function that returns `true` or `false`:

```js
let users = [
  { id: 1, name: "John" },
  { id: 2, name: "Pete" },
  { id: 3, name: "Mary" }
];

users.find(u => u.id === 2);        // { id: 2, name: "Pete" }
users.findIndex(u => u.id === 2);   // 1
users.findLast(u => u.id < 3);      // { id: 2, name: "Pete" } (searches from the end)
```

- `find` → returns **the element** found (or `undefined`)
- `findIndex` → returns **the position** (or `-1`)
- Both stop at the **first** match

### `filter`: all elements that match

```js
users.filter(u => u.id < 3);
// [{ id: 1, name: "John" }, { id: 2, name: "Pete" }]
```

| | `find` | `filter` |
|---|---|---|
| Returns | one element | an array |
| Stops at first match? | yes | no |
| If nothing matches | `undefined` | `[]` |

## 4. Transforming: `map`

Applies a function to **every element** and returns a **new array** with the results. Same length as the original.

```js
["Bilbo", "Gandalf", "Nazgul"].map(s => s.length);
// [5, 7, 6]

[1, 2, 3].map(n => n * 2);
// [2, 4, 6]

users.map(u => u.name);
// ["John", "Pete", "Mary"]
```

| | `filter` | `map` |
|---|---|---|
| Purpose | **choose** which to keep | **transform** each one |
| Result length | can be shorter | same as original |

## 5. Sorting

### `sort`: careful, it sorts as TEXT (mutating)

```js
[1, 2, 15].sort();   // [1, 15, 2]  ← wrong for numbers!
```

With no arguments, `sort` converts everything to strings and compares character by character: `"15"` comes before `"2"` because `"1"` < `"2"`.

### The compare function

To sort numbers, pass a function that receives **two values** (`a` and `b`) and returns a number:

| Result | Meaning |
|--------|---------|
| positive | `a` goes **after** `b` |
| `0` | they are equal |
| negative | `a` goes **before** `b` |

```js
[1, 2, 15].sort((a, b) => a - b);   // [1, 2, 15]  ascending
[1, 2, 15].sort((a, b) => b - a);   // [15, 2, 1]  descending
```

`a` and `b` are just **placeholders**: `sort` calls your function many times with different pairs of elements until the array is ordered. You only write the rule.

### Sorting text with accented letters

```js
["Österreich", "Andorra", "Vietnam"].sort((a, b) => a.localeCompare(b));
```

`localeCompare` respects language rules (accents, case).

### Sorting objects by a property

```js
users.sort((a, b) => a.name.localeCompare(b.name));  // by name
users.sort((a, b) => a.id - b.id);                   // by id
```

### `reverse`: reverses the order (mutating)

```js
[1, 2, 3].reverse();   // [3, 2, 1]
```

## 6. Strings ↔ arrays

```js
"a,b,c".split(",");           // ["a", "b", "c"]
"hello".split("");            // ["h", "e", "l", "l", "o"]
"a,b,c,d".split(",", 2);      // ["a", "b"]  (limit)

["a", "b", "c"].join("-");    // "a-b-c"
["a", "b", "c"].join("");     // "abc"
```

`split` goes from string to array, `join` does the reverse.

## 7. Reducing to a single value: `reduce`

```js
arr.reduce((accumulator, element, index, array) => {
  return newAccumulator;
}, initialValue);
```

The **accumulator** is a value that carries the partial result from one round to the next.

```js
[1, 2, 3, 4].reduce((sum, n) => sum + n, 0);   // 10
```

Round by round:

| round | `sum` (before) | `n` | returns |
|-------|----------------|-----|---------|
| 1 | 0 (initial value) | 1 | 1 |
| 2 | 1 | 2 | 3 |
| 3 | 3 | 3 | 6 |
| 4 | 6 | 4 | 10 |

Another example: finding the largest number.

```js
[3, 9, 4].reduce((max, n) => (n > max ? n : max), 0);   // 9
```

> **Always pass the initial value** (`0` in the example). Without it, `reduce` on an empty array throws an error.

`reduceRight` works the same but starts from the last element.

## 8. Useful checks

```js
Array.isArray([1, 2]);   // true
Array.isArray({});       // false
typeof [1, 2];           // "object" (doesn't tell arrays apart!)

[1, 2, 3].some(n => n > 2);    // true: AT LEAST ONE matches
[1, 2, 3].every(n => n > 0);   // true: ALL of them match
```

## 9. Other handy methods

```js
// fill: fills with a value (mutating)
new Array(3).fill(0);          // [0, 0, 0]

// flat: flattens nested arrays
[1, [2, [3]]].flat();          // [1, 2, [3]]
[1, [2, [3]]].flat(2);         // [1, 2, 3]

// Array.from: creates an array from something iterable
Array.from("abc");             // ["a", "b", "c"]
Array.from({ length: 3 }, (_, i) => i * 2);   // [0, 2, 4]
```

## 10. Chaining methods

Since `filter` and `map` return arrays, you can chain them one after another:

```js
let prices = [10, 25, 8, 40, 15];

let total = prices
  .filter(p => p > 9)       // [10, 25, 40, 15]
  .map(p => p * 1.22)       // adds VAT
  .reduce((s, p) => s + p, 0);
```

Read it top to bottom: *"keep those above 9, apply VAT, add them up"*.

## Summary table

| I want to... | Method | Mutates the original? |
|--------------|--------|-----------------------|
| add/remove at the end | `push` / `pop` | yes |
| add/remove at the start | `unshift` / `shift` | yes |
| remove/insert/replace | `splice` | yes |
| copy a portion | `slice` | no |
| join arrays | `concat`, `[...a, ...b]` | no |
| do something for each element | `forEach` | no |
| check if a value exists | `includes` | no |
| find the position of a value | `indexOf` | no |
| find an element by condition | `find` / `findIndex` | no |
| keep only some elements | `filter` | no |
| transform every element | `map` | no |
| sort | `sort` | **yes** |
| reverse | `reverse` | **yes** |
| reduce to a single value | `reduce` | no |
| at least one / all match | `some` / `every` | no |
| split/join strings | `split` / `join` | no |

---

## Common mistakes to avoid

1. **`sort()` on numbers without a function**: it sorts as text.
2. **Mixing up `slice` and `splice`**: one copies, the other modifies.
3. **Using `map` when you don't need the result**: if you just want to "do something", use `forEach`.
4. **Forgetting the initial value in `reduce`**.
5. **Thinking `sort` and `reverse` make a copy**: they modify the original array. To keep it intact, copy first: `[...arr].sort(...)`.
6. **Comparing arrays with `===`**: `[1] === [1]` is `false`, because it compares references.
