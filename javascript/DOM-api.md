# DOM API

- [Event](#event)
  - event flow
  - `event.target`
  - `event.currentTarget`
  - `event.eventPhase`
  - creating `CustomEvent`
- [Node](#node)
- [Element](#element)
- [Viewport](#viewport)

## Event

### [Event dispatch and DOM event flow - W3](https://www.w3.org/TR/DOM-Level-3-Events/#event-flow)
![DOM Event Flow](https://www.w3.org/TR/DOM-Level-3-Events/images/eventflow.svg)
1. capture phase
2. target phase
3. bubble phase

Event objects complete these phases as described below. A phase will be skipped if it is not supported, or if the event object’s propagation has been stopped. For example, if the `bubbles` attribute is set to `false`, the bubble phase will be skipped, and if `stopPropagation()` has been called prior to the dispatch, all phases will be skipped.

### `Event.target`: element that triggers the event

### `Event.currentTarget`: element where the event is originally binded to.

### `Event.eventPhase`
- `Event.NONE`
- `Event.CAPTURING_PHASE`
- `Event.AT_TARGET`
- `Event.BUBBLING_PHASE`

### `Event order`
http://www.quirksmode.org/js/events_order.html#link4

## Creating custom event
[MDN - create & dispatch customized event](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Creating_and_triggering_events)

## Node

- A `node` is the generic name for any type of object in the DOM hierarchy.
- A node could be one of the built-in DOM elements such as `document` or `document.body`. it could be an HTML tag specified in the HTML such as `<input>` or `<p>` or it could be a text node that is created by the system to hold a block of text inside another element.
- a node is any DOM object

### modify itself
1. `node.remove()`: removes the object from the tree it belongs to.
2. `node.cloneNode(shouldDeepCopy)`
    - if `shouldDeepCopy` sets to true, the method will copy childNodes as well.
    - `.cloneNode()` doesn't copy JavaScript properties that you added to DOM nodes, such as event handlers. It only copies attributes and optionally, childNodes.
3. `node.append()`
    - The `ParentNode.append` method inserts a set of `Node` objects or `DOMString` objects after the last child of the ParentNode.
      - `DOMString` objects are inserted as equivalent `Text` nodes.
      - Polyfill Source: https://github.com/jserz/js_piece/blob/master/DOM/ParentNode/append()/append().md

### with children nodes
1. `node.children`
    - a read-only property that returns a live `HTMLCollection` of the child elements of Node.
    - `Node.children` is an array-like object.
    - To convert it to an array
```javascript
var childrenNode = divElement.children;
var childrenNodeList = [];

for (let i = 0; i < childrenNode.length; i += 1) {
  childrenNodeList.push(childrenNode[i]);
}
```
2. `node.childNodes`
3. `node.firstChild`
4. `node.lastChild`
5. `node.hasChildNodes()`
6. `node.replaceChild(oldNode, newNode)`
7. `node.removeChild(node)`
8. `node.insertBefore(nodeToInsert, referenceNode)`
    - if `referenceNode` is `null`, it acts like `appendChild()`
9. `node.appendChild()`
    - It adds a node to the end of the list of children of a specified parent node.
    - If the given child is a reference to an existing node in the document, it moves it from its current position to the new position.
    - If needed, use `Node.cloneNode()` to get a copy, and use `.appendChild()` method

### With neighbor nodes
1. `node.nextSibling`
2. `node.previousSibling`

### With parent node
1. `node.parentNode`

### With elements
1. `node.parentElement`
2. `node.nextElementSibling`
3. `node.previousElementSibling`

### - `node.parentNode` vs `node.parentElement`
  - In most cases, it is the same as parentNode.
  - The only difference comes when a node's parentNode is not an element. If so, parentElement is null.

### - `HTMLElement vs Node`
[MDN - Node.nodeType](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType)

## `Element`
- An `element` is one specific type of node.
- And there are many other types of nodes (text nodes, comment nodes, document nodes, etc...).

### `Element.id`

### `Element.classList`: return `DOMTokenList`

### `Element.classNames`: return `DOMString`

### `Element.innerHTML`

### `Element.tagName`

### `Element.getAttribute(attributeName)`

### `Element.hasAttribute(attributeName)`

### `Element.removeAttribute(attributeName)`

### `Element.setAttribute(attributeName, attributeValue)`

### `Element.querySelector()`

### `Element.querySelectorAll()`

### `Element.style`

### `HTMLElement.dataset`: access `data-*`
- access with **camelCase** => `data-member-id` as `dataset.memberId`

## The Document type
`Document` represents the document node.

- `nodeName`: `#document`
- `nodeValue`: `null`
- `parentNode`: `null`
- `document.body` refers to `<body>` element
- `document.documentElement` refers to `<html>` element
- `document.title` refers to the page title
- `document.URL`
- `document.domain`

## Selector API

### - `querySelector()`
### - `querySelectorAll()`
### - `matchesSelector()` check if an element would be returned by `querySelectorAll` or `querySelector`
### - `getElementsByClassName()` is added in HTML5
### - `node.classList` provides a way to easily manipulate class names
  - `add`
  - `remove`
  - `toggle`
  - `contains`

### -  Focus management
  - `document.activeElements` contains a pointer to the DOM element that currently has focus
  - `.focus()`
  - `document.hasFocus()`

### - Custom Data `data-`
access by `node.dataset.appId`

### - Markup insertion
  1. `.innerHTML` it is not available for all elements. Be extremely careful when using this method.
  2. `.outerHTML`
  3. `.insertAdjacentHTML()`

When using the methods above, it is best to manually remove all event handlers and properties that are on elements.

### - `node.innerText`

### - `scrollIntoView()`

### - `node.children` contains `element` node

### - `parentNode.contains(childNode)`

## Viewport

### - `getBoundingClientRect()`
The `Element.getBoundingClientRect()` method returns the size of an element and its position relative to the viewport.

```javascript
ClientRect {
  top: -110,
  right: 672,
  bottom: -29,
  left: 0,
  width: 672
}
```

### - `clientHeight`
MDN: [Element.clientHeight()](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientHeight)



## `HTMLCollection()`
The `HTMLCollection` interface represents **a generic collection** (**array-like object** similar to `arguments`) of elements (in document order) and offers methods and properties for selecting from the list.

- `HTMLCollection.length`
- `HTMLCollection.item()` - Returns the specific node at the given zero-based index into the list. Returns null if the index is out of range.

## `Image()`

```javascript
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  var img = new Image();
  img.onload = function() {
    ctx.drawImage(img, 0, 0);
    ctx.beginPath();
    ctx.moveTo(30, 96);
    ctx.lineTo(70, 66);
    ctx.lineTo(103, 76);
    ctx.lineTo(170, 15);
    ctx.stroke();
  };
  img.src = 'https://mdn.mozillademos.org/files/5395/backdrop.png';
}
```
See result in [here](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Using_images)

## `FormData`
```javascript
var formElement = document.querySelector('form');
var formData = new FormData(formElement);
formData.append('username', 'Zoe');
```

## `EventSource`
MDN - [EventSource](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)
```javascript
// create a EventSource object
var evtSource = new EventSource("//api.example.com/ssedemo.php", { withCredentials: true } );

// listen to a message
evtSource.onmessage = function(e) {
  var newElement = document.createElement("li");

  newElement.innerHTML = "message: " + e.data;
  eventList.appendChild(newElement);
}

```
