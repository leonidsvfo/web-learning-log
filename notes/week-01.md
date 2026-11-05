# Web Developer Studies

*Study notes: the Internet, HTML, CSS and JavaScript foundations*


---

# Chapter I – The Internet

## How the Internet works

The Internet is a vast network of computers that communicate with one another. To communicate, two computers need to be connected either physically or wirelessly.

Connecting a large number of computers together can be difficult because it requires too many cables. To solve this problem, each computer can be connected to a small network switch. This switch has only one job: it forwards messages to their intended destination. To distinguish between computers, the switch uses MAC addresses, much like a courier delivering a package to the right address. In this case, every Wi-Fi or Ethernet interface has its own MAC address. Switches can also be interconnected, allowing the network to grow much larger. But if you connected ten billion computers to this network, each switch would need to remember up to ten billion MAC addresses.

When an address has been deleted due to inactivity or another malfunction, switches must broadcast the message to all computers on the local network. As the network grows, it becomes increasingly costly to keep track of individual devices and find unknown recipients. The key problem is that our addresses have no hierarchy and no structure—they are just raw addresses. And that's when routers step in.

We divide computers into separate local networks and connect these networks using a device called a router. It uses a different kind of address, an IP address, which is a 4-number sequence like 142.250.190.78. Unlike MAC addresses, which are "fingerprints", IP addresses are "street addresses" and are assigned when a computer connects to a network, identified in the IP address by a shared prefix. A router can therefore store forwarding instructions for a whole group of addresses (e.g., "forward to this router whenever the IP address starts with 142.250") without learning the location of every individual computer in that group. IP and MAC addresses work together for better long-distance and local connectivity. Such a network comes very close to what we call the Internet.

We just need the physical medium (cables) to connect all these routers.

Luckily, such an infrastructure already existed prior to the Internet: the telephone network. To connect our network to the telephone infrastructure, we need a special piece of equipment called a modem. This modem turns the information from our network into information manageable by the telephone infrastructure and vice versa.

The next step is to send the messages from our network to the network we want to reach. To do that, we connect our network to an Internet Service Provider (ISP). An ISP is a company that manages routers, all linked together around the world with fiber-optic cables. The Internet consists of this whole infrastructure of networks.

## Domain names (DNS)

DNS names are aliases for IP addresses, such as google.com for 142.250.190.78.

## Internet and the web

The difference between the web and the internet is that while the internet is an infrastructure, the web is a service built on top of it, where some computers (web servers) can send messages intelligible to web browsers.

## Intranets and Extranets

Intranets are private networks that are restricted to members of a particular organization, used to provide a portal to securely access shared resources, collaborate and communicate. Extranets are very similar to Intranets, except they open all or part of a private network to allow sharing and collaboration with other organizations.

## Web page

A document that can be displayed in a web browser, often called "pages".

It can provide:

- **Style information** – the look;
- **Scripts** – the interactivity of the page;
- **Media** – images, video, sounds.

A web page has its unique URL, or web address, to access the page. A URL is basically HTTP + DNS + path.

## Web site

A collection of web pages grouped all together into a single unit, a "site". This collection of web pages shares the same domain name (DNS).

## Web server

A computer that hosts a website on the internet. All the web pages and their associated files are on the server; it can host multiple websites and share them between many computers at the same time.

## Web service

Software that responds to requests over the Internet to provide data.

## Search engine

A web service that helps you find other websites, pages, or other information.

## Clients and servers

Computers connected to the internet act as clients and servers.

Clients are typical internet users' devices, such as PCs or smartphones, that use software (like a browser) for data exchange. Servers are computers that store data and host services (or applications) to share information with clients.

Data exchange is possible when the following are in place:

1. **Internet connection:** The physical link required to transmit data.
2. **TCP/IP:** Transmission Control Protocol and Internet Protocol. These communication protocols define how data should be transmitted.
3. **DNS:** Domain Name System. The browser finds the IP address of the site by "translating" the domain name so it understands which IP address to send HTTP messages to.
4. **HTTP:** Hypertext Transfer Protocol. An application protocol that defines a language between clients and servers to communicate with each other.

Website files usually consist of:

- **Code:** HTML, CSS, and JavaScript.
- **Assets:** Documents, images, videos, etc.

## So how does the web work?

