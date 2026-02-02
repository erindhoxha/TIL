## Day 15

How anchor links with #id work across pages

When clicking a link like:

```
<a href="another_page.html#hello">Click here</a>
```

The browser navigates to `another_page.html,` then looks for an element with `id="hello"`. If the element exists, the
page automatically scrolls to it. If it doesn’t, the page still loads normally with no error.

This behavior is built into the browser, requires no JavaScript, and works with any element type, not just `<div>`.
