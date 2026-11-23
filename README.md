<div align="center">

# My Web Development Studies

</div>

**Most of the content in my notes comes from The Odin Project, MDN Web Docs and JavaScript.info.**

## Table of Contents

*   [Week 1: Fundamentals of the Web, HTML & CSS Foundations]
*   [Week 2: JavaScript Foundations & flexbox]

---

### Week 1: Fundamentals of the Web

*   **How the Web Works:** 
    *   Internet, IP and MAC addresses
    *   DNS, Clients, and Servers
    *   TCP/IP protocol, HTTP, and status codes
*   **Work Environment:** 
    *   VS Code, Command Line, Git & GitHub
*   **HTML (Structure):** 
    *   Elements, attributes, and boilerplate structure (`<!DOCTYPE>`, `head`, `meta`, `body`)
    *   Text, lists, links, and images
*   **CSS (Style):** 
    *   Selectors, specificity, and inheritance
    *   The DOM, the Box Model, `box-sizing`, and the `display` property

---

### Week 2: Advanced Layouts & JavaScript Foundations

*   **Flexbox:** 
    *   Flex containers and flex items
    *   Sizing properties (`flex-grow`, `flex-shrink`, `flex-basis`) and direction (`flex-direction`)
    *   Alignment (`justify-content`, `align-items`, `align-self`, `gap`, `flex-wrap`, `align-content`)
*   **How a Computer Works:** 
    *   Machine code, compilers, compiled vs. interpreted languages
    *   How the browser executes JavaScript
*   **JavaScript Basics:** 
    *   The role of JS alongside HTML and CSS, plus Browser APIs
    *   `console.log`, comments, variables (`let`, `const`), naming rules, and clean code
    *   Numbers, operators, and string concatenation
*   **Data Types:** 
    *   Primitives and Objects: `number`, `string`, `boolean`, `null`, `undefined`, `objects`, `symbols`
    *   Template literals and the `typeof` operator

---

### Week 3: Conditionals, Strings & Functions

*   **Variables, Classes & Objects:**
    * Variable recap: `let`, name, assignment `=`, value
    * Classes as blueprints (properties, methods) and objects built with `new`
*   **Strings:**
    * Quotes (single, double, backticks) and template literals with `${...}`
    * Primitives vs. `String` objects, and the automatic wrapper that lets primitives use methods
    * Basic methods: `length`, `charAt()`, `at()`, `slice()`, `substring()`, `toUpperCase()`, `toLowerCase()`, `trim()`, `padStart()`, `repeat()`, `replace()`, `replaceAll()`, `split()`
*   **Comparisons & Conditionals:**
    * Comparison operators, returning booleans, string (lexicographical) comparison, and type conversion
    * Strict equality (`===`, `!==`) vs. loose equality (`==`)
    * `if ... else`, `else if`, nesting, and truthy/falsy values
    * Logical operators `&&`, `||`, `!`, precedence, and short-circuit evaluation
    * `switch` (with `break`, `default`, and grouped cases) and the ternary operator
*   **Developer Tools:**
    * Opening Chrome DevTools, the Sources panel, and the Console
    * Breakpoints, the `debugger` command, and stepping through code (Resume, Step, Step over, Step out)
    * Inspecting and editing CSS with the Elements/Styles panel
*   **Functions:**
    * Declaration, parameters, arguments, and `return`
    * Local vs. outer variables, shadowing, and default parameter values
    * Naming conventions (verb prefixes) and the "one function, one action" rule
    * Functions vs. methods

---

### Week 4: Events, Functions & Debugging

*   **Events & Properties:**
    * Events as strings (`"keydown"`, `"click"`, `"submit"`) and `addEventListener`
    * The `event` object and its properties (`event.key`, `textBox.value`)
    * Properties vs. methods
    * Passing a function vs. calling it (`logKey` vs. `logKey()`)
*   **Advanced Functions:**
    * Function scope: local vs. global
    * Function expressions vs. function declarations (hoisting)
    * Callback functions
    * Arrow functions
*   **Call Stack:**
    * Single-threaded, LIFO execution and stack overflow
*   **Problem Solving:**
    * Understanding the problem, planning, pseudocode, and divide and conquer
*   **Understanding Errors:**
    * Error anatomy (type, message, location, stack trace)
    * `SyntaxError`, `ReferenceError`, `TypeError`
    * Debugging process: `console.log()`, `console.table()`, `console.trace()`, and the debugger

---

### Week 5: Clean Code, Loops & Arrays

*   **Clean Code:** 
    *   camelCase naming convention
    *   Meaningful names for variables and functions
    *   Consistent vocabulary (variables as nouns or adjectives, functions as verbs)
    *   Searchable and immediately understandable names (avoiding magic numbers, e.g. `ONE_HOUR`)
    *   Indentation and line length
    *   Comments: code tells you "how", comments tell you "why"
    *   Don't use comments for things Git already does
*   **Loops:** 
    *   `for` statement (initialization, condition, afterthought)
    *   `while` and `do...while`
    *   `for...of` and why it is safer than the classic `for` with an index
    *   `break` and `continue`
    *   `map()` and `filter()` with callback functions
*   **Arrays:** 
    *   Ordered lists, indexes starting from 0, and `length`
    *   Reading and changing elements, and `at(-1)` for the last element
    *   `push()`, `pop()`, `unshift()`, `shift()`, and stack vs. queue
    *   Looping over arrays (`for`, `for...of`, `forEach`) and why to avoid `for...in`
    *   Arrays are objects: copy by reference vs. shallow copy (`[...arr]`)
    *   Multidimensional arrays (arrays of arrays)
    *   Array to string conversion and comparing arrays by reference
*   **Array Methods:** 
    *   Mutating vs. non-mutating methods
    *   `splice()` vs. `slice()`, and `concat()`
    *   Searching: `indexOf()`, `includes()`, `find()`, `findIndex()`
    *   Transforming and filtering: `map()`, `filter()`
    *   `sort()` with a compare function, and `reverse()`
    *   `split()` and `join()`
    *   `reduce()` and the accumulator
    *   `some()`, `every()`, `Array.isArray()`, and method chaining