1. You type a web address in your browser (DNS). The browser, through DNS, finds the IP of the server where the website works and sends an HTTP request message to ask for a copy of the site to be sent to the client. This exchange works using TCP/IP. Such requests are made using a technology called HTTP (Hypertext Transfer Protocol), which uses a language of verbs (GET) to describe what should happen.
2. If the server approves the client's request, it sends a "200 OK" message with all the data and files, which are divided into small chunks called packets. Typically, there is more than one request, occurring one after another.
3. The browser assembles all the chunks and shows the site to you. When all of the resources have been requested, the web browser parses and renders them as required before displaying the result to the user.

### Packets

**Packets** are small parts of data that contain:

- **Header:** IP address of the client and the server, total number of packets, protocol.
- **Payload:** The actual requested data.

### HTTP

**HTTP** (Hypertext Transfer Protocol) is a simple language used to send requests; typically we use GET:

**Request:**

```http
GET /en-US/ HTTP/2
Host: developer.mozilla.org
```

**Response:**

```http
HTTP/2 200
date: Tue, 11 Feb 2025 11:13:30 GMT
expires: Tue, 11 Feb 2025 11:40:01 GMT
server: Google frontend
last-modified: Tue, 11 Feb 2025 00:49:32 GMT
ETag: "65f26b7f6463e2347f4e5a7a2adcee54"
content-length: 45227
content-type: text/html

<!doctype html> ... (the 45227 bytes of the requested web page HTML)
```

- `HTTP/2 200`: version of HTTP and status code;
- `date`, `expires`, etc.: HTTP headers, extra information;
- `<!doctype html>`: the body, which contains the web page.

### Status codes

Status codes are used to understand the server's responses:

- `200`: OK.
- `301`: The content has been moved.
- `400`: The server can't process the request; there could be errors.
- `403`: The server doesn't give the user permission to enter.
- `503`: Maintenance.

---

# Chapter II – The Work Environment and HTML Foundations

## Operating system (OS)

An **operating system (OS)** is **the core system software that manages a computer's hardware and software resources**, acting as an essential bridge between the user, applications, and physical device components. Most web servers run on a Linux environment, in particular the Ubuntu distro (Linux distribution). It is recommended to use the Ubuntu environment for web development. If you are using another OS, you should be aware that some of the instructions in this guide could be different.

## Text editor

A text editor is used to write text. For coding there are multiple recommended text editors, like Visual Studio Code. It includes many tools to write better and cleaner code. For this guide we are using VSCode.

## Command line (or Command Line Interface / CLI)

Humans and computers commonly interact through screen interfaces, better called **graphical user interfaces (GUI)**. With a GUI, we give instructions by clicking a mouse and using menu-driven interaction. While it is simpler and more intuitive to learn, this way scales very poorly for bigger tasks.

A **command line** is a text-based screen where you type text commands to tell your computer's operating system what to do, instead of clicking with a mouse. A shell is a particular program that lets you type commands:

- `ls`: Lists all files and folders in your current directory.
- `cd [folder]`: Changes your current directory (moves into a folder).
- `cd ..`: Moves up from the current directory.
- `pwd`: Shows the path of the directory you are currently in.
- `mkdir [name]`: Creates a new folder.
- `rm [file]`: Deletes a file.
- `cp [source] [dest]`: Copies a file or folder from one place to another.
- `mv [source] [dest]`: Moves or renames a file or folder.
- `cat [file]`: Displays the text content of a file on the screen.

## Version control system

Version control is a system that keeps track of every change to your files. It allows you to revert selected or all files back to a previous state, and vice versa. There are three types:

- **Local version control system:** Your PC with every snapshot of every version of the project. If your PC goes down, the project is lost.
- **Centralized version control system:** A number of computers connected to a single server that contains all the snapshot versions. If the server goes down, goodbye project.
- **Distributed version control system:** Every computer involved in the project shares information and has a copy with all the versions and files.

## Git

Git is the most used version control system; it contains all of your saved text files and different versions of your saves, keeping a historical record of each save. Then you can use your saved projects and publish them online on GitHub to share and collaborate with other developers. So GitHub essentially becomes your personal portfolio.

## HTML foundations

Hypertext Markup Language defines the structure and content of webpages: paragraphs, headings, lists, images, links.

### Creating the HTML file

First of all we need to create the directory of your project to work with.

Make a new folder with the name of your project; within that folder, create a new file and name it **index.html** (web servers by default look for an index.html for the homepage).

Open your text editor (VSCode is recommended), and start from the first line.

### Boilerplate

Every HTML document starts with the boilerplate, the same basic structure that needs to be in place before anything useful can be done.

#### `<!DOCTYPE html>`

