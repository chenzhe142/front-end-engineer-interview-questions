# use JavaScript in HTML

## the `<script>` element
There are 6 attributes for the `<script>` element:

1. `async`: the script should begin downloading immediately, but should not prevent other actions on the page. valid only for external script files.
  - HTML5 introduces `async`
  - `async` does not guarantee that scripts will be executed in order.

2. `charset`: this attribute is rarely used, because most browsers don't honor its value.
3. `defer`: the script will be loaded after the page has been completely parsed and displayed.
  - the script will start downloading after the browser has received the closing `</html>` tag.
  - the HTML5 specification indicates that scripts will be executed **in the order** in which they appear.
  - `defer` attribute may not be fully supported by all browsers. Because of this, it's still best to put deferred scripts at the bottom of the page.
4. `language`: deprecated. do not use.
5. `src`
6. `type`: indicates the content type (also MIME type). this value is safe to omit, as "text/javascript" is assumed when missing.

## the `<noscript>` element
`<noscript>`使得不支持javascript的浏览器可以平稳退化，用以显示替代内容。包含在`<noscript>`元素中的内容只有在下列情况下才会显示出来：
1. 浏览器不支持javascript
2. 浏览器支持javascript，但被禁用

## notes

- as with inline javascript code, processing of the page is halted while the external file is interpreted.
- always use `<script src="source.js"></script>` with open and close tag. It's not legal to have self-closing tag `<script />` in HTML.
- browsers don't check the file extension of included JavaScript files. This leave open the possibility of dynamically generating JavaScript code using JSP or other server-side scripting language. If you don't use a `.js` extension, make sure that your server is returning the correct MIME type.
- `<script>` allows to include JavaScript files from outside domains. Make sure you know where the code comes from.
- put `<script>` at the end of `<body>` tag.
  - rendering begins when the browser receives the opening `<body>` tag
  - it won't block the page rendering. The page is completely rendered in the browser before the javascript code is processed.
