<!--
															  Boxes
                                                        The box model
Every single thing on a website is a rectangular box. These boxes can have other boxes inside of them. They are many ways to 
manipulate the size of these boxes, and the space between them, using padding, border and margin.
- content box: The area where your content is displayed; size it using properties like width and height;
- padding increases the space between the border of a box and the content of the box. Unlike margins, you cannot have a negative 
padding.

Border

Borders adds space between the margin and the padding. If you are using the standard box model, the size of the border is added 
to the width and height of the content box. If you are using the alternative box model, then the bigger the border is, the smaller 
the content box is, as the border takes up some of that available width and height of the element box. For styling borders, there 
are a large number of properties — there are four borders, and each border has a style, width, and color that we might want to manipulate.
To set the properties of each side individually, use:

    • border-top 
    • border-right 
    • border-bottom 
    • border-left 

To set the width, style, or color of all sides, use: border-width, border-style, border-color. To set the width, style, or color 
of a single side, use one of the more granular longhand properties like “border-top-width”, “border-left-style” and so on. 

Margin

Margin is an invisible space, inreases the space between the borders of a box and the borders of adjacent boxes. Margins can have 
negative and positive value, depending on whether two elements whose margins touch have positive or negative margins, the results will be different:

    • Two positive margins will combine to become one margin. Its size will be equal to the largest individual margin. 
    • Two negative margins will collapse and the smallest (furthest from zero) value will be used. 
    • If one margin is negative, its value will be subtracted from the total.  
      
                                                         Elements proprieties

Every element comes with three most important factors:
Sizing: box-sizing;
Layout behavior: display (block, inline, flex, grid, none);
Other layout tools: float, position.


                                                                    BOX-SIZING

In the standard box model, the property box-sizing: content-box, if you set width and height property values on a box, these values 
define the width and height of the content box. Any padding and borders are then added to those dimensions to get the total size taken up by the box

.box {
 width: 350px;
 height: 150px;
 margin: 10px;
 padding: 25px;
 border: 5px solid black;
}

The actual space taken up by the box will be 410px wide (350 + 25 + 25 + 5 + 5) and 210px high (150 + 25 + 25 + 5 + 5).
Box-sizing: border-box
In the alternative box model, any width is the width of the visible box on the page. The content area width is that width minus the 
width for the padding and border (see image below). This is convenient as there is no need to add up the border and padding to get the 
real size of the box. To turn on the alternative model for an element, set box-sizing: border-box on it:

.box {
 width: 350px;
 height: 150px;
 margin: 10px;
 padding: 25px;
border: 5px solid black;
}
                                                                                          
                                                                     DISPLAY

Elements on a webpage lay out in normal flow if you haven’t applied any CSS to change the way they behave between each other. For 
example elements like <img> and <button> are by default with the “display: inline-block” propriety. The display property defines the 
relationships between multiple boxes in a different ways.

display: block
Displays an element as a block element (like <p>). It starts on a new line, and takes up the whole width

display: inline:
Respect left & right margins and padding, but not top & bottom.
Cannot have a width and height set.
Allow other elements to sit to their left and right. 

display: inline-block:
Allow other elements to sit to their left and right. 
Respect top & bottom margins and padding. 
Respect height and width. 

Use it if you do not want an item to break onto a new line, but do want it to respect width and height and avoid the overlapping seen above.
When building a web page, not every piece of content has a specific semantic tag. Sometimes, you just need a container you can style 
or position. That’s where <div> (block element) and <span> come in.

Particular elements

For elements the default behavior is  box-sizing: content-box, but there are some particular that have for default inline:

<img> is inline-block
<button> is inline-block
<span> is inline
<textarea> is inline
<input> is inline
<select> is inline-block

Inner and outer display types

Block and inline display values are said to be outer display types — they affect how the box is laid out in relation to other 
boxes around it. Boxes also have an inner display type, which dictates how elements inside that box are laid out.
You can change the inner display type by setting an inner display value, for example display: flex;. 
The element will still use the outer display type block but this changes the inner display type to flex. Any direct children of this box will become flex 
items and behave according to the Flexbox specification.

                                                              FLEXBOX
Flexbox - display: flex;

