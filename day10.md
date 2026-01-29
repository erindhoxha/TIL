## Day 10

- I've created a demo showing of how Percy + Playwright works.

Made a simple config with Playwright:

```
import { defineConfig, devices } from '@playwright/test';

// eslint-disable-next-line import/no-default-export
export default defineConfig({
  testDir: './tests',
  timeout: 30_000,
  expect: {
    timeout: 5000,
  },
  fullyParallel: true,
  reporter: [['list'], ['html']], // HTML report in "playwright-report"
  use: {
    headless: true,
    viewport: { width: 1280, height: 720 },
    ignoreHTTPSErrors: true,
    screenshot: 'only-on-failure',
    video: 'retain-on-failure',
  },
  projects: [
    { name: 'chromium', use: { ...devices['Desktop Chrome'] } },
    { name: 'firefox', use: { ...devices['Desktop Firefox'] } },
    { name: 'webkit', use: { ...devices['Desktop Safari'] } },
  ],
});
```

Then generated a simple file called `snapshot.mjs`:

```
import { chromium } from 'playwright';
import percySnapshot from '@percy/playwright';

(async () => {
  const browser = await chromium.launch({ headless: true });

  try {
    const page = await browser.newPage();

    await page.goto('https://staging.socarolinainjuryfirm.com/', { waitUntil: 'networkidle' });

    await percySnapshot(page, 'Example Site');

    await page.close();
  } catch (err) {
    console.error('Error in Percy snapshot:', err);
  } finally {
    await browser.close();
  }
})();
```

What happens is, when we run:

`npx percy exec -- node tests/snapshot.mjs`

It sends the screenshot to Percy, then we can make a visual diff with the "baseline", it checks pixel by pixel and then
finds the % of the differences, then we can either accept or reject the build, resulting in better visual QA-ing.
