# front-end-engineer-interview-questions
A collection of questions I have been asked during front end job interview.
Some of the practical questions are pretty challenging and interesting to solve.
Hope this helps you prepare your interview better!

Please feel free to create pull requests, and add your interview questions here. :)

## javascripts
- ajax: request, response, how to implement, and solve it using native javascripts

There are two ways of doing Ajax call, one is using `XMLHttpRequest`, and the other is using `fetch`.

XMLHttpRequest: [MDN]()

Using `XMLHttpRequest`
```
```

fetch: [MDN]()

Using `fetch`
```
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


- prototype inheritance

Unlike class inheritance in other languages (Java, Python, etc.), inheritance in JavaScript is entirely different. Make sure you have read through documentations before interview.

Here are some useful links and books for further reading:
1. MDN Introduction to JavaScript: [prototype inheritance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
2. JavaScript - the good parts

Interviewers usually give you an object, and let you distinguish either the output of a function, or an inner variable's value.


- event delegation
- event capture vs. event bubbling
- `==` vs `===`
- how to use `addEventListener(eventName, function, useCapture)`
- what does `Event.preventDefault()` mean?
- how to solve scope issue? what is the scope of `this` referring to in `.bind(this)`?
- `let` vs `var`
- what is promise? how to use it?

See documentation: [MDN Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

Blog posts: [usage of Promise](https://www.toptal.com/javascript/javascript-promises)

```
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
- web accessibility: how to make `<a>` tag accessible?
- what are the commonly used attributes in order to make tags accessible?
- what is `iframe`?

## css

## frameworks
- how do you think of Angular 2?
- what do you like about React?

## practical questions
- lazy loading images
- infinite scrolling
- form validation
- how do you make a website faster?
- how to track user clicking event?
- how to implement an infinite scrolling carousel?
- what is cookie, and how to set it?
- write a function to toggle `checkAll` checkbox, and other normal boxes

## user experience
Although UX is not the main job of front end engineers, interviewers may still ask you and check your understanding on good user experience. It would be good to have some basic understanding on UX, and stay up-to-date for the latest UX trend.
- what do you think makes a good UX engineer?
- when to use optimistic update?