The main idea behind the flex layout is to give the container the ability to alter its items’ width/height (and order) to best 
fill the available space (mostly to accommodate to all kind of display devices and screen sizes). We use flexbox to organize 
items into rows or columns.This items will grow or shrink based on rules that you define. Adding <div> will show another box 
alongside the others, and everything will flex to fit  within the available area.

Flex containers and flex items

Flex is more than just a property, is a toolbox of properties where some of them belong on the flex container and som go on the 
flex items. A flex container is any element that has display: flex on it. A flex item is any element that is inside of that 
container. Any element can be at the same time a flex container and a flex item, when you code display: flex inside them.

Flex shorthand

The “flex” declaration is a shorthand for 3 properties that you can set on a flex item, they affect how flex items size themselves 
within their container, in this case: flex-grow, flex-shrink, flex-basis (flex: 1 1 0). So basically this values are needed when 
you risize your window browser, so that your boxes are going to resize equally.

Flex-grow

By default, elements in a Flexbox context will shrink down to their minimum comfortable size along the primary axis. Flex-grow 
is a single number value, that value is the grow factor. If you apply flex:1 to a container of divs, every div will grow the same 
amount. If you add flex:3 to just one div then that div would grow to x3 the size of the others. The default value is 1. 
Flex-grow controls how the extra space is distributed when the items are smaller than their container.

Flex-shrink

Similar to flex-grow, but sets the shrink factor of a flex element. Flex-shrink only ends up being applied if the size of all 
flex items is larger than their parent container. The default value is 1. flex-shrink controls how space is removed when the 
items are bigger than their container. When you don’want some of your items to shrink you can set flex-shrink: 0 to flex children.

Flex-basis

Flex-basis sets the initial size of a flex item, so any sort of flex-grow or flex-shrink starts from that baseline width size 
pegged to the primary axis. The default value is 0%, if you don’t set this value on “auto” those items would ignore the item’s 
width, and everything would shrink evenly. So auto tells the item to check for a width declaration.

Flex:auto sets your flex values like this: flex: 1 1 0%. Flex: 1 = 1 1 0%. In practice you will likely not be using complex 
values for flex-grow, flex-shrink or flex-basis. Generally, you’re most likely to use declarations like flex: 1; to make divs 
grow evenly and flex-shrink: 0 to keep certain divs from shrinking.

Flex-direction

The flex-direction property enables you to define how flex items are placed in a flex container. The default direction for a 
flex container is horizonal, or row, you can change it to vertical or column from flex-direction: column. This link explore 
more: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/flex-direction.

Alignment

So putting with display:flex in the container and flex: 1 makes each of the element grow and shrink equaly, but if you want 
them to stay in the same width, so with space between them, you should delete flex:1 and add to th container justify-content: space-between.
If you want them united in the center you can use  justify-content: center.
Setting gap on a flex container adds a specified space between flex items, similar to adding a margin to the items themselves. 
We can bunch all the items up in a particular spot (with flex-start, center, and flex-end), or we can spread them apart 
(with space-between, space-around, and space-evenly).

Align-self

Unlike justify-content and align-items, align-self is applied to the child element, not the container. It allows us to change 
the alignment of a specific child along the cross axis.

justify — to position something along the primary axis.
align — to position something along the cross axis.
content — a group of “stuff” that can be distributed.
items — single items that can be positioned individually.

min-width

By setting min-width: 0px directly on the Flexbox child, we tell the Flexbox algorithm to overwrite the “built-in” minimum width.

Flex-wrap

- flex-wrap: wrap gives us two rows of stuff.
- Within each row, align-items lets us slide each individual child up or down
- Zooming out, however, we have these two rows within a single Flexbox context! The cross axis will now intersect two rows, not 
one. And so, we can't move the rows individually, we need to distribute them as a group.
- Using our definitions from above, we're dealing with content, not items. But we're also still talking about the cross axis! 
And so the property we want is align-content.

                                                                           CAPTER III

                                      Introduction of how a computer works and JavaScript basics 	

A computer’s processor understands only machine code: sequences of 0s and 1s (binary). Each 0 or 1 is a bit, representing an 
electrical signal that is off or on. Every instruction and every piece of data, whether text, images or programs, is ultimately 
stored and processed in this form.
Humans can’t write programs comfortably in binary, so we write code in programming languages that are readable to us. This code 
must be translated into machine code before the processor can act on it.

What a compiler is

