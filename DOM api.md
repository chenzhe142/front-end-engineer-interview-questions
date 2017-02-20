# DOM API

## methods

### DOM Element Node

#### - `ParentNode.append()`
The `ParentNode.append` method inserts a set of `Node` objects or `DOMString` objects after the last child of the ParentNode. 

`DOMString` objects are inserted as equivalent `Text` nodes.

**polyfill for IE 9 and higher:**
```javascript
// Source: https://github.com/jserz/js_piece/blob/master/DOM/ParentNode/append()/append().md
(function (arr) {
  arr.forEach(function (item) {
    if (item.hasOwnProperty('append')) {
      return;
    }
    Object.defineProperty(item, 'append', {
      configurable: true,
      enumerable: true,
      writable: true,
      value: function append() {
        var argArr = Array.prototype.slice.call(arguments),
          docFrag = document.createDocumentFragment();
        
        argArr.forEach(function (argItem) {
          var isNode = argItem instanceof Node;
          docFrag.appendChild(isNode ? argItem : document.createTextNode(String(argItem)));
        });
        
        this.appendChild(docFrag);
      }
    });
  });
})([Element.prototype, Document.prototype, DocumentFragment.prototype]);
```

#### - `Node.appendChild()`
- It adds a node to the end of the list of children of a specified parent node. 
- If the given child is a reference to an existing node in the document, it moves it from its current position to the new position.
- If needed, use `Node.cloneNode()` to get a copy, and use `.appendChild()` method

### Viewport

#### - `getBoundingClientRect()`
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

#### - `clientHeight`
MDN: [Element.clientHeight()](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientHeight)

## object

### `Image()`

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

### `Array`

#### `Array.prototype.splice(start, deleteCount, item1, item2, ...)`

### `FormData`
```javascript
var formElement = document.querySelector('form');
var formData = new FormData(formElement);
formData.append('username', 'Zoe');
```

### `EventSource`
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
