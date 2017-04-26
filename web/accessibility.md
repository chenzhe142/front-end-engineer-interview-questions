# accessibility

It means people with disabilities can use the web. In details, they can perceive, navigate and interact with the website.

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

### how to improve

1. Do not make your pages dependent on images
2. Make sure all your images have ALT text. Screen readers cannot "read images". In order for your images meaningful for people with disabilities, you need to add written descriptions for the images.
3. Don't make the font size too small
4. Use highly contrasting colors for your text and background.
5. Screen reader friendly: use proper `aria` label, name and descriptions to navigate users to interact the page.
6. Use semantic markups, and then enhance with ARIA.
7. add labels for form elements
8. make sure you can navigate through a page using keyboard only
9. create meaningful links
10. etc.

To use accessibility API describe an object:

1. role
2. name
3. state

Further readings:
- [w3.org - Introduction to web accessibility](https://www.w3.org/WAI/intro/accessibility.php)
- [w3.org - How people with disabilities use the web](https://www.w3.org/WAI/intro/people-use-web/Overview.html)
- [Smashing magazine - web accessibility with accessibility API](https://www.smashingmagazine.com/2015/03/web-accessibility-with-accessibility-api/)

Online tools for checking your markup:
- [achecker](http://achecker.ca/checker/index.php#output_div)

### - web accessibility: how to make `<a>` tag accessible?

HTML markup:

1. `href` should present
2. `name`
3. `id` if needed
4. `textContent`

1. make the text of `<a>` concise. so that when screen readers read the link, people with disabilities can understand it.
2. don't capitaliz link text. avoid using ASCII charactors, and using URLs as text.
3. restrict numbers of links on a page
4. always alert a user when opening a new tab/window. For example, add a new icon "external-link" so that screen readers can read it to people.
5.  to be continued
