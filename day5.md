## Day 5

- Learned about Percy, Your all-in-one visual review platform
- We can integrate Percy + Playwright, which connects to the app, then tests "Snapshots" in the UI

Something like:

```
// tests/landingPage.visual.spec.ts
import { test } from '@playwright/test';
import Percy from '@percy/playwright';

// Add Percy snapshot to Playwright test
test('Landing page visual regression', async ({ page }) => {
  // Go to staging landing page
  await page.goto('https://staging.example.com/landing');

  // Optional: wait for dynamic content to load
  await page.waitForTimeout(2000);

  await page.addStyleTag({
    content: `
      .carousel,
      .dynamic-banner,
      .ad-slot,
      .timestamp {
        visibility: hidden !important;
      }
    `
  });

  // Take Percy snapshot
  await Percy.snapshot(page, 'Landing Page', {
    widths: [375, 768, 1280], // mobile, tablet, desktop
    minHeight: 1024,          // ensure full page
  });
});
```

- Tomorrow I'll dive deeper into:
- Challenges: Sliding Window, Recursion
