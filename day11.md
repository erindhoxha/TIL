## Day 11

I made a documentation about QA Tooling Evaluation & Recommendation

# QA Tooling Evaluation & Recommendation

## Integrating Lighthouse CI

Lighthouse doesn’t care how the page is built, React, Next, Sanity, or any stack.

- Track the score
- Fail on significant regressions

**Effort**:

Initial setup (1 day)

**Recommendation if we start here:**

1. Add Lighthouse CI in non-blocking mode
2. Run it on 1–2 staging campaign URLs
3. Decide thresholds later

First we run `yarn add -D @lhci/cli`

Example config, the file name would be called for example: `lighthouserc.json`

```tsx
{
  "ci": {
    "collect": {
      "numberOfRuns": 3,
      "url": [
        "https://staging.socarolinainjuryfirm.com/animal-bite"
      ],
      "settings": {
        "preset": "desktop",
        "chromeFlags": "--no-sandbox --disable-dev-shm-usage"
      }
    },
    "assert": {
      "assertions": {
        "performance": ["warn", { "minScore": 0.75 }],
        "accessibility": ["warn", { "minScore": 0.85 }],
        "best-practices": ["warn", { "minScore": 0.85 }],
        "seo": ["warn", { "minScore": 0.85 }]
      }
    },
    "upload": {
      "target": "temporary-public-storage"
    }
  }
}
```

Then, we run `npx lhci autorun` after `deploy-to-staging`

That would be literally it, then:

Lighthouse will:

- Run audits
- Print results in CI logs
- Upload a report link we can click

We could use other tools such as **WebPageTest, k6, Pa11y / axe-core (this is more accessibility)**, but Lighthouse CI
is a solid choice as well and the setup should be the same/similar.

---

### Visual Regression Testing

Visual regression testing to detect any UI changes by comparing screenshots between builds.

Tools:

- **Percy**
- **Applitools**
- **Chromatic**

Setup I recommend: Playwright + Percy

| Factor              | Playwright + Percy                                    | BrowserStack + Percy                                           |
| ------------------- | ----------------------------------------------------- | -------------------------------------------------------------- |
| Snapshot accuracy   | ✅ Full hydrated page                                 | ✅ Full page on real devices                                   |
| Multi-device review | ⚠️ Only simulated viewports (desktop, tablet, mobile) | ✅ Real device browsers (iOS Safari, Android Chrome)           |
| Cost                | ✅ Low                                                | ❌ High                                                        |
| CI speed            | ✅ Fast                                               | ⚠️ Slower                                                      |
| Marketing access    | ✅ Percy dashboard easy                               | ✅ Percy dashboard still works, but slower snapshot generation |
| PR-level feedback   | ✅ Yes                                                | ✅ Yes, but slower                                             |

**Percy with Browserstack?**

- How it works: BrowserStack spins up real devices and browsers in the cloud, Percy then takes snapshots of those
  sessions.
- Pros:
  - Tests real devices (iOS, Android, Safari, old Edge)
  - Captures true device/browser layout issues
- Cons:
  - Expensive, slower than CI headless browsers
  - Dynamic content masking is harder
- Use case: Optional pre-production QA or high-risk campaigns; not needed for daily PR checks.

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

**How will the marketing/CMS team review?**

- Marketing logs in to Percy dashboard:
  - See side-by-side comparisons of baseline vs current build
  - Toggle overlay to highlight differences
  - Approve or decline each snapshot
- Approve: baseline updated for future comparisons
- Decline: developer fixes the issue → new snapshot uploaded → Slack alerts marketing again

**How it’ll look like?**

- In CI: Playwright + Percy runs → snapshots uploaded → Slack alerts
- Percy dashboard:

  ```
  Baselinesnapshot |Newsnapshot | Pixel diff highlighted

  ```

  - Marketing sees red highlights for removed/changed elements, green for new elements
  - Multi-viewport tabs: Desktop / Tablet / Mobile

