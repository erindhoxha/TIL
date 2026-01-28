## Day 9

- First drawing in Wacom Intuos M, I'll share the drawing later (or never :P)
- Reading about Visual QA, there are some tools that we can use:
  - Applitools
  - Percy
  - Chromatic

Applitools is more an AI visual QA, which checks any dynamic content and then removes it Percy is great when joined
together with Playwright (or Cypress) which takes a snapshot, sends it to Percy and then makes a visual diff. Chromatic
is used more when you have Storybook installed in your app.

Also there's a cool tool called BrowserStack, which helps to test your app and website.

BrowserStack is a cloud testing platform that lets us test websites and apps on real browsers and real devices, without
having to install or maintain any of them locally.

Think of it as: “open Chrome on an actual iPhone 14 using Safari from your laptop in 10 seconds.”

I'm reading more how to use Percy + BrowserStack and some notes I've written in my Notion document:

**Percy with Browserstack?**

- How it works**:** BrowserStack spins up \***\*real devices and browsers in the cloud**,\*\* Percy then takes snapshots
  of those sessions.
- Pros**:**
  - Tests real devices (iOS, Android, Safari, old Edge)
  - Captures true device/browser layout issues
- Cons**:**
  - Expensive, slower than CI headless browsers
  - Dynamic content masking is harder
- Use case**:** Optional pre-production QA or high-risk campaigns; not needed for daily PR checks.

**Percy with playwright?**

- How it works:
  - Playwright renders hydrated Next.js pages (dynamic CMS content included) locally or in CI
  - Percy takes screenshots of the page at multiple viewports
- Pros:
  - Fast & cheap (CI friendly)
  - Supports masking dynamic content (dates, carousels etc)
  - Multi-viewport snapshots for desktop/tablet/mobile
  - CMS team can review immediately in Percy dashboard
- Cons:
  - Only simulated devices, not real hardware
- Use case: Day-to-day PR-level visual regression