A new webpage starts with a doctype declaration, an instruction for the browser that declares which version of HTML it should use to render the document: `<!DOCTYPE html>`. Its purpose is mostly to prevent the browser from switching into "quirks mode", an old rendering mode kept for backward compatibility with older pages: your site would probably still work without this instruction, but it might be displayed inconsistently. It does not have a closing tag.

#### `<html>`

Right below the `<!DOCTYPE html>` instruction we should write `<html lang="en">` with the closing tag `</html>`; everything else about our site goes into this element. This element represents the HTML document that the browser is going to read and show to the clients. The `lang="en"` attribute that we put inside `<html>` represents the language chosen for the page.

#### `<head>`

In the `<html>` element we should include a `<head>` element. The head element is where we put all of the meta information about our website, required to render correctly in the browser, that is not visible in our web page.

#### `<meta>` – Metadata

Metadata is data (information) about data. In the `<head>` element we put `<meta>` tags that are typically used to specify the character set, page description, keywords, author of the document and viewport settings. One of the most important pieces of data that we are going to write is the charset attribute: ***`<meta charset="UTF-8">`***. This is needed to process special symbols and characters from different languages correctly.

There are many important pieces of metadata that you will be adding to your website, one of them is `<meta name>`, where you need to specify the **content** of that data. For example:

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="A short description of the page" />
</head>
```

- **viewport:** tells the browser how to show your page on a mobile device;
- **description:** the text that is shown below your title on a web search engine, like Google;
- **author:** the author of the page;
- **favicon:** a small image displayed next to the page title in the browser tab (it is added with a `<link rel="icon">` element rather than a `<meta>` tag).

Another `<meta>` example: if we want to add a preview of our website on another website, we could use the Open Graph protocol:

```html
<meta property="og:title" content="The Rock" />
<meta property="og:type" content="video.movie" />
<meta property="og:url" content="https://www.imdb.com/title/tt0117500/" />
<meta property="og:image" content="https://ia.media-imdb.com/images/rock.jpg" />
```

#### `<title>` – Browser tab title

In the head element we should add the `<title>My First site</title>` element, used to give the webpages a human-readable title which is displayed in our browser tab.

#### `<body>`

The final element to complete our boilerplate is the `<body>`; it is where all the content that will be displayed to users goes – text, images, lists, links, etc. This element goes in the `<html>` element (**NOT** in the `<head>` element).

The final boilerplate could look like this:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="title" content="My page">
    <meta name="description" content="My first website!">
    <meta name="author" content="Leonid Svetlov">
    <title>Recipes</title>
  </head>

  <body>
  </body>
</html>
```

It is good practice to maintain consistent indentation between nested elements.

### Elements / tags

An HTML element is defined by a start tag, some content, and an end tag.

The HTML element is everything from the start tag to the end tag:

```html
<tagname>Content goes here...</tagname>
```

Most content on the web is text-based, so you will find yourself needing to work with HTML text elements quite a bit. We have different types of elements that can customize your text, like:

- `<p>` paragraphs;
- `<h1>` to `<h6>` headings (from the biggest to the smallest);
- `<strong>` bold element;
- `<br>` breaks the text onto a new line;
- `<em>` italic; etc.

### Boxes

In modern web development, web pages are conceptually built using a system of nested **boxes or containers** like `<div>` and `<span>`. These containers structure and organize all visual elements on the page, from text and images to videos and interactive components.

### Semantic tags

Semantic tags describe the *meaning* of the content they wrap, not just how it looks. Browsers, search engines, and screen readers use them to understand the structure of a page. An HTML document becomes more readable using semantic tags.

The main ones are:

1. `<header>`: introductory content or navigation links at the top of a page or section;
2. `<nav>`: a block of navigation links;
3. `<main>`: the main content of the page (only one per page);
4. `<section>`: a thematic group of content, usually with a heading;
5. `<article>`: a self-contained piece of content that makes sense on its own, like a blog post;
6. `<aside>`: side content related to the main content, like a sidebar;
7. `<footer>`: closing content at the bottom of a page or section, like copyright info or links;
8. `<figure>`: illustration, diagram, photo, blockquote.

### Lists

To write a list of content we have these options:

**Unordered lists** (`<ul>`):

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

**Ordered lists** (`<ol>`):

```html
<ol>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ol>
```

### Attributes

An attribute gives additional information to an HTML element and always goes in the opening tag. An attribute is usually made up of two parts: a name and a value. Not all attributes require a value.

#### Links

