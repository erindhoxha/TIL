## Day 8

- Learned about Krita studio brushes:
  - Color Smudge Engine
  - Bristle Brush Engine which is like acrylic/oil
  - Pixel Brush Engine which is the most common brush

Unicode sneaks in and ruins assumptions (in a good way)

One of the most eye-opening bits is how JavaScript handles characters:

- Not all “characters” are one byte
- Emojis and accented characters break naïve indexing
- `length` doesn’t always mean “number of visible characters”
