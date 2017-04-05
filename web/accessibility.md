# accessibility

## tab & hover
- how to find tab-focused element - [David Walsh - focused element](https://davidwalsh.name/focused-element)

## use `tabIndex` to enable focusable HTML elements
`tabIndex` is a global attribute responsible for two things:
1. it sets the order of "focusable" elements
2. it makes elements "focusable"

### use case
1. To make your element focusable, use `tabindex="0"`
2. If don't want to make element to be focusable by tab, use `tabIndex="-1"`

### links
- [stack overflow](http://stackoverflow.com/questions/4112289/what-is-the-html-tabindex-attribute)
- [MDN - tabIndex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)
