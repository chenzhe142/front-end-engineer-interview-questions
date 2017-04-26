# front end study notes
A notebook repo to keep track of front end technologies & knowledges I learned daily.

- [javascript](#javascript)
- [html](#html)
- [css](#css)
- [practical questions](#practical-questions)
- [user experience](#user-experience)
- [system design](#system-design)
- [product-taste](#product-taste)



## javascript

### - ajax: request, response, how to implement, and solve it using native javascripts

AJAX is the use of JavaScript to send and receive using HTTP without reloading the page.

There are two ways of doing Ajax call, one is using `XMLHttpRequest`, and the other is using `fetch`.

XMLHttpRequest: [MDN]()

Using `XMLHttpRequest`

```javascript
var request = new XMLHttpRequest();
request.open("POST", "path/to/api", true);
request.onreadystatechange = function () {
  if (request.readyState != 4 || request.status != 200) return;
  alert("Success: " + request.responseText);
};
request.send("banana=yellow");

var request = new XMLHttpRequest();
request.open('GET', 'http://www.example.com');
request.onreadystatechange = function() {
  if (request.readyState === XMLHttpRequest.DONE && request.status === 200) {
    console.log(request.responseText);
  }
};

request.send();
```

Parameters

```javascript
xhrReq.open(method, url);
// the default value of async is true
xhrReq.open(method, url, async);
xhrReq.open(method, url, async, user);
xhrReq.open(method, url, async, user, password);
```
fetch: [MDN]()

Using `fetch`

```javascript
// use query params
var url = new URL('http://www.example.com/api');
url.searchParams.append('name', 'zchen');

var myRequest = new Request(url, {
  method: 'GET',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json',
    'Origin': 'http://www.example.com'
  },
  mode: 'cors',
  cache: 'default'
});

fetch(myRequest).then(function(response) {
  console.log(response);
}).catch(function(error) {
  console.log('cannot fetch');
  console.log(error);
});

```

Using jQuery

```javascript
$.ajax({
  url: 'www.example.com/api',
  dataType: 'json',
  type: 'GET',
  error: function() {
    console.log('shoot! cannot make ajax call');
  },
  success: function(data) {
    console.log('data retrieved!');
  }
});

```


### - what is prototype
A prototype is an internal object from which other objects inherit properties. Its main purpose is to allow multiple instances of an object to share a common property. Thus, object properties which are defined using the prototype object are inherited by all instances which reference it.


### - prototype inheritance

Unlike class inheritance in other languages (Java, Python, etc.), inheritance in JavaScript is entirely different. Make sure you have read through documentations before interview.

Here are some useful links and books for further reading:

1. MDN Introduction to JavaScript: [prototype inheritance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
2. JavaScript - the good parts

Interviewers usually give you an object, and let you distinguish either the output of a function, or an inner variable's value.


### - difference between prototype inheritance & classical inheritance


### - event capture vs. event bubbling. when to use them?

Event bubbling and capturing are two ways of event propagation in the HTML DOM API, when an event occurs in an element inside another element, and both elements have registered a handle for that event.

The event propagation mode determines in which order the elements receive the event.

With bubbling, the event is first captured and handled by the innermost element and then propagated to outer elements.

With capturing, the event is first captured by the outermost element and propagated to the inner elements.

Further reading:
- [stack overflow - what is event bubbling and capturing?](http://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing)
- [Quirks mode - Event order](http://www.quirksmode.org/js/events_order.html)
- [CSS Tricks - the difference between "return false;" and "event.preventDefault();" ](https://css-tricks.com/return-false-and-prevent-default/)


### - why do you want to prevent event bubbling?


### - event delegation.

`Event delegation allows us to attach a single event listener, to a parent element, that will fire for all descendants matching a selector, whether those descendants exist now or are added in the future.`

`Event delegation refers to the process of using event propagation (bubbling) to handle events at a higher level in the DOM than the element on which the event originated. It allows us to attach a single event listener for elements that exist now or in the future.`

If there are many elements inside one parent, and you want to handle events on them - don’t bind handlers to each element. Instead, bind the single handler to their parent, and get the child from e.target || e.srcElement.

Assume we have an unordered list. We want to output the text when we click on the list element. Note that we may add/delete list elements.

Here is the HTML markup:

```html
<ul class="parent">
 <li>one</li>
 <li>two</li>
 <li>three</li>
</ul>
```

In order to achieve the goal, we can bind function for each `<li>` element. But there is a better way to do it.

From [stack overflow - what is DOM event delegation?](http://stackoverflow.com/questions/1687296/what-is-dom-event-delegation):

```DOM event delegation is a mechanism of responding to ui-events via a single common parent rather than each child, through the magic of event "bubbling" (aka event propagation).```

```Event bubbling provides the foundation for event delegation in browsers. Now you can bind an event handler to a single parent element, and that handler will get executed whenever the event occurs on any of its child nodes (and any of their children in turn). This is event delegation.```

Using event delegation:

```javascript
var target = document.querySelector('.parent');

target.addEventListener('click', function(event) {
  // currentTarget => <ul class="parent">
  console.log(event.currentTarget);

  // target: the element that you are clicking on
  console.log(event.target.textContent);
}, false);
```

#### example 2:
```javascript
document.addEventListener('click', function(event) {
  event.target.style.visibility = 'none';
}, false);
```
We delegate clicking event to `document`. When an element is clicked, use `event.target` to access that element, and set it to `visibility: hidden`.

#### pros
1. With event delegation, the number of event bindings can be drastically decreased by moving them to a common parent element.
2. total memory used by `addEventListener` goes down

#### cons
You need caution when managing some mouse events. If your code is handling the mousemove event; Not all events bubble.; There’s a risk your event management code could become a performance bottleneck.

Further reading:
- [stack overflow - what is DOM event delegation?](http://stackoverflow.com/questions/1687296/what-is-dom-event-delegation)
- [David Walsh - how javascript event delegation works](https://davidwalsh.name/event-delegate)



### - what does `Event.preventDefault()` mean?

- [Quirks mode - Event order](http://www.quirksmode.org/js/events_order.html)
- [CSS Tricks - the difference between "return false;" and "event.preventDefault();" ](https://css-tricks.com/return-false-and-prevent-default/)

### - `==` vs `===`
‘==’ evaluates equality of the value, while ‘===’ evaluates equality of type and value.



### - how to use `addEventListener(eventName, function, useCapture)`



### - how to solve scope issue? what is the scope of `this` referring to in `.bind(this)`?

documentation: [MDN - .bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

```javascript
Function.prototype.bind()
```

We use the Bind () method primarily to call a function with the this value set explicitly. It other words, bind () allows us to easily set which specific object will be bound to this when a function or method is invoked.

This might seem relatively trivial, but often the this value in methods and functions must be set explicitly when you need a specific object bound to the function’s this value.

The need for bind usually occurs when we use the this keyword in a method and we call that method from a receiver object; in such cases, sometimes this is not bound to the object that we expect it to be bound to, resulting in errors in our applications.


### - What is a “closure” in JavaScript? Provide an example/why use closure?


### - `let` vs `var`

#### `var`
`var`-declaring a variable in the head of a for loop creates a **single binding (storage space) for that variable**:

```javascript
const arr = [];
for (var i=0; i < 3; i++) {
    arr.push(() => i);
}
arr.map(x => x()); // [3,3,3]
```

Every i in the bodies of the three arrow functions refers to the same binding, which is why they all return the same value.

#### `let`

If you let-declare a variable, **a new binding is created for each loop iteration**:

```javascript
const arr = [];
for (let i=0; i < 3; i++) {
    arr.push(() => i);
}
arr.map(x => x()); // [0,1,2]

```
This time, each i refers to the binding of one specific iteration and preserves the value that was current at that time. Therefore, each arrow function returns a different value.


- [ES6 - variables and scoping](http://exploringjs.com/es6/ch_variables.html#sec_let-const-loop-heads)


### - what is promise? how to use it?

See documentation: [MDN Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

Blog post: [usage of Promise](https://www.toptal.com/javascript/javascript-promises)

```javascript
var rollDice = function() {
  return Math.ceil(Math.random() * 6);
};

var newPromise = new Promise(function(resolve, reject) {
  var n = rollDice();
  if (n === 6) {
    resolve(n);
  } else {
    reject(n);
  }
}).then(function(n) {
  console.log('you win!');
}).catch(function(error) {
  console.log('cannot resolve');
  console.log(error);
});

```

### - callback vs promise

*promise*: promise is a method that let you handle asynchronous operation based the operation's final state.

If it's resolved or fulfilled, we do a function. Or it is rejected, we do another function. syntax is better.

*callback*: function used as another function's parameter / arguments


### - what is event loop?

JavaScript runtimes contain a message queue, and it stores a list of messages to be processed and their associated callback functions.

In a loop, the queue grabs for the next message, and calls its associated function. Since javascript is single-threaded, queue waits for the function to be finished, and then get the next message.

- [The javascript event loop: explained](http://blog.carbonfive.com/2013/10/27/the-javascript-event-loop-explained/)


### - Non-blocking javascript: we know that browser is single-threaded, and other tasks will be blocked if one task is not yet finished. how would you solve this issue?

1. Service Worker - [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)

2. Split one huge task into small tasks. For example, use `setTimeout()` to call a certain function. [Stack overflow](http://stackoverflow.com/questions/26615966/how-to-make-non-blocking-javascript-code)

3. If the task is too heavy, let server do the job.


### - immediately-invoked function express
```javascript
(function test() {
    console.log('kakak');
})();

var a = function() {
    console.log('a');
}();
```

- [Ben Alman - immediately invoked function expression](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)

### -debouncing

- [David Walsh - Function debounce](https://davidwalsh.name/function-debounce)
- [CSS Tricks - the difference between throttling and debouncing](https://css-tricks.com/the-difference-between-throttling-and-debouncing/)

## html


### - what is `iframe`?

### - what's new in HTML5?


### - how to use data attributes?
To access `data` attribute, use `element.dataset.attributeName`.

Usage:

1. tracking user behavior, such as clicking event.

Pros:

1. Easy to store some data on a tag. Easy access.

Cons:

1. Do not store content that should be visible and accessible in data attributes, because assistive technology may not access them.
2. In addition, search crawlers may not index data attributes' values.
3. `element.dataset.attributeName` does not work on IE 10 and before. To use it, use `.getAttribute()`.

### - What is Doctype & why its important?


### - What are meta tags?




## css



### - what is `float`?
In web design, page elements with the CSS float property applied to them are just like the images in the print layout where the text flows around them. Floated elements remain a part of the flow of the web page. This is distinctly different than page elements that use absolute positioning. Absolutely positioned page elements are removed from the flow of the webpage.


### - explain clearfix
A clearfix is a way for an element to automatically clear its child elements, so that you don't need to add additional markup. It's generally used in float layouts where elements are floated to be stacked horizontally. The clearfix is a way to combat the zero-height container problem for floated elements.

```css
.clearfix {
  overflow: auto;
}
```

or:

```css
.clearfix:after {
   content: "";
   visibility: hidden;
   display: block;
   height: 0;
   clear: both;
}
```



## browser compatibility




## practical questions

### - lazy loading images

[CSS Tricks - lazy loading](https://css-tricks.com/snippets/javascript/lazy-loading-images/)

### - infinite scrolling

### - form validation

### - how to check if an element is in viewport?

### - design a calendar

### - How to give <a> so that it won’t take you to another page but gives you alert message.

```javascript
var aTag = document.querySelector('a');
a.addEventListener('click', function(event) {
  alert('hey');
  event.preventDefault();
}, false);
```

### - how to track user clicking event?

#### example 1: save clicked elements into an array
See codepen demo [here](http://codepen.io/chenzhe142/pen/PWBbJo?editors=1111)

```html
<div class="container">
  <a href="#section-a" class="post">post a new comment</a>
</div>

<div class="section">
  <div class="section-a">
    this is section a
  </div>
</div>
```

```javascript
var clickingElements = [];

document.addEventListener('click', function(event) {

  console.log('trigger post');
  clickingElements.push(event.target);
  console.log(clickingElements);

}, false);
```
Use event delegation, delegating all elements's event inside of `<body>` to `document`. When any element is clicked, add `eventTarget` to `clickingElements` array.

#### example 2: when clicking an element, trigger a `POST`, writing into backend database for logging


### - what is cookie, and how to set it?

### - write a function to toggle `checkAll` checkbox, and other normal boxes



## user experience

Although UX design is not the main focus of front end engineers, interviewers may still ask you and check your understanding on good user experience. It would be good to have some basic understanding on UX, and stay up-to-date for the latest UX trend.


### - when to use optimistic update?