A compiler is a program that translates source code (written in a programming language) into machine code, or into another 
lower-level form that can be executed. Depending on the language, this translation can happen ahead of time, before the program 
runs (as in C), or during execution, as in just-in-time (JIT) compilation (as in modern JavaScript engines).
Compiled vs Interpreted

Compiled (C, C++)

A program called a compiler translates all your code into machine code once, ahead of time. The result is an executable binary 
file. Whoever uses it receives only that file, and the processor runs it directly. The source code is no longer needed.
Interpreted (e.g. JavaScript)

No binary is produced in advance. The browser already contains a program called a JavaScript engine (Chrome’s is called V8), 
which is itself compiled into machine code. When the browser receives your JavaScript as text, the engine reads it and carries 
out the corresponding actions as it goes. Your code never becomes a binary of its own: the engine, already in 0s and 1s, does the 
things your code describes.

An analogy: you need someone who only speaks Japanese to follow instructions.

    • Compiled: you translate the whole instruction manual into Japanese beforehand and hand it over. They read it directly. 
    • Interpreted: you hire an interpreter who stands next to them and translates sentence by sentence while they work. 
      The instructions stay in Italian, but the interpreter turns them into Japanese on the fly. 

So how does the browser understand JavaScript? The JavaScript engine is already installed in the browser and is made of 0s 
and 1s. Your JavaScript travels over the network as plain text (which is also 0s and 1s, but only as data, like any text file).
The engine then interprets its meaning and turns it into actions the processor can perform.
Why is JavaScript called “not compiled”? Because the distinction is about workflow, not physics:

    • In C: write, compile, distribute the binary, someone runs it. 
    • In JavaScript: write, distribute the text, and the engine translates and runs it on the spot, every time.	

JavaScript is a scripting or programming language that allows you to implement complex features on web pages. Without 
JavaScript your webpage, with only html and css, would be static information page, JavaScript is what makes your website 
interactive: content updates, interactive maps, antimated 2D/3D graphics, scrolling system, setc. The three layers build 
on top of one another:

    • HTML is the markup language that we use to structure and give meaning to our web content, for example defining 
paragraphs, headings, and data tables, or embedding images and videos in the page. 

    • CSS is a language of style rules that we use to apply styling to our HTML content, for example setting background 
colors and fonts, and laying out our content in multiple columns. 

    • JavaScript is a scripting language that enables you to create dynamically updating content, control multimedia,
animate images, and pretty much everything else. (Okay, not everything, but it is amazing what you can achieve with a few 
lines of JavaScript code.)

 Application programming Interfaces (APIs)

APIs are ready-made sets of code blocks that allow a developer to implement programs that would otherwise be hatd or 
impossible to implement. They do like IKEA ready-made furniture kits: you have already cut panels that you can screw 
together to make a bookshelf, you don’t need to find by yourself the wood, get measures, cut all the panels to the 
right size and shape, etc.
Browser APIs  are built into your web browser, and are able to expose data from the surrounding computer enviroment, 
and do useful things for developer:

    • The DOM (Document Object Model) API  allows you to manipulate HTML and CSS, creating, removing and changing HTML;
    •  The Geolocation API  retrieves geographical information, like in Google Maps;
    • The Canvas and WebGL APIs allow you to create animated 2D and 3D graphics;
    • Audio and Video APIs like HTMLMediaElement and  WebRTC allow you to customize things with multimedia, like play 
      audio and video in the webpage, show your webcam and display it on someone esle’s pc.

Third-party APIs  are not built into the browser by default, you can grab their code from somowhere like:

    • The Bluesky API allows you to do things like displaying your latest posts on your website;
    • The Google Maps API and OpenStreetMap API allows you ti embed custom maps into your website, and other functionality.

                                      What is JavaScript doing on your page: brief recap

When you load a web page in a browser, you are running your code (HTML, CSS, JavaScript) inside an execution environment 
(browser tab). It takes raw materials (the code) and outputs a product: the web page. It is a common habit to use JavaScript 
to modify HTML and CSS via the DOM API.

                                                        Browser security

Each browser tab has his own separate blocks of code called “execution environments”. So each tab run separately, 
and they can’t affect each other. This is a good securety measure, if this were not the case then pirates could 
start writing code to steal information from other websites.

JavaScript running order

When the browser encounters a block of JavaScript, it generally runs it in order, from top to bottom. This means 
that you need to be careful what order you put things in

