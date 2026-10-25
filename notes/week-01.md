CAPTER I

The internet
The Internet is a vast network of computers that communicate with one another. To communicate, two computers need to be connected either physically or wirelessly.
Connecting a large number of computers together can be difficult because it requires too many cables. To solve this problem, each computer can be connected to a 
small network switch. This switch has only one job: it forwards messages to their intended destination. To distinguish between computers, the switch uses MAC addresses, 
much like a courier delivering a package to the right address. In this case, every Wi-Fi or Ethernet interface has its own MAC address. Switches can also be 
interconnected, allowing the network to grow much larger. But if you connected ten billion computers to this network, each switch would need to remember up to ten 
billion MAC addresses.

When an address has been deleted due to inactivity or another malfunction, switches must broadcast the message to all computers on the local network. As the network 
grows, it becomes increasingly costly to keep track of individual devices and find unknown recipients. The key problem is that our addresses have no hierarchy and 
no structure—they are just raw addresses. And that’s when routers steps on.

We divide computers into separate local networks and connect these networks using a device called a router. It uses a different kind of address, an IP address, 
which is a 4-number sequence like 142.250.190.78. Unlike MAC addresses, which are "fingerprints", IP addresses are "street addresses" and are assigned when a 
computer connects to a network, identified in the IP address by a shared prefix. A router can therefore store forwarding instructions for a whole group of addresses
(e.g., "forward to this router whenever the IP address starts with 142.250") without learning the location of every individual computer in that group. IP and MAC 
addresses work together for better long-distance and local connectivity. Such a network comes very close to what we call the Internet.

We just need the physical medium (cables) to connect all these routers. 
Luckily, such an infrastructure already existed prior to the Internet: the telephone network. To connect our network to the telephone infrastructure, we need a 
special piece of equipment called a modem. This modem turns the information from our network into information manageable by the telephone infrastructure and vice versa. 
The next step is to send the messages from our network to the network we want to reach. To do that, we connect our network to an Internet Service Provider (ISP). 
An ISP is a company that manages routers, all linked together around the world with fiber-optic cables. The Internet consists of this whole infrastructure of networks.

Domain names (DNS)
DNS are alias for IP addresses, such as google.com for 142.250.190.78
Internet and the web
The difference between the web and the internet is that while the internet is an infrastructure, the web is a service build on top, where some computer (web servers) 
can sand messages intelligible to web browsers.

Intranets and Extranets
Intranets are private network that are restricted to members of a particular organization, used to provide a portal to securely access shared resources, collaborate 
and communicate. Extranets are very similar to Intranets, except they open all or part of a private network to allow sharing and collaboration with other organizations.
Web page
A document that can be displayed in a web browser, often called “pages”.
Can provide:
Style information – the look;
Scripts – interactivity of the page;
Media – images, video, sounds.

The web page have his unique URL, or web address, to access the page. URL is basically HTTP + DNS + path.

Web site
A collection of web pages grouped all together into a single unit, “site”. This collections of web pages shares the same domain name DNS.

Web server
A computer that host a website on the internet. All the web pages and their associated files are on the server, it can host multiple websites and share between many
computers at the same time.

Web service
Software that responds to requests over the Internet to provide data. 
Search engine
A web service that helps you find other websites, pages, or other information.

Clients and servers

Computers connected to the internet act as clients and servers.
Clients are typical internet users' devices, such as PCs or smartphones, that use software (like a browser) for data exchange. Servers are computers that store 
data and host services (or applications) to share information with clients
Data exchange is possible when the following are in place:
1) Internet connection: The physical link required to transmit data.
2) TCP/IP: Transmission Control Protocol and Internet Protocol. These communication protocols define how data should be transmitted.
3) DNS: Domain Name System. The browser finds the IP address of the site by "translating" the domain name so it understands which IP address to send HTTP messages to.
4) HTTP: Hypertext Transfer Protocol. An application protocol that defines a language between clients and servers to communicate with each other.
 Website files usually consist of:
 - Code: HTML, CSS, and JavaScript.
 - Assets: Documents, images, videos, etc. 

