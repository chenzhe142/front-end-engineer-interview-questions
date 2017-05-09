# web疑难杂症

## unexpected spacing between `inline-block` elements
article: [CSS Tricks - fighting space between inline elements](https://css-tricks.com/fighting-the-space-between-inline-block-elements/)
if you have the following HTML:
```html
<span>
  <a>link1</a>
  <a>link2</a>
  <a>link3</a>
</span>
```
There will be spacing between each link.
原因：因`<a>`是`inline element`，每个tag间的换行被看作是一个空格，于是最终render的结果出现了空格