To create a link we use an anchor element `<a>`. For a link we need to add the `href` (hypertext reference) attribute to the opening anchor tag. The value of the href attribute is the destination we want our link to go to:

```html
<a href="https://www.theodinproject.com/about">About The Odin Project</a>
```

This method opens the link directly in your current tab. If you want it to be opened in a new tab, you will need to add the `target` attribute. By default your link is set to the `_self` value, which is your current tab; you need to change it to `_blank`:

```html
<a href="https://www.theodinproject.com/about" target="_blank" rel="noreferrer">About The Odin Project</a>
```

The `rel` attribute is used to describe the relation between the current page and the link, and can be set to:

- `noopener`: prevents the new tab from accessing the original page, which would have opened the possibility of phishing attacks like tabnabbing;
- `noreferrer`: same as `noopener` but more secure.

#### Absolute links and relative links

Absolute links are completely other sites that we want to put in our page; relative links are pages of our website. An absolute link includes `scheme://dns/path`; a relative link includes only the path, because it is already in our website, like this:

```html
<a href="./pages/about.html">About</a>
```

#### Images and their attributes

##### `src`

Images are void elements that do not include a closing tag. They use the `src` attribute, which tells the browser where the image file is located (like the `href` attribute). It can embed an image using both absolute and relative paths:

```html
<img src="https://theodinproject.com/mstile-310x310.png">
```

##### `alt`

The alt attribute (`alt="title-of-my-image"`) in the image element is used to describe the image on the webpage, only for screen readers, SEO, or as a fallback. It will be used in place of the image if it cannot be loaded:

```html
<img src="https://theodinproject.com/mstile-310x310.png" alt="The Odin Project logo">
```

##### Height and width

It's a good habit to always specify the size of an image, even if you customize it in CSS, to prevent visual errors:

```html
<img src="./images/theodinlogo.png" alt="the-odin-logo" height="310" width="210">
```

##### `srcset` and `sizes`

A web page could be opened by many different devices, on different browsers. Sometimes, when you have a high-quality image, it could have responsive troubles rendering the image on older devices. For that we use the `srcset` and `sizes` attributes to get the right size and quality for the device.

It is also a good habit to use the `<figure>` tag as a container of the image, and `<figcaption>` for its description.

### The structure of a website

In a work environment or in group (or solo) projects, the files of a website usually look like this from your MAIN folder:

```text
MyStudySite/
│
├── public/                 # Static assets visible to the browser
│   ├── assets/
│   │   ├── images/         # All media files (img/png, svg, etc.)
│   │   ├── css/            # Stylesheets (style.css, responsive.css)
│   │   └── js/             # Scripts (main.js, utils.js)
│   │
│   ├── index.html          # Home page
│   ├── about.html          # About page
│   ├── contact.html        # Contact page
│   └── sitemap.xml         # SEO file
│
├── pages/                  # Source code for dynamic rendering (if using a
│   │                       # framework) or logical grouping
│   ├── layout/             # Reusable header/footer components
│   └── content/            # Text-heavy pages
│
├── data/                   # Raw data files for analysis
│   └── sample_data.csv     # Example dataset
│
├── docs/                   # Documentation
│   ├── README.md           # Project overview
│   └── guide.md            # Study notes
│
└── config.json             # Configuration settings
```

---

# Chapter III – CSS

If HTML is the structure, CSS is the style that makes our web page look good. ***Cascading Style Sheets*** is a style sheet language used for specifying the presentation and styling of a document written in a markup language.

First of all we need to add a CSS file to our structure. There are three ways to add CSS to HTML: external CSS, internal CSS and inline CSS.

## Ways to add CSS

### External CSS

External CSS is the most common method you will come across; it involves creating a separate file for CSS (`styles.css`, for example) and linking it inside the HTML:

```html
<head>
  <link rel="stylesheet" href="styles.css">
</head>
```

First we add the void `link` element, then we add the `rel` attribute, which specifies the relationship between the HTML file and the linked file, and the `href` attribute, which includes the path to find the file.

### Internal CSS

Internal CSS involves adding the style within the HTML file, placing the rules in `<style>` opening and closing tags, which go inside the `<head>` element.

```html
<head>
  <style>
    p { color: red; }
  </style>
</head>
```

### Inline CSS

Inline CSS makes it possible to add styles directly to HTML elements, through the `style` attribute:

```html
<p style="color: green;">Some text</p>
```

## Basic syntax

CSS is made up of various rules; each rule is made up of a selector and a semicolon-separated list of declarations, with each of those declarations being made up of a property-value pair.