So how does the web work?
1) You type a web address in your browser (DNS). The browser, through DNS, finds the IP of the server where the website works and sends an HTTP request message
2) to send a copy of the site to the client. This exchange works using TCP/IP. Such requests are made using a technology called HTTP (Hypertext Transfer Protocol),
3) which uses a language of verbs (GET) to describe what should happen.
4) If the server approves the client's request, it sends a "200 OK" message with all the data and files that are divided in small chunks called packets.
5) Typically, there is more than one request, occurring one after another.
6) The browser assembles all the chunks and shows the site to you. When all of the resources have been requested, the web browser parses and renders them as
7) required before displaying the result to the user. 

Packets are small parts of data that contain:
- Header: IP address of the client and the server, total number of packets, protocol.
- Payload: The actual requested data. 

HTTP (Hypertext Transfer Protocol) is a simple language used to send requests,; typically we use GET:

Request:
GET /en-US/ HTTP/2
Host: developer.mozilla.org

Response:
HTTP/2 200
date: Tue, 11 Feb 2025 11:13:30 GMT
expires: Tue, 11 Feb 2025 11:40:01 GMT
server: Google frontend
last-modified: Tue, 11 Feb 2025 00:49:32 GMT
ETag: "65f26b7f6463e2347f4e5a7a2adcee54"
content-length: 45227
content-type: text/html
<!doctype html> ... (the 45227 bytes of the requested web page HTML)
-----------------------------------------------------------------
- HTTP/2 200: version of http and status code;
- Data, expires, etc: https headers , extra information;
- <!doctype html> : body which contains the web page.


Status code are used to understand servers responses:
- 200: OK
- 301: The content has been moved.
- 400: Server can't process; could be errors.
- 403: Server doesn't give user permission to enter.
- 503: Maintenance.

CHAPTER II
The Work Environment

Text Editor
A text editor is used to write code. The best editor is Visual Studio Code; it is free and is a performant tool for web developers.

Command Line (or Command Line Interface / CLI)
What is a shell?
Humans and computers commonly interact through screen interfaces, better called graphical user interface GUI. With a GUI, we give instructions by 
clicking a mouse and using menu-driven interaction. While is more simple and intuitive to learn, this way scales very poorly for bigger tasks. 
A command line is a text-based screen where you type text commands to tell your computer's operating system what to do, instead of clicking with a mouse. 
A shell is a particular program that lets you type commands, 

- ls: Lists all files and folders in your current directory.
- cd [folder]: Changes your current directory (moves into a folder).
- cd .. : move up from current directory.
- pwd: Shows the path of the directory you are currently in.
- mkdir [name]: Creates a new folder.
- rm [file]: Deletes a file.
- cp [source] [dest]: Copies a file or folder from one place to another.
- mv [source] [dest]: Moves or renames a file or folder.
- cat [file]: Displays the text content of a file on the screen.


GIT
Git is a version control system; it contains all of your saved text files and different versions of your saves, keeping a historical record of each save. 
Then you can use your saved projects, publish them online on GitHub to share and collaborate with other developers. So GitHub essentially becomes your personal portfolio.

Version Control
Version control is a system that keeps track of every change to your files. It allows you to revert selected or all files back to a previous state, 
and vice versa. There are three types:
- Local version control system: Your PC with every snapshot of every version of the project. If your PC goes down, the project is lost.
- Centralized Version Control system: A number of computers connected to a single server that contains all the snapshot versions. If the server goes down,
- goodbye project.
- Distributed Version Control System: Every computer involved in the project shares information and has a copy with all the versions and files.

HTML
Hypertext Markup Language defines the structure and content of webpages: paragraphs, headings, lists, images, links. Elements are pieces of content wrapped 
in opening and closing HTML tags.
Tags define the content of the webpage; they are represented by angle brackets < >, where between them you'll find a keyword that says which type of 
content is inside this element.
For example:
<p> Hello, world!</p>

- <p> stands for opening tag and means "paragraph".
- "Hello, world!" Is the content wrapped within the opening and closing tags.
- </p> is the closing tag.

Some elements do not have a closing tag, they are called ‘’Void Elements’’, they have a single tag like <br> or <img>.


Creating the first HTML file

