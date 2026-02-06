## Day 17

I learned that we can add a custom `PortableText` in Sanity, that instead of using the default one from `next-sanity`,
we could create our own marks and "blocks".

Example:

```
import { PortableText as IPortableText, PortableTextComponents } from '@portabletext/react';
import styles from './styles.module.scss';
import { ComponentProps, LinkProps, PortableTextProps } from './types';

const components: Partial<PortableTextComponents> = {
  marks: {
    link: ({ children, value }: LinkProps) => {
      const { href, blank } = value || {};
      return (
        <a
          href={href}
          className={styles.link}
          target={blank ? '_blank' : '_self'}
          rel={blank ? 'noopener noreferrer' : undefined}
        >
          {children}
        </a>
      );
    },
  },
  list: {
    bullet: ({ children }: ComponentProps) => <ul className={styles.listDisc}>{children}</ul>,
    number: ({ children }: ComponentProps) => <ol className={styles.listDecimal}>{children}</ol>,
  },
};

export const PortableText = ({ value }: PortableTextProps) => <IPortableText value={value} components={components} />;
```

We can add more to it, so I made a change in the repo:

```
import { PortableText as IPortableText, PortableTextComponents } from '@portabletext/react';
import styles from './styles.module.scss';
import { ComponentProps, LinkProps, PortableTextProps } from './types';

const components: Partial<PortableTextComponents> = {
  marks: {
    link: ({ children, value }: LinkProps) => {
      const { href, blank } = value || {};
      return (
        <a
          href={href}
          className={styles.link}
          target={blank ? '_blank' : '_self'}
          rel={blank ? 'noopener noreferrer' : undefined}
        >
          {children}
        </a>
      );
    },
    underline: ({ children }: ComponentProps) => <span className={styles.underline}>{children}</span>,
    strong: ({ children }: ComponentProps) => <strong className={styles.strong}>{children}</strong>,
    em: ({ children }: ComponentProps) => <em className={styles.italic}>{children}</em>,
  },
  list: {
    bullet: ({ children }: ComponentProps) => <ul className={styles.listDisc}>{children}</ul>,
    number: ({ children }: ComponentProps) => <ol className={styles.listDecimal}>{children}</ol>,
  },
  block: {
    h1: ({ children }: ComponentProps) => <h1 className={styles.h1}>{children}</h1>,
    h2: ({ children }: ComponentProps) => <h2 className={styles.h2}>{children}</h2>,
    h3: ({ children }: ComponentProps) => <h3 className={styles.h3}>{children}</h3>,
    h4: ({ children }: ComponentProps) => <h4 className={styles.h4}>{children}</h4>,
    h5: ({ children }: ComponentProps) => <h5 className={styles.h5}>{children}</h5>,
    h6: ({ children }: ComponentProps) => <h6 className={styles.h6}>{children}</h6>,
    normal: ({ children }: ComponentProps) => <p className={styles.p}>{children}</p>,
    blockquote: ({ children }: ComponentProps) => <blockquote className={styles.blockquote}>{children}</blockquote>,
  },
};

export const PortableText = ({ value }: PortableTextProps) => (
  <div className={`${styles.portableWrapper} temp-portable-wrapper`}>
    <IPortableText value={value} components={components} />
  </div>
);
```

This way, we can also style these with styles.module file, example:

```
.listDisc {
  list-style-type: disc !important;
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding-left: 1rem;
}

.listDisc li + li {
  margin-top: 8px;
}

.listDecimal {
  list-style-type: decimal !important;
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding-left: 1rem;
}

.listDecimal li + li {
  margin-top: 8px;
}

.link {
  color: #4285f4;
  text-decoration: underline;
}

.h1,
.h2,
.h3,
.h4,
.h5,
.h6,
.p {
  padding: 0;
  margin: 0;
}

.h5 {
  font-weight: 700;
}

.blockquote {
  font-size: 1rem;
  position: relative;
  padding-left: 16px;
}

.italic {
  font-style: italic;
}

.strong {
  font-weight: 600;
}

.blockquote::before {
  left: 0;
  width: 4px;
  height: 100%;
  content: '';
  position: absolute;
  background-color: var(--primary-color, #000);
  border-radius: 2px;
}

.portableWrapper {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.underline {
  text-decoration: underline;
}
```

Also I read about how to integrate Percy "baseline", we can change the baseline of Percy with using `PERCY_BRANCH`: We
can force a specific build to act as the baseline by setting the branch environment variable to our main branch during
the upload: bash

`PERCY_BRANCH="main" npx percy upload ./screenshots`
