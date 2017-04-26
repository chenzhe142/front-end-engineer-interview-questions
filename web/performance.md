# Dealing with pragmatic issues

- [JavaScript tricks](#javascript)
- [Web Performance](#web-performance)
- [lazy-loading](#lazy-loading)
- [throttle](#throttle)
- [debounce](#debounce)
- [reflow](#reflow)
- [repaint](#repaint)

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

## lazy-loading
本章节摘自文章：[学习原生JS延时加载](https://www.denpe.com/javascript-images-lazyload/)

1. 基本原理

  - 正常网页页面结构：头部CSS样式和少量JS；中间部分是内容，包括图片、视频、文本等；底部主要JS文件。
  - 浏览器打开网页时这些资源按顺序从前到后逐一加载，而大多页面都无法一屏显示完全。
  - 如果初次打开页面时让浏览器只加载可视区域的图片，不加载当前不可见图片，就可以把下载看不见图片的时间用来下载页面后面的js等内容，大大提高页面访问速度。
  - 当鼠标像下滚动浏览器时，再按需加载出现在可视区的图片。

2. 方法
  ![lazy-loading](https://www.denpe.com/content/images/2016/01/imglazyload.png)
  ```javascript
  const getTopOffset = function(element) {
    let offset = 0;

    while (element.offsetParent) {
      offset += element.offsetTop;
      element = element.offsetParent;
    }

    return offset;
  }

  const img = document.getElementsByTagName('img')[0];

  if (img.offsetTop <= document.body.scrollTop + window.innerHeight) {
    img.src = img.dataset.imgSrc;
  }
  ```

  jQuery's implementation of calculating offset:

  `到viewport top的offset + window.scrollTop = total top offset`

  ```javascript
  rect = elem.getBoundingClientRect();

	doc = elem.ownerDocument;
	docElem = doc.documentElement;
	win = doc.defaultView;

	return {
		top: rect.top + win.pageYOffset - docElem.clientTop,
		left: rect.left + win.pageXOffset - docElem.clientLeft
	};
  ```

## infinite scrolling & loading
本章节摘自[JS+HTML实现列表动态无限滚动](https://segmentfault.com/a/1190000008730771)


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

```javascript
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

```

## `debounce`
debounce和throttle很像，debounce是空闲时间必须大于或等于 一定值的时候，才会执行调用方法。

debounce是空闲时间的间隔控制。比如我们做autocomplete，这时需要我们很好的控制输入文字时调用方法时间间隔。一般时第一个输入的字符马上开始调用，根据一定的时间间隔重复调用执行的方法。对于变态的输入，比如按住某一个建不放的时候特别有用。

debounce主要应用的场景比如：

- 文本输入keydown 事件，keyup 事件，例如做autocomplete

算法：
1. check if there's already scheduled task
2. if so, cancel it, reschedule
3. if none, schedule a new one

```javascript
// as long as the event is triggered, it won't invoke the function.
_.debounce = function(func, wait, immediate) {
    var timeout, result;

    return function() {
      var context = this, args = arguments;

      var later = function() {
        timeout = null;
        if (!immediate) {
          result = func.apply(context, args);
        }
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

## How do you make a website faster?

1. css sprite
2. load pictures only when needed
3. load javascript files only when needed - use `<script src="path/to/script" async />`
4. Optimize CSS and JS files. Enable compression: minify front end files, combine multiple front end files into one
5. use CDN
6. check if you put unused code into the page, or JS CSS files.
7. eliminate HTTP requests
8. make images internet-friendly

HTTP/2 may also help. However, be extremely cautions to mention it, because your interviewer may not know about HTTP/2's new feature. Don't get into trouble!

1. use HTTP/2 to have multiple connection. Front end files will be downloaded in parallel.
2. HTTP/2 server push - it allows a web server to send resources to a browser before the browser gets to request them