First of all we need to create an HTML file to work with:
- one folder, within that folder create a new file and name it index.html (web servers by default look for an index.html for the homepage;

Boilerplate
The boilerplate of an HTML document is the same basic structure that needs to be in place before anything useful can be done.
Our coding experience begins with a doctype declaration, the doctype tell the browser what version of HTML it should use to render the document: 
<!DOCTYPE html>.
Now we need to create our html element <html lang=”en”>      and closing    </html>, everything else about our site goes into this element.
Let’s add <head> element (opening and closing), is where we put all of the meta information about our website required to render correctly 
in the browser *it is not visible in our web page.
In the <head> element we put <meta charset=”UTF-8”> this is needed to process special symbols and characters from different languages correctly.
Shortly after we put the <title>My First site</title> element, used to give the webpages a human-readble title wich is displayed in our browser tab.
The final element to complete our boilerplate is the <body>, is where all the content that will be displayed to users will go – text, images, 
lists, links, ecc.

Text
Most content on web is text-based, so you will find yourself needing to work with HTML text elements quite a bit.
Every text you like to show on the web site needs to be put in the <body element>. We have different types of elements that can customize your text:

- <p> paragraphs
- <h1> to <h6> (from the biggest to the smallest) headings
- <strong> bold element
- <em> italic (corsivo)

If you need to leave a comment in your html file that does influence your code, you need to write it like this : <!-- this is a comment -->

Lists
To write a list of content we have this options:
- unordered lists 
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
- ordered lists
<ol>   
<li>Item 1</li>   
<li>Item 2</li>   
<li>Item 3</li> 
</ol>
Links
To create a link we use an anchor element <a>. Attribute gives additional information to an HTML element and always goes in the opening tag. An 
  attribute is usually made up of two parts: a name and a value. But not all attributes require a value. For a link we need to add href 
  (hypertext reference) attribute to the opening anchor tag. The value of the href attribute is the destination we want our link to go: 
  <a href=”https://www.theodingproject.com/about”>About The Odin Project</a>
This method opens the link directly in your open tab, if you want to be opened in a new tab, you will need to add the target element. By 
  default your link is set on _self value, which is your current tab, you need to change it to _blank: 
<a href=”https//www.theodinproject.com/about” target=”_blank” rel=”noreferrer”>About The Odin Project</a>
The “rel” attribute is used to describe the relation between the current page and the link, and can be set on:
- noopener: Prevents new tab from accessing the original page, which would have opened the possibility of phishing attack like tabnabbing;
- noreferrer: same as nooperner but more secure.
Absolute links and relative links
Absolute links are completely other sites that we want to put in our page, relative links are pages of our web site. An absolute link includes 
  scheme://dns/path a relative link include only the path because is already in our website, like this <a> href="./pages/about.html">About</a>.
Images
Images are void elements that not include a closing tab, they use “src” element which tells the browser where the image file is located 
(like the href attribute). It can embed an image using both absolute and relative paths: <img src=”https://theodinproject.com/mstile-310x310.png”>.
Alt attribute in the image element is used to describe the image on the webpage. It will be used in place of the image if it cannot be loaded. 
It is also used with screen readers to describe what the image is to visually impaired users: <img src=”https://theodinproject.com/mstile-310x310.png
alt=”The odin project logo”>.
It’s a good habit to always specify the size of an image, even if you customize it in CSS, for preventing visual errors 
  <img src=”./images/theodinlogo” alt=”the-odin-logo” height=”310” width=”210”>



The structure of a web site
The files of a web site need to have a structure like this:
MyStudySite/
│
├── /public                 # Static assets visible to the browser
│   ├── /assets
│   │   ├── /images         # All media files (img/png, svg, etc.)
│   │   ├── /css            # Stylesheets (style.css, responsive.css)
│   │   └── /js             # Scripts (main.js, utils.js)
│   │
│   ├── index.html          # Home page
│   ├── about.html          # About page
│   ├── contact.html        # Contact page
│   └── sitemap.xml         # SEO file
│
├── /pages                  # Source code for dynamic rendering (if using a framework) or logical grouping
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




CAPTER III
CSS
If HTML is the structure CSS is the style to make look good our web page. Cascading Style Sheets is a style sheet language used for specifying 
the presentation and styling of a document written in a markup language. First of all we need to add a CSS file to our structure. There are three 
ways to add CSS to HTML: External CSS, Internal CSS, inline CSS.
External CSS
External is the most common method you will come across, it involves creating a separate file for CSS (styles.css for example) and linking it inside 
the HTML:
<head>
 <link rel=”stylesheet” href=”styles.css”>
<head>
First we add void “link” element than we add “rel” attribute which specifies the relationship between the HTML file and the linked file, and “href’ 
  attribute that include the path to find the file.
Internal CSS
Internal CSS involves adding the style within the HTML file, placing the rules in <style> opening and closing tags, that are going inside oh the <head> 
  element.
<head>
      <style>
      p{ color: red;}
     </style>
<head>
Inline CSS
Inline CSS makes possible to add styles directly to HTML elements:   p{color:green;}

Basic syntax
CSS is made up of various rules, each rule is made up of a selector and a semicolon-separated list of declarations, with each of those declarations 
being made up of property-value pair.
Selectors
Selectors refer to the HTML elements to which rule apply; they’re what is actually being selected for each rule. The most common are:
-   *  select every HTML elements;
- type selector: p { color: white; } (every p element is selected);
- class selector: if you put a “class” attribute to a element, you can chose that particular class to be selected (class=”red”)   -----> .red { color: red; }.
  Another thing you can do with the class attribute is to add multiple classes to a single element as a space-separated list, such as class="red blu green";
- ID selector: is the same as class selector with only difference that an element can only have one ID, it cannot be repeated like the class selector
  (that you can use on multiple elements). <div id=”blue”>Awesome</div>  ----→  #blue { backgound-color: blue;}
- grouping selector: when multiple selector shares the same style declarations, you can just put both selector one after other divided by a comma
  together: .red, .blue { color: white };
- chaining selector: if we have for example two elements with similar classes “this blue” and “this red” you can chain both the class selectors together 
like this : .this.blue { color: blue}.  Or for example 
<div>
<div class="right now">Latest Posts</div>
<p class="right" id="not">
This is where a preview for a post might go. </p>
</div>
.right.not { color: blue}
Descendant combinator
To select nested descendants based on their ancestors, use the descendant combinator which is represented in CSS by a single space between selectors.

<div class="ancestor">
    <div class="contents">
         <div class="contents"></div>
<di class=”contents”></div>

.ancestor .contents {}
In the above example, the first two elements with the contents class (on lines 4 and 5) would be selected, but the last element (on line 9) wouldn’t be. 
CSS property
The color property sets an element’s text color, while background-color sets, well, the background color of an element. Both of these properties can accept
one of several kinds of values: HEX, RGB, HSL and key word (like “red”). Font-family (if the font family has space between words you need to use quotes like ‘ or “), 
font-size, font-weight (boldness), text align, height, width.








The cascade of CSS
The cascade is what determines which rules actually get applied to our HTML. There are different rules that defines what comes first.
Specificity
We have different kind of specificity that could be on declarations or type of styles. The most specific style is inline, which have the highest specificity 
compared to selectors, while each type of selectors has its own specificity level. A CSS declaration that is more specific will take precedence over less specific ones:
1) ID selectors (more specific selector);
2) Class selector;
3)Type selector.
Specificity will only be taken into account when an element has multiple conflicting declarations targeting it. If comparing specificity doesn’t determine a winner,
compare the number of selectors in the same category, the rule with more selectors takes precedence. 
Inheritance
Inheritance refers to certain CSS properties that, when applied to an element, are inherited by that element’s descendants, even if we don’t explicitly write a rule
for those descendants. Typography-based properties (color, font-size, font-family, etc.) are usually inherited, while most other properties aren’t. 
<div id="parent">
  <div class="child"></div>
