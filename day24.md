## Day 24

- Learned more about gsap, I'm looking to build something with: https://www.youtube.com/watch?v=AW1yfBKRMKc
- Adding gap between items in WYSIWYG works! You can add a gap: 16px; and every paragraph, heading etc. will have that
  gap. I used to overthink this.
- Also learned that there's a package for gsap and React, I used to think that gsap is only for vanilla projects.

"An abstract data type is realized by writing a special kind of program which defines the type in terms of the
operations which can be performed on it." Barbara Liskov, Programming with Abstract Data Types

From the Eloquent Javascript

Here’s a simple example of animating a box when the component mounts:

```tsx
import React, { useEffect, useRef } from "react";
import { gsap } from "gsap";

const AnimatedBox: React.FC = () => {
  const boxRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    if (boxRef.current) {
      gsap.from(boxRef.current, { opacity: 0, x: -100, duration: 1, ease: "power2.out" });
    }
  }, []);

  return (
    <div
      ref={boxRef}
      style={{
        width: "150px",
        height: "150px",
        backgroundColor: "#4f46e5",
        display: "flex",
        alignItems: "center",
        justifyContent: "center",
        color: "white",
        fontWeight: "bold",
        borderRadius: "8px",
      }}>
      Hello GSAP
    </div>
  );
};

export default AnimatedBox;
```

What’s happening:

The useRef hook captures the DOM element. gsap.from animates it from opacity: `0` and `x: -100` to its natural position
and opacity over 1 second. You can easily expand this with scroll triggers, staggered animations, and more complex
timelines.
