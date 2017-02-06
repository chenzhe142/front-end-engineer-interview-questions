# front-end-engineer-interview-questions
A collection of questions I have been asked during front end job interview.
Some of the practical questions are pretty challenging and interesting to solve.
Hope this helps you prepare your interview better!

Please feel free to create pull requests, and add your interview questions here. :)

- [javascript](#javascript)
- [html](#html)
- [css](#css)
- [frameworks](#frameworks)
- [practical questions](#practical-questions)
- [user experience](#user-experience)

## javascript
### - ajax: request, response, how to implement, and solve it using native javascripts

There are two ways of doing Ajax call, one is using `XMLHttpRequest`, and the other is using `fetch`.

XMLHttpRequest: [MDN]()

Using `XMLHttpRequest`
```
```

fetch: [MDN]()

Using `fetch`
```javascript
var myRequest = new Request('http://www.zhechen.co/', {
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


### - prototype inheritance

Unlike class inheritance in other languages (Java, Python, etc.), inheritance in JavaScript is entirely different. Make sure you have read through documentations before interview.

Here are some useful links and books for further reading:

1. MDN Introduction to JavaScript: [prototype inheritance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
2. JavaScript - the good parts

Interviewers usually give you an object, and let you distinguish either the output of a function, or an inner variable's value.


### - event capture vs. event bubbling. when to use them?

Event bubbling and capturing are two ways of event propagation in the HTML DOM API, when an event occurs in an element inside another element, and both elements have registered a handle for that event.

The event propagation mode determines in which order the elements receive the event.

With bubbling, the event is first captured and handled by the innermost element and then propagated to outer elements.

With capturing, the event is first captured by the outermost element and propagated to the inner elements.

Further reading:
- [stack overflow - what is event bubbling and capturing?](http://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing)

### - event delegation.

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

#### what's good about event delegation
1. With event delegation, the number of event bindings can be drastically decreased by moving them to a common parent element.
2. total memory used by `addEventListener` goes down

Further reading:
- [stack overflow - what is DOM event delegation?](http://stackoverflow.com/questions/1687296/what-is-dom-event-delegation)
- [David Walsh - how javascript event delegation works](https://davidwalsh.name/event-delegate)

### - `==` vs `===`
### - how to use `addEventListener(eventName, function, useCapture)`
### - what does `Event.preventDefault()` mean?
### - how to solve scope issue? what is the scope of `this` referring to in `.bind(this)`?

documentation: [MDN - .bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

```javascript
Function.prototype.bind()
```

### - `let` vs `var`
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

## html
### - what is website accessibility, and how to improve the accessibility of a website?
It means people with disabilities can use the web. In details, they can perceive, navigate and interact with the website.

How to improve:
1. Do not make your pages dependent on images
2. Make sure all your images have ALT text. Screen readers cannot "read images". In order for your images meaningful for people with disabilities, you need to add written descriptions for the images.
3. Don't make the font size too small
4. Use highly contrasting colors for your text and background.
5. Screen reader friendly: use proper `aria` label, name and descriptions to navigate users to interact the page.
6. Use semantic markups, and then enhance with ARIA.
7. etc.

To use accessibility API describe an object:
1. role
2. name
3. state

Further readings:
- [w3.org - Introduction to web accessibility](https://www.w3.org/WAI/intro/accessibility.php)
- [w3.org - How people with disabilities use the web](https://www.w3.org/WAI/intro/people-use-web/Overview.html)
- [Smashing magazine - web accessibility with accessibility API](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/)

### - web accessibility: how to make `<a>` tag accessible?
### - what are the commonly used attributes in order to make tags accessible?
### - what is `iframe`?
### - can you nest `<a>`?
### - what's new in HTML5?
### - how to use data attributes?

## css
### - what CSS preprocessor do you use? Pros and cons?
I use `Stylus` and `PostCSS` (with css-next plugin).

Pros:
1. nested syntax
2. can use variable, function, mixins, etc.
3. etc.

Cons:
1. harder to debugging. change file -> compile -> refresh page to see changes
2. learning curve

### - what is `float`?

## frameworks
### - how do you think of Angular 2?
### - what do you like about React?

## practical questions
### - lazy loading images
### - infinite scrolling
### - form validation
### - how to check if an element is in viewport?
### - design a calendar
### - how do you make a website faster?
### - how to track user clicking event?
### - how to implement an infinite scrolling carousel?
### - what is cookie, and how to set it?
### - write a function to toggle `checkAll` checkbox, and other normal boxes

## user experience
Although UX design is not the main focus of front end engineers, interviewers may still ask you and check your understanding on good user experience. It would be good to have some basic understanding on UX, and stay up-to-date for the latest UX trend.
### - what do you think makes a good UX engineer?
### - when to use optimistic update?
