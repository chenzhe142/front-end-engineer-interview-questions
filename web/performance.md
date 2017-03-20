# Dealing with pragmatic issues

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
