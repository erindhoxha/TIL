## Day 30

Today I learned about **adding optional borders to sections** instead of having a fixed `border-bottom` for every
section.

## Context

Previously, every section had a CSS rule like:

```scss
.section:not(:last-of-type) .section__inner {
  border-bottom: 1px solid $secondary-30;
}
```

This automatically added a border to all sections except the last one.

The issue: sometimes a section shouldn’t have a border, but this rule applied to all of them.

Solution Approach

- Make the border-bottom a configurable option in the section block inside Sanity Studio.
- Content editors can then toggle showBorderBottom for each section.
- The SCSS can then conditionally apply the border:

```
.section__inner {
  border-bottom: 1px solid $secondary-30;

  &.no-border {
    border-bottom: none;
  }
}
```

In the React component, add a class based on the block’s field from Sanity:

```
<div className={mergeClasses(styles.section__inner, !block.showBorderBottom && 'no-border')}>
  ...
</div>
```

Benefit

- Provides flexibility to content editors.
- Avoids hardcoding UI decisions in CSS.
- Keeps the design consistent and configurable per section.