</div>
#parent {  color: red;}
.child {  color: blue;}
Despite the parent element having a higher specificity with an ID, the child element would have the color: blue style applied since that declaration directly 
targets it, while color: red from the parent is only inherited. If after every other factor has been taken into account there are still multiple conflicting rules 
targeting an element, whichever rule was the last defined is the winner.
There are also hierarchy between the web-server, user and browser, that comes in this order.
HTML vs DOM
When you use a web browser to request a page, the server returns an HTML document, but the browser parses (analizza) the HTML and creates a tree of objets. The 
Document Object Model (DOM) is a programming interface provided by the browser that represents an HTML (or XML) document as a tree of objects.
In simple terms:
    • Your HTML file is just text 
    • The browser parses this text 
    • The browser converts it into a structured object tree 
    • That tree is the DOM 
JavaScript does not manipulate HTML text directly. Instead, it manipulates the DOM. The DOM is a live, in‑memory representation of a document that allows 
programs to read, modify, add, and delete content, structure, and styles.
                                                                             Boxes
The box model
Every single thing on a website is a rectangular box. These boxes can have other boxes inside of them. They are many ways to manipulate the size of these boxes, 
and the space between them, using padding, border and margin.
- content box: The area where your content is displayed; size it using properties like width and height;
- padding increases the space between the border of a box and the content of the box. Unlike margins, you cannot have a negative padding.

