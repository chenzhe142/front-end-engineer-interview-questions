# my approach for a front-end design task

## requirements
  1. UI design
  2. User experience
    - what's the user scenario?
      - different states?
      - loading, error, normal, alert error
    - where it is used by a web page?
  3. User behavior & interaction
    - what are we expected for user to use the widget?
    - accessibility
      - use `aria-label`, `role`, `alt`, `for`
  3. Data
    - get data from server
      - what
        - ajax
        - streaming, websocket
      - when
        - initial load, lazy load
      - where
    - send data to server
      - what
        - validate & serialize formData
      - when
        - could be clicking event
      - where
  4. platform
    - desktop
    - mobile
    - responsive
  5. priority on the page
    - server-side rendering
    - client-side rendering

## approach
  1. decide a design pattern
    - MVC
      - Controller:
        - 在初始化时，构造相应的 View 和 Model。
        - 监听 Model 层的事件，将 Model 层的数据传递到 View 层。
        - 监听 View 层的事件，并且将 View 层的事件转发到 Model 层。
      - View: HTML & CSS
      - Model: stores business logic
      - Emitter
        - link `View` and  `Model`
        - `View`'render method can subscribe to `Model`'s update or change event
  2. design methods
  3. think about code reuse & maintainability

## 附录
1. [Model-View-Controller MVC in JavaScript](https://alexatnet.com/articles/model-view-controller-mvc-javascript)
2. [被误解的MVC和被神化的MVVM](http://www.infoq.com/cn/articles/rethinking-mvc-mvvm)