```css
div.bold-text {
  font-weight: 700;
}
```

In this rule, `div.bold-text` is the **selector**, `font-weight` is the **property** and `700` is the **value**.

## Selectors

Selectors refer to the HTML elements to which a rule applies; they're what is actually being selected for each rule. The most common are:

- **universal selector:** `*` selects every HTML element;
- **type selector:** `p { color: white; }` (every `p` element is selected);
- **class selector:** if you give an element a `class` attribute, you can choose that particular class to be selected (`class="red"`) → `.red { color: red; }`. Another thing you can do with the class attribute is to add multiple classes to a single element as a space-separated list, such as `class="red blue green"`;
- **ID selector:** the same as the class selector, with the only difference that an element can only have one ID, and it cannot be repeated like the class selector (which you can use on multiple elements). `<div id="blue">Awesome</div>` → `#blue { background-color: blue; }`;
- **grouping selector:** when multiple selectors share the same style declarations, you can just put them one after the other, divided by a comma: `.red, .blue { color: white; }`;
- **chaining selector:** if we have for example two elements with similar classes "this blue" and "this red", you can chain both class selectors together like this: `.this.blue { color: blue; }`.

Or, for example:

```html
<div>
  <div class="right now">Latest Posts</div>
  <p class="right" id="not">
    This is where a preview for a post might go.
  </p>
</div>
```

```css
/* selects only the first div: it is the only one with both classes */
.right.now { color: blue; }
```

### Shorthand properties

Shorthand properties let you set the values of multiple other properties simultaneously; this way you can write more concise stylesheets, making code clearer and saving time.

```css
background-color: black;
background-image: url("images/bg.gif");
background-repeat: no-repeat;
background-position: left top;
```

These four declarations can be shortened to just one:

```css
background: black url("images/bg.gif") no-repeat left top;
```

### Descendant combinator

To select nested descendants based on their ancestors, use the descendant combinator, which is represented in CSS by a single space between selectors.

```html
<div class="ancestor">     <!-- A -->
  <div class="contents">   <!-- B -->
    <div class="contents"> <!-- C -->
    </div>
  </div>
</div>

<div class="contents"></div> <!-- D -->
```

```css
.ancestor .contents {
  /* some declarations */
}
```

In the above example, the first two elements with the `contents` class (B and C) would be selected, but the last element (D) wouldn't be.

## CSS properties

The `color` property sets an element's text color, while `background-color` sets, well, the background color of an element. Both of these properties can accept one of several kinds of values: HEX, RGB, HSL and keywords (like "red"). Other common properties are `font-family` (if the font family has spaces between words you need to use quotes like ' or "), `font-size`, `font-weight` (boldness), `text-align`, `height` and `width`.

## The cascade of CSS

The cascade is what determines which rules actually get applied to our HTML. There are different rules that define what comes first.

### Specificity

We have different kinds of specificity that could be on declarations or types of styles. The most specific style is inline, which has the highest specificity compared to selectors, while each type of selector has its own specificity level. A CSS declaration that is more specific will take precedence over less specific ones:

1. ID selectors (the most specific selector);
2. Class selectors;
3. Type selectors.

Specificity will only be taken into account when an element has multiple conflicting declarations targeting it. If comparing specificity doesn't determine a winner, compare the number of selectors in the same category: the rule with more selectors takes precedence.

### Inheritance

Inheritance refers to certain CSS properties that, when applied to an element, are inherited by that element's descendants, even if we don't explicitly write a rule for those descendants. Typography-based properties (`color`, `font-size`, `font-family`, etc.) are usually inherited, while most other properties aren't.

```html
<div id="parent">
  <div class="child"></div>
</div>
```

```css
#parent {
  color: red;
}

.child {
  color: blue;
}
```

Despite the parent element having a higher specificity with an ID, the child element would have the `color: blue` style applied since that declaration directly targets it, while `color: red` from the parent is only inherited.

If, after every other factor has been taken into account, there are still multiple conflicting rules targeting an element, whichever rule was the *last* defined is the winner.

There is also a hierarchy between the web server, the user and the browser, which comes in this order.

## HTML vs DOM

When you use a web browser to request a page, the server returns an HTML document, but the browser parses it and creates a tree of objects. The **Document Object Model (DOM)** is a **programming interface** provided by the browser that represents an HTML (or XML) document as a **tree of objects**.

In simple terms:

- Your HTML file is just text;
- The browser parses this text;
- The browser converts it into a structured object tree;
- That tree is the DOM.