Internal JavaScript

For the foundations of JavaScript is recommended to use the Internal link, through the browser. For start, you need 
to put this at the end of your <body>:

<script>
    console.log("Hello, World!")
</script>

Your code won’t work if the JavaScript is loaded and parsed before the HTML, and error could happens if you put 
it before the end of the body.
Save and open in live browser, so to begin you should write your code directly in your browser:
- F12;
- Find and select the “Console” tab, where you should see the output of our console.log statement.

Console.log is the command to print something to the developer console in your browser.
Another way to include JavaScript is a webpage is through an external script: <script src="javascript.js"></script>.
External are used for more complex scripts, but for now is recommended usining throgh the browser.

Comments

Before you start learning to code, it is good  -m "Update README"practice to remember to leave comments in your code. Comments do not
affect how the code runs, but they can be very useful for giving instructions to other developers, or even to yourself.
To write a comment you will use this form:
// I am a comment          /* I am also a comment* /        

Variables

Variables are the building block of any program: they are storage containers for data in your code. Variables are 
structured by a declaration (let), variable (firstName) and the value of the variable (Leo). The assignment operator 
is =. When the type of the value is surrounded by quotes we call it string. 
You can declare variebles using the let keyword.

let firstName = "John";
let lastName = "Doe";

Using console.log() you ask a program for an output in this case it would be:

console.log(firstName);
John
console.log(lastName);
Doe

You can also re-assign variables:

firstName = “Ethan”              console.log(firstName); Ethan

We can also declare two variables and copy data from one into the other:

let hello = 'Hello world!';
let message;

message = hello;

Since the variable has already been declared earlier we don’t need to use let again. But if we want a constant 
which will never need to be re-assigned, we can use const keyword:

const pi = 3.14;
pi = 10;
ERROR

If you try to re-assign the constant an error is going to pop. In old school code you will quite probably find 
var instead of let but they are very similar with some different quirks.

Variable naming 

They are limitations on variable names in JavaScript:
1. The name must contain only letters, digits, or the symbols $ and _ 
2. The first character must not be a digit.
3. There a list of reserved words, which cannot be used as variable like: let, class, return, function.

Write clean code

A variable name should have a clean, ovious meaning, describing the data that it stores. Variable naming is one 
of the most important skills in programming. In real project, most of the time is spent modifying and extending 
an existing code base, so it is always reccomendet to make it clear for everybody.

Some good-to-follow rules are:

    • Use human-readable names like userName or shoppingCart. 
    • Stay away from abbreviations or short names like a, b, and c, unless you know what you’re doing. 
    • Make names maximally descriptive and concise. Examples of bad names are data and value. Such names say 
      nothing. It’s only okay to use them if the context of the code makes it exceptionally obvious which data or 
      value the variable is referencing. 
    • Agree on terms within your team and in your mind. If a site visitor is called a “user” then we should 
      name related variables currentUser or newUser instead of currentVisitor or newManInTown. 

For the sake of better readability you should use a single line per variable, and not something like this 
(that would still run the code): let user = 'John', age = 25, message = 'Hello';

                                                         Numbers in JavaScript

Numbers in JavaScript use the standard mathematical Order of Operations PEMDAS: parentheses, exponentiation,
multiplication, addition and substraction. Number values are typed in without quote marks.
Assignment operators
Assignment operators are operators that assign a value to a variable.

let x = 3;  x contains the value 3
let y = 4;   y contains the value 4
x = y;      x now contains the same value y contains, 4

Chaining assignments:   let a, b, c;

	  		        a = b = c = 2 + 2;

			   alert( a ); // 4
	   		   alert( b ); // 4
			   alert( c ); // 4

Increment/Decrement

The operators ++ and -- can be placed either before or after a variable.

    • When the operator goes after the variable, it is in “postfix form”: counter++. 
    • The “prefix form” is when the operator goes before the variable: ++counter. 

Both of these statements do the same thing: increase counter by 1.
If we’d like to increase a value and immediately use the result of the operator, we need the prefix form:

let counter = 0;
alert( ++counter ); // 1

If we’d like to increment a value but use its previous value, we need the postfix form:

let counter = 0;
alert( counter++ ); // 0

Remainder %
The remainder operator %, despite its appearance, is not related to percents.
alert( 8 % 3 ); // 2, the remainder of 8 divided by 3

