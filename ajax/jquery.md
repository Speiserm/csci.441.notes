## JQuery

### Test points:
#### [1. Why use a CDN?](#cdn)

#### [2. Why do // instead of http:// or https://?](#slashes)

#### [3. Breaking down a jQuery call](#syntax)

#### [4. Do selection by id, class, and tag type](#selection)

#### [5. Write code for ready event, event listener, DOM val(), and getting/setting DOM html()](#code)

---

### What is JQuery?
JQuery is a Library which aims to:
- Reduce the amount of code you need to write
- Ease DOM manipulation and events
- Eliminate cross browser incompatibilities
- Make AJAX simpler

It is used by over 50% of websites, including Google, Microsoft, Netflix, etc.

### How to use jQuery
JQuery comes in two forms
- Development - Fully documented version
- Production - Minified

Then, you should include a `<script>` tag on the page.
```html
<html>
<body>
  <h1>Hi!</h1>
  <script src="jquery.min.js"></script>
  <script>
  // Your code here
  </script>
</body>
</html>
```
<a name="cdn"></a>
### The better way, a Content Delivery Network
__Why use a CDN?__

Using a CDN can make it so your site delivers content much faster. It offloads the jQuery loading to the CDN and takes a load off of your site. If you have a highly trafficked website, it can speed up the content much faster for several users, especially if they're close to a server where it is being delivered from. The disadvantages to it is that it may cost money, and that it can make development a little more difficult. Users could also have filters which would block the CDN.

You can implement it in the same way as before, but by linking to the CDN instead of local javascript:
```html
<html>
<body>
  <h1>Hi!</h1>
  <scriptsrc="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
  <script>
  // Your code here
  </script>
</body>
</html>
```
<a name="slashes"></a>
__Why do you use `//` instead of `http://` or `https://`?__
If you use // in the URL instead of `http://` or `https://`, it makes the request agnostic to HTTP vs HTTPS, so you don't have to worry about getting denied because you're not using HTTPS or using HTTPS when it wants HTTP.

### Why use jQuery?
It makes everything a lot easier. Here's a few examples to convince you:

No library:
```java
var elems = document.getElementsByTagName("img");
for(var i =0; i< elems.length; i++){
  elems[i].style.display ="none";
}
```

jQuery:
```java
$('img').hide();
```

No library:
```java
var p = document.createElement('p');
p.appendChild(document.createTextNode('Welcome!'));
p.style.cssFloat ='left';
p.style.backgroundColor ='red';
p.className ='special';
document.querySelector('div.header').appendChild(p);
```

jQuery:
```java
var newP = $('<p>Welcome!</p>');
newP.css({'float':'left','background‐color':'red'});
newP.addClass('special');
$('div.header').append(newP);
```

<a name="syntax"></a>
### How to use jQuery
1. Select element

  `$('p')`

2. Use a jQuery method to manipulate

  `$('p').addClass('special');`

This would turn
`<p>Welcome to jQuery!</p>`
into:
`<p class="special">Welcome to jQuery!</p>`

But it would also add that class to all other `<p>` tags since you selected by that tag.


__Breaking down the jQuery call:__

`$('p').addClass('special');`

|`$`|('p')|addClass('special')|
|---|---|---|
|The global jQuery function. Can also be "jQuery".|Finds DOM element(s) according to whatever is in the quotes.|Built-in jQuery method that adds the specified class to the collection.|

<a name="syntax"></a>
### Selection with jQuery
__All CS selectors are valid, plus more.__

Type|Example|How to select it
---|---|---
HTML tag|`<p>Welcome!</p>`|`$('p')`
ID|`<p id="main">Welcome!</p>`|`$('#main')`
Class|`<p class="intro">Welcome!</p>`|`$('.intro')`
Class within div|`<div id="main><p class="intro">Welcome</p></div>`|`$(#main .intro)`

__Creating and injecting with jQuery__

You can inject HTML easily by creating and manipulating it:
1. Create element and store a reference

Here's some examples of creating HTML:

|jQuery|Created HTML|
|---|---|
|`$('<p>');`|`<p></p>`|
|`$('<p>Welcome!</p>');`|`<p>Welcome!</p>`|
|`$('<p class="intro">Welcome!</p>');`|`<p class="intro">Welcome!</p>`|

And, we can store a reference to our new element:

`var myParagraph = $('<p class="intro">Welcome!</p>');`

2. Use a method to manipulate (Optional)

  Now that we've got our reference, we can manipulate it:

  `myParagraph.css('font‐size','4em');`

3. Inject into your HTML

  Finally, we can take our reference and inject it directly into our HTML:

  `$('body').append(myParagraph);`

  `$('body').prepend(myParagraph);`

### jQuery events
jQuery is also designed to make events easier, including clicks, keypresses, focus, and changes to these.

One of the most common events is the ready method:
```java
$(document).ready(function(){
  // your script goes here
});
```
or
```java
$(function() {
  // your script goes here
});
```

Both of these wait until the DOM is ready and built before the function is called.
