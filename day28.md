# Day 28

Today I learned about using the **`inline` layout** for background images in the Hero block.

## Key Points

- `backgroundImageLayout` can be `"fullWidth"` or `"inline"`.
- `"inline"` allows the image to be positioned **independently of the main hero section**, usually at the
  **bottom-right**.
- Useful for adding visual elements like **lawyer photos** without affecting text alignment.
- The Hero component handles it with:
  ```ts
  const isBgInline = backgroundImageLayout === "inline";
  ```

And it works, of course in the future we'd have to add the `position` in Sanity CMS to position the image in whichever
origin we need, but this works well for this use case.