Exponentiation **
The exponentiation operator a ** b raises a to the power of b.
alert( 2 ** 2 ); // 2² = 4

String concatenation with binary +
If the binary + is applied to strings, it merges (concatenates) them:

let s = "my" + "string";
alert(s); // mystring

Note that if any of the operands is a string, then the other one is converted to a string too.

alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
alert(2 + 2 + '1' ); // "41" and not "221"
alert('1' + 2 + 2); // "122" and not "14"

If the first operand is a string, the compiler treats the other two operands as strings too. The 2 gets 
concatenated to '1', so it’s like '1' + 2 = "12" and "12" + 2 = "122".
The binary + is the only operator that supports strings in such a way. Other arithmetic operators work only 
with numbers and always convert their operands to numbers.
The need to convert strings to numbers arises very often. For example, if we are getting values from HTML
form fields, they are usually strings. What if we want to sum them?
The binary plus would add them as strings:

let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23", the binary plus concatenates strings
If we want to treat them as numbers, we need to convert and then sum them:

let apples = "2";
let oranges = "3";
alert( +apples + +oranges ); // 5

Bitwise operators (mostly used in cryptography)

    • AND (&)
    • OR ( | ) 
    • XOR ( ^ ) 
    • NOT ( ~ ) 
    • LEFT SHIFT ( << ) 
    • RIGHT SHIFT ( >> ) 
    • ZERO-FILL RIGHT SHIFT ( >>> )

Comma operators
The comma operator allows us to evaluate several expressions, dividing them with a comma ,. Each of them is 
evaluated but only the result of the last one is returned.
let a = (1 + 2, 3 + 4);
alert( a ); // 7 (the result of 3 + 4)
Comma has a very low precedence!

Please note that the comma operator has very low precedence, lower than =, so parentheses are important in 
the example above. Without them: a = 1 + 2, 3 + 4 evaluates + first, summing the numbers into a = 3, 7, then 
the assignment operator = assigns a = 3, and the rest is ignored. It’s like (a = 1 + 2), 3 + 4.


                                                          CAPTER IV
                                             Data types and Conditionals: the first look
A data type is a collection or grouping of data values, usually specified by a set of possible values, a set of 
allowed operations on these values, and/or a representation of these values as machine types. Most common type of 
data are number and strings. 

Numbers type

In JavaScript numbers cannot be larger than (253-1) or less than -(253-1) . But sometimes, for cryptography perhaps,
we would need larger numbers. For that we have the BigInt type that will go even further.
String type
A string, as we said before, is an information surrounded by quotes let str = "Hello"; 

- Double quotes: "Hello"
- Single quotes: 'Hello'
- Backticks: `Hello`

There is no difference using a single or double quote format. Backticks are “extended functionality” quotes. They 
allow us to embed variables and expressions into a string by wrapping them in ${…}, for example:

let name = "John";
// embed a variable
alert( `Hello, ${name}!` ); // Hello, John!
// embed an expression
alert( `the result is ${1 + 2}` ); // the result is 3

The expression inside ${…} is evaluated and the result becomes a part of the string. We can put anything in there: 
a variable like name or an arithmetical expression like 1 + 2 or something more complex.

NOTE:

In some languages, there is a special “character” type for a single character. For example, in the C language and in 
Java it is called “char”. In JavaScript, there is no such type. There’s only one type: string. A string may consist
of zero characters (be empty), one character or many of them.

Logical type: Boolean

The boolean type has only two values: true and false.
let isGreater = 4 > 1;
alert( isGreater ); // true (the comparison result is "yes")
let nameFieldChecked = true; // yes, name field is checked
let ageFieldChecked = false; // no, age field is not checked

Special values

:undefined
The special value undefined is “value is not assigned”:  
let age;
alert(age); // shows "undefined"

:null 

It’s a special value which represents “nothing”, “empty” or “value unknown”.
let age = null;

Objects and Symbols
All other types are primitive because their values can contaion only a single thing. Objects are used to store collections
of data and more complex entitiese.
The symbol type is used to create unique identifiers for objects.

The typeof operator returns the type of the operand:

typeof undefined // "undefined"
typeof 0 // "number"
typeof 10n // "bigint"
typeof true // "boolean"
typeof "foo" // "string"
typeof Symbol("id") // "symbol"
typeof Math // "object"  

-->