JavaScript does **not** manipulate HTML text directly. Instead, it manipulates the DOM. The DOM is a **live, in-memory representation** of a document that allows programs to read, modify, add, and delete content, structure, and styles.

## The box model

Every single thing on a website is a rectangular box. These boxes can have other boxes inside of them. There are many ways to manipulate the size of these boxes, and the space between them, using padding, border and margin.

- **content box:** the area where your content is displayed; size it using properties like `width` and `height`;
- **padding:** increases the space between the border of a box and the content of the box. Unlike margins, you cannot have a negative padding.

### Border

Borders add space between the margin and the padding. If you are using the standard box model, the size of the border is added to the **width** and **height** of the content box. If you are using the alternative box model, then the bigger the border is, the smaller the content box is, as the border takes up some of that available **width** and **height** of the element box. For styling borders, there are a large number of properties—there are four borders, and each border has a style, width, and color that we might want to manipulate.

To set the properties of each side individually, use:

- `border-top`
- `border-right`
- `border-bottom`
- `border-left`

To set the **width**, **style**, or **color** of all sides, use: `border-width`, `border-style`, `border-color`. To set the width, style, or color of a single side, use one of the more granular longhand properties like `border-top-width`, `border-left-style` and so on.

### Margin

Margin is an invisible space; it increases the space between the borders of a box and the borders of adjacent boxes. Margins can have negative and positive values. Depending on whether two elements whose margins touch have positive or negative margins, the results will be different:

- Two positive margins will combine to become one margin. Its size will be equal to the largest individual margin.
- Two negative margins will collapse and the smallest (furthest from zero) value will be used.
- If one margin is negative, its value will be **subtracted** from the total.

### Element properties

Every element comes with three important factors:

- **Sizing:** `box-sizing`;
- **Layout behavior:** `display` (block, inline, flex, grid, none);
- **Other layout tools:** `float`, `position`.

### Box-sizing

In the standard box model, the property `box-sizing: content-box`, if you set `width` and `height` property values on a box, these values define the `width` and `height` of the **content box**. Any padding and borders are then added to those dimensions to get the total size taken up by the box.

```css
.box {
  width: 350px;
  height: 150px;
  margin: 10px;
  padding: 25px;
  border: 5px solid black;
}
```

The **actual** space taken up by the box will be **410px** wide (350 + 25 + 25 + 5 + 5) and **210px** high (150 + 25 + 25 + 5 + 5).

#### `box-sizing: border-box`

In the alternative box model, any width is the width of the visible box on the page. The content area width is that width minus the width for the padding and border. This is convenient as there is no need to add up the border and padding to get the real size of the box. To turn on the alternative model for an element, set `box-sizing: border-box` on it:

```css
.box {
  box-sizing: border-box;
  width: 350px;
  height: 150px;
  margin: 10px;
  padding: 25px;
  border: 5px solid black;
}
```

## Display

Elements on a webpage lay out in normal flow if you haven't applied any CSS to change the way they behave between each other. For example, elements like `<img>` and `<button>` are by default displayed as `inline-block`. The `display` property defines the relationships between multiple boxes in different ways.

**`display: block`**

Displays an element as a block element (like `<p>`). It starts on a new line, and takes up the whole width.

**`display: inline`**

- Respects left & right margins and padding, but **not** top & bottom.
- Cannot have a width and height set.
- Allows other elements to sit to their left and right.

**`display: inline-block`**

- Allows other elements to sit to their left and right.
- Respects top & bottom margins and padding.
- Respects height and width.

Use it if you do not want an item to break onto a new line, but do want it to respect `width` and `height` and avoid the overlapping seen above.

When building a web page, not every piece of content has a specific semantic tag. Sometimes, you just need a container you can style or position. That's where `<div>` (block element) and `<span>` come in.

### Particular elements

For elements, the default behavior is `box-sizing: content-box`, but there are some particular ones that have a different default `display` value:

- `<img>` is **inline-block**
- `<button>` is **inline-block**
- `<span>` is **inline**
- `<textarea>` is **inline**
- `<input>` is **inline**
- `<select>` is **inline-block**

### Inner and outer display types

**Block** and **inline** display values are said to be **outer display** types—they affect how the box is laid out in relation to other boxes around it. Boxes also have an **inner display** type, which dictates how elements inside that box are laid out.

You can change the inner display type by setting an inner display value, for example `display: flex;`. The element will still use the outer display type **block**, but this changes the inner display type to **flex**. Any direct children of this box will become flex items and behave according to the **Flexbox** specification.