Border
Borders adds space between the margin and the padding. If you are using the standard box model, the size of the border is added to the width and height of the 
content box. If you are using the alternative box model, then the bigger the border is, the smaller the content box is, as the border takes up some of that available 
width and height of the element box. For styling borders, there are a large number of properties — there are four borders, and each border has a style, width, and 
color that we might want to manipulate.
To set the properties of each side individually, use:
    • border-top 
    • border-right 
    • border-bottom 
    • border-left 
To set the width, style, or color of all sides, use: border-width, border-style, border-color. To set the width, style, or color of a single side, use one of 
the more granular longhand properties like “border-top-width”, “border-left-style” and so on. 
Margin
Margin is an invisible space, inreases the space between the borders of a box and the borders of adjacent boxes. Margins can have negative and positive value, 
depending on whether two elements whose margins touch have positive or negative margins, the results will be different:
    • Two positive margins will combine to become one margin. Its size will be equal to the largest individual margin. 
    • Two negative margins will collapse and the smallest (furthest from zero) value will be used. 
    • If one margin is negative, its value will be subtracted from the total.  
      
                                                         Elements proprieties
Every element comes with three most important factors:
Sizing: box-sizing;
Layout behavior: display (block, inline, flex, grid, none);
Other layout tools: float, position.


                                                                    BOX-SIZING
In the standard box model, the property box-sizing: content-box, if you set width and height property values on a box, these values define the width and 
height of the content box. Any padding and borders are then added to those dimensions to get the total size taken up by the box
.box {
 width: 350px;
 height: 150px;
 margin: 10px;
 padding: 25px;
 border: 5px solid black;
}
The actual space taken up by the box will be 410px wide (350 + 25 + 25 + 5 + 5) and 210px high (150 + 25 + 25 + 5 + 5).
Box-sizing: border-box
In the alternative box model, any width is the width of the visible box on the page. The content area width is that width minus the width for the padding 
and border (see image below). This is convenient as there is no need to add up the border and padding to get the real size of the box. To turn on the alternative 
model for an element, set box-sizing: border-box on it:
.box {
 width: 350px;
 height: 150px;
 margin: 10px;
 padding: 25px;
border: 5px solid black;
}
                                                                                          
                                                                     DISPLAY
Elements on a webpage lay out in normal flow if you haven’t applied any CSS to change the way they behave between each other. For example elements like <img> 
and <button> are by default with the “display: inline-block” propriety. The display property defines the relationships between multiple boxes in a different ways.
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
When building a web page, not every piece of content has a specific semantic tag. Sometimes, you just need a container you can style or position. That’s where 
<div> (block element) and <span> come in.
Particular elements
For elements the default behavior is  box-sizing: content-box, but there are some particular that have for default inline:
<img> is inline-block
<button> is inline-block
<span> is inline
<textarea> is inline
<input> is inline
<select> is inline-block
Inner and outer display types
Block and inline display values are said to be outer display types — they affect how the box is laid out in relation to other boxes around it. Boxes 
  also have an inner display type, which dictates how elements inside that box are laid out.
You can change the inner display type by setting an inner display value, for example display: flex;. The element will still use the outer display 
  type block but this changes the inner display type to flex. Any direct children of this box will become flex items and behave according to the Flexbox specification.
