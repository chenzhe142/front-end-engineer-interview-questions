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
  3. Data
    - get data from server
      - what
      - when
      - where
    - send data to server
      - what
      - when
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
