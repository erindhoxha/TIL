## Day 25

Today I shipped UX improvements to our DatePicker / TimePicker in Lawfty.

## Clear & Apply buttons

- Added explicit **Clear** and **Apply** actions.
- Date updates immediately on selection.
- **Apply** only closes the popover.
- **Clear** resets the value.
- Added RTL + Vitest tests to cover this behavior.

## `resetOnOpen` prop

```ts
resetOnOpen?: boolean;
```

- Recomputes the default date when the popover opens.
- Prevents stale quarter-hour defaults (e.g. `getNextQuarterInET()`).
- Useful when validation errors require recalculating the next valid time.

## Layout tweaks

- Improved footer spacing.
- Refactored `TimePicker` layout for proper full-width alignment.
- Made `TimePeriodSelect` responsive (`w-full`).

## Takeaway

Small UX + state handling improvements can prevent subtle time-related bugs and make date selection more predictable.