### BrowserStack

- BrowserStack is a cloud-based cross-browser testing platform.
- It lets you run your site or tests on real devices and browsers (desktop, mobile, iOS, Android) without owning the
  hardware.

**How it would look like:**

Our Next.js page → BrowserStack (real browser) → Percy (visual diff)

---

**My recommendation:**

- Step 1: Push changes to staging
- Step 2: Percy snapshots run automatically
  - Playwright navigates pages and uploads screenshots to Percy
- Step 3: Slack notification sent to a CMS notifications channel
  ```
  Visual changes detected on branch `API-{{branch_name}}
  Pages affected: staging.injuryfirmstl.com, staing.socarolinainjuryfirm.com
  Snapshots changed:3
  Review here: https://percy.io/lawfty/legacy/builds/1
  ```
- Step 4: Marketing reviews visual differences in Percy dashboard
  - Side by side comparison of baseline vs current build
  - Approve if layout looks correct (Marketing or the CMS team)
  - Decline if there’s a layout shift or visual regression
- Step 5: Developer fixes issues (if declined)
  - Pushes fixes → CI reruns Percy snapshots → Slack notifies marketing of updates.
- Step 6: PR merge
  - PR merges only when all required CI checks pass
  - Percy approvals do NOT merge or deploy, they only update the baseline for visual comparisons

TLDR;

Step 1: PR deploys to staging Step 2: Playwright uploads visuals to Percy Step 3: Slack notification Step 4: Marketing
review (in Percy) Step 5: Developer fixes issue Step 6: PR merge

## Smoke E2E Tests

We can use Playwright to cover critical flows. Visual regression snapshots can be integrated into these same tests. For
example, show if the website has a carousel etc.

Example of both tests at the same time:

```tsx
import { test, expect } from "@playwright/test";
import percySnapshot from "@percy/playwright";

test.describe("Smoke E2E - critical flows", () => {
  const stagingUrls = [
    "https://staging.socarolinainjuryfirm.com/animal-bite",
    "https://staging.socarolinainjuryfirm.com/car-accident",
  ];

  stagingUrls.forEach((url) => {
    test(`Page loads correctly: ${url}`, async ({ page }) => {
      await page.goto(url);

      await expect(page).toHaveTitle(/Injury|Law|Firm/); // generic title check
      await expect(page.locator("header")).toBeVisible();
      await expect(page.locator("footer")).toBeVisible();

      const contactForm = page.locator("form#contact");
      if ((await contactForm.count()) > 0) {
        await contactForm.locator('input[name="name"]').fill("John Doe");
        await contactForm.locator('input[name="email"]').fill("john@example.com");
        await contactForm.locator('textarea[name="message"]').fill("Hello from smoke test");
        await contactForm.locator('button[type="submit"]').click();

        await expect(page.locator(".success-message")).toBeVisible();
      }

      await percySnapshot(page, `Smoke Test Snapshot - ${url}`, {
        widths: [375, 768, 1280],
      });
    });
  });
});
```

## Cost

| Option                          | Cost      | Onboarding                                                  |
| ------------------------------- | --------- | ----------------------------------------------------------- |
| **Percy + Playwright (CI)**     | ✅ Low    | ✅ Easy (browser-based dashboard, no local dev needed)      |
| **Percy + BrowserStack**        | ❌ High   | ⚠️ Medium (marketing can still review in Percy, but slower) |
| **Chromatic (Storybook)**       | ⚠️ Medium | ✅ Easy for component-level snapshots                       |
| **Playwright only**             | ✅ Low    | ⚠️ Dev-only (marketing can’t review visuals easily)         |
| **WebPageTest / Lighthouse CI** | ✅ Low    | ✅ Easy                                                     |

We can also add the CI check here:

https://www.browserstack.com/docs/percy/source-code-integrations/github?_gl=1*1dz0ykk*_gcl_au*MjAxMDM0Nzg1LjE3NjkwOTAxNDc.#next-step
