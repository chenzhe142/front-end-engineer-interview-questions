# Dealing with pragmatic issues

## JavaScript
1. access一个object中的key需要`O(n)`
2. access a value in array by index需要`O(1)`

## Web Performance

In addition to general programming best practices, you should expect for interviewers to look at your code or design and its performance implications. It used to be enough to put CSS at the top of a document and JS scripts at the bottom of a page but the web is moving fast and you should be familiar with the complexities in this space.

- Critical rendering path.
- Service workers.
- Image optimizations.
- Lazy loading and bundle splitting.
- General implications of HTTP/2 and server-push.
- When to prefetch and preload resources.
- Reduce browser reflows and when to promote an element to the GPU.
- Differences between the browser layout, compositing and painting.

## `throttle` 

我们这里说的throttle就是函数节流的意思。再说的通俗一点就是函数调用的频度控制器，是连续执行时间间隔控制。主要应用的场景比如：

- 鼠标移动，mousemove 事件
- DOM 元素动态定位，window对象的resize和scroll 事件

有人形象的把上面说的事件形象的比喻成机关枪的扫射，throttle就是机关枪的扳机，你不放扳机，它就一直扫射。我们开发时用的上面这些事件也是一样，你不松开鼠标，它的事件就一直触发。

```javascript
function throttle(fn, threshhold, scope) {
  threshhold || (threshhold = 250);
  var last,
      deferTimer;
  return function () {
    var context = scope || this;

    var now = +new Date,
        args = arguments;
    if (last && now < last + threshhold) {
      // hold on to it
      clearTimeout(deferTimer);
      deferTimer = setTimeout(function () {
        last = now;
        fn.apply(context, args);
      }, threshhold);
    } else {
      last = now;
      fn.apply(context, args);
    }
  };
}
```

```
/*
* 频率控制 返回函数连续调用时，fn 执行频率限定为每多少时间执行一次
* @param fn {function}  需要调用的函数
* @param delay  {number}    延迟时间，单位毫秒
* @param immediate  {bool} 给 immediate参数传递false 绑定的函数先执行，而不是delay后后执行。
* @return {function}实际调用函数
*/
var throttle = function (fn,delay, immediate, debounce) {
   var curr = +new Date(),//当前事件
       last_call = 0,
       last_exec = 0,
       timer = null,
       diff, //时间差
       context,//上下文
       args,
       exec = function () {
           last_exec = curr;
           fn.apply(context, args);
       };
   return function () {
       curr= +new Date();
       context = this,
       args = arguments,
       diff = curr - (debounce ? last_call : last_exec) - delay;
       clearTimeout(timer);
       if (debounce) {
           if (immediate) {
               timer = setTimeout(exec, delay);
           } else if (diff >= 0) {
               exec();
           }
       } else {
           if (diff >= 0) {
               exec();
           } else if (immediate) {
               timer = setTimeout(exec, -diff);
           }
       }
       last_call = curr;
   }
};
 
/*
* 空闲控制 返回函数连续调用时，空闲时间必须大于或等于 delay，fn 才会执行
* @param fn {function}  要调用的函数
* @param delay   {number}    空闲时间
* @param immediate  {bool} 给 immediate参数传递false 绑定的函数先执行，而不是delay后后执行。
* @return {function}实际调用函数
*/
 
var debounce = function (fn, delay, immediate) {
   return throttle(fn, delay, immediate, true);
};
```

## `debounce`
debounce和throttle很像，debounce是空闲时间必须大于或等于 一定值的时候，才会执行调用方法。

debounce是空闲时间的间隔控制。比如我们做autocomplete，这时需要我们很好的控制输入文字时调用方法时间间隔。一般时第一个输入的字符马上开始调用，根据一定的时间间隔重复调用执行的方法。对于变态的输入，比如按住某一个建不放的时候特别有用。

debounce主要应用的场景比如：

- 文本输入keydown 事件，keyup 事件，例如做autocomplete

```javascript
// as long as the event is triggered, it won't invoke the function.
_.debounce = function(func, wait, immediate) {
    var timeout, result;
    
    return function() {
      var context = this, args = arguments;
      var later = function() {
        timeout = null;
        if (!immediate) result = func.apply(context, args);
      };
      
      var callNow = immediate && !timeout;
      
      clearTimeout(timeout);
      
      timeout = setTimeout(later, wait);
      
      if (callNow) {
        result = func.apply(context, args);
      }
      
      return result;
    };
  };
```

## Reflow
### [Stack overflow - what is DOM reflow](http://stackoverflow.com/questions/27637184/what-is-dom-reflow)
### [Repaints and reflows: manipulating the DOM responsibly](http://blog.letitialew.com/post/30425074101/repaints-and-reflows-manipulating-the-dom)

A **reflow** computes the layout of the page. A reflow on an element recomputes the dimensions and position of the element, and it also triggers further reflows on that **element’s children, ancestors and elements that appear after it in the DOM**. Then it calls a final repaint. 

**Reflowing is very expensive, but unfortunately it can be triggered easily.**

Reflow occurs when:
- insert, remove or update an element in the DOM
- modify content on the page, e.g. the text in an input box
- move a DOM element
- animate a DOM element
- take measurements of an element such as offsetHeight or getComputedStyle
- change a CSS style
- change the className of an element
- add or remove a stylesheet
- resize the window
- scroll

### How to prevent
1. avoid setting multiple inline styles, setting styles individually.
2. use `classNames` of elements and do so as low as in the DOM tree as possible.
3. batch DOM changes, and perform changes "offline". i.e., removing the element from the active DOM (`$.detach()` in jQuery), performing DOM changes, and re-appending the element to the DOM.
4. avoid computing styles too often. try to cache values.
5. apply animations with position `fixed` or `absolute`.
6. stay away from table layouts.

## repaint
It goes through all the elements and determines their visibility, colour, outline and other visual style properties, then it updates the relevant parts of the screen.

## The rendering cycle
### Video: [Google I/O 2013 - True Grit: Debugging CSS & Render Performance](https://www.youtube.com/watch?v=gqc88qWuiI4)

Edits to the document cause the browser to enter the rendering cycle.

1. Build the DOM
2. Calculate CSS property values
3. Build the rendering tree
4. Calculate layout
5. Paint
6. Composite

## autocomplete - triggering multiple ajax call
- use `event.preventDefault()` to cancel previous events.
- Cancels the event if it is cancelable, without stopping further propagation of the event.
