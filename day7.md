## Day 7

- Learned more about namespacing in CSS (modules or just an .scss file)
- I learned that it's useful to get some of the bootstrap CSS, not all of them

For example, in a `LandingPage` file, we set:

```
 <main className="main-legacy">
```

Then in the SCSS (or CSS):

```
:root {
 --white: #ffffff;
 --cta-bg: var(--primary-color, #18ce0f);
 --cta-bg-hover: var(--primary-color, #15b60d);
 --chat-cta-bg: var(--primary-color, #f1880f);
 --chat-cta-bg-hover: #8aa8b0;
}

.main-legacy {
 @import 'bootstrap/scss/bootstrap-utilities';
 @import 'bootstrap/scss/bootstrap-grid';
 @import './partials/colors';
 @import './partials/buttons';
 @import './partials/layout';
 @import './partials/footer';
 @import './partials/navbar';
 @import './partials/form';
 @import './partials/header';
 @import './partials/livechat';
 @import './partials/practice-areas';
 @import './partials/cta';
 @import './partials/whychooseourlaywers';
 @import './partials/steps-header';
 @import './partials/steps-section';
 @import './partials/injury-lawyers';
 @import './partials/side-livechat';
 @import './partials/general';
 @import './partials/testimonials';
 @import './fontawesome';
 @import './partials/typography';

 color: #2c2c2c;
 font-size: 14px;
 font-family: 'Montserrat', 'Helvetica Neue', Arial, sans-serif;
 -moz-osx-font-smoothing: grayscale;
 -webkit-font-smoothing: antialiased;
 margin: 0;
 font-weight: 400;
 line-height: 1.5;
 color: #212529;
 text-align: left;
 background-color: #fff;
}

.grecaptcha-badge {
 display: none !important;
}
```

This makes sure, that the SCSS file is running only under `main-legacy` which renders the css such as:

`.main-legacy h1 { ... }` etc.

- Also I learned more about the Wacom tablet, and there's a free software called Krita, which allows to learn more about
  digital drawing.

https://krita.org/en/

It seems it's a great tool to get started.
