# DOM API

## methods

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

### 'FormData'
```javascript
var formElement = document.querySelector('form');
var formData = new FormData(formElement);
formData.append('username', 'Zoe');
```
