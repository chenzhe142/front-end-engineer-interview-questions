# rendering

## server-side rendering: When the browser fetches the page over HTTP, it immediately gets back HTML describing the page.

### good
1. The content is visible to search engine like Google
2. The page loads faster (relatively, may effect t_done). There's no "white page" while the browser downloads the rendering code and data and the runs the code.
3. It maintains the idea that pages are documents.
4. performance is predictable.

### bad

## client-side rendering: JavaScript running in the browser produces HTML or manipulates the DOM.

### goood
1. can update the screen instantly when event occurs - no need to call & wait for server's response to re-render & update the page
2. improve performance - when you get enough resources, i.e., web pages & templates, no need to call server and fetch pages again.

### bad
1. Loading spinner - people need to wait till they get the data
2. unpredictable performance - heavily relied on what devices people use.
