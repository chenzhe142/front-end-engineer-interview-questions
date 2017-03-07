# DOM API

## DOM Element Node

### - `node.children`
- a read-only property that returns a live `HTMLCollection` of the child elements of Node.
- `Node.children` is an array-like object.

#### To convert it to an array
```javascript
var childrenNode = divElement.children;
var childrenNodeList = [];

for (let i = 0; i < childrenNode.length; i += 1) {
  childrenNodeList.push(childrenNode[i]);
}


```

### - `node.firstChild`

### - `node.lastChild`

### - `node.nextSibling`

### - `node.previousSibling`

### - `node.parentNode`

### - `node.parentElement`

### - `node.nextElementSibling`

### - `node.previousElementSibling`

### - `HTMLElement.dataset`
- it allows access, both in reading and writing mode, to all the custom data attributes (`data-*`) set on the element, either in HTML or in the DOM.
- access with **camelCase**

### - `Element.setAttribute('attributeName', 'value')`

### - `ParentNode.append()`
The `ParentNode.append` method inserts a set of `Node` objects or `DOMString` objects after the last child of the ParentNode. 

- `DOMString` objects are inserted as equivalent `Text` nodes.
- Polyfill Source: https://github.com/jserz/js_piece/blob/master/DOM/ParentNode/append()/append().md

### - `Node.appendChild()`
- It adds a node to the end of the list of children of a specified parent node. 
- If the given child is a reference to an existing node in the document, it moves it from its current position to the new position.
- If needed, use `Node.cloneNode()` to get a copy, and use `.appendChild()` method

### - `Node.cloneNode()`: returns a duplicate of the node on which this method was called.

```javascript
// set deep to true if you want to clone its children.
var dupNode = node.cloneNode(deep);
```

### - `ChildNode.remove()`: removes the object from the tree it belongs to.

### - `node.parentNode` vs `node.parentElement`
- In most cases, it is the same as parentNode. 
- The only difference comes when a node's parentNode is not an element. If so, parentElement is null.

### - `HTMLElement vs Node`

#### `node`

- A `node` is the generic name for any type of object in the DOM hierarchy. 

- A node could be one of the built-in DOM elements such as `document` or `document.body`. it could be an HTML tag specified in the HTML such as <input> or <p> or it could be a text node that is created by the system to hold a block of text inside another element. 

- So, in a nutshell, **a node is any DOM object**.

#### `element`

- An `element` is one specific type of node. 
- And there are many other types of nodes (text nodes, comment nodes, document nodes, etc...).



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

## `Array`

### `Array.prototype.splice(start, deleteCount, item1, item2, ...)`

### `Array.isArray()`

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
