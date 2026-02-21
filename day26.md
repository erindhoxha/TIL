## Day 26

Shipped a large cleanup + standardization of our Sanity WYSIWYG rendering.

## Centralized PortableText Rendering

- Replaced `next-sanity` usage across blocks with our own `PortableText` wrapper.
- Moved all styling + structure into a single reusable component.
- Added support for:
  - Headings (H1–H6)
  - Paragraphs
  - Blockquotes
  - Caption
  - Bullet & numbered lists
  - Strong / Em / Underline
  - Links

Now all blocks (Carousel, Grid, FiftyFifty, Text, etc.) use the same rendering logic.

---

## Global Typography Consistency

- Standardized heading weights (e.g. H1/H5 → 700).
- Unified responsive font mixins.
- Removed duplicated typography logic from individual blocks.
- Deleted old block-level WYSIWYG styles and moved everything into the global PortableText styles.

---

## Improved List Handling

- Rebuilt bullet + numbered lists with custom markers.
- Ensured proper alignment and spacing.
- Added support for headings inside list items.
- Applied consistent responsive typography inside `li`.

---

## Sanity Schema Updates

- Cleaned up duplicate styles.
- Added explicit support for:
  - `H1–H6`
  - `blockquote`
  - `caption`
  - `underline`

---

## Testing Updates

- Updated tests to mock our new `PortableText` wrapper.
- Ensured template variable rendering still works correctly.

---

## Takeaway

Centralizing WYSIWYG rendering:

- Removes duplication
- Prevents styling drift between blocks
- Makes global typography changes predictable
- Gives us full control over Sanity output rendering
