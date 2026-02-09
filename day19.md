## Day 19

Today I learned about the distinction between **`marks`** and **`blocks`** in WYSIWYG editors like Sanity's Portable
Text, and why it’s important when rendering rich text in React.

In Portable Text:

- **Marks** are **inline formatting** applied to text segments.  
  They affect only part of a block, like a single word or phrase. Examples include:
  - `strong` → bold text
  - `em` → italic
  - `underline` → underlined text
  - `strike` → strikethrough
  - `code` → inline code snippet
  - `link` → clickable anchor tags

- **Blocks** are structural elements that define the layout of content. They wrap multiple inline marks or plain text.
  Examples include:
  - `Headings`: h1–h6
  - `Paragraphs`: normal
  - `Blockquotes`: blockquote
  - `Code blocks`: code

- **Lists** are a special kind of block that can be nested and can have custom styles:
  - `bullet` → unordered lists (`<ul>`)
  - `number` → ordered lists (`<ol>`)

Example:

```
import { PortableText as IPortableText, PortableTextComponents } from '@portabletext/react';
import styles from './styles.module.scss';
import { ComponentProps, LinkProps, PortableTextProps } from './types';
import { renderBlockContent } from '@/app/utils/renderContent';

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
    strike: ({ children }: ComponentProps) => <span className={styles.strike}>{children}</span>,
    code: ({ children }: ComponentProps) => <code className={styles.code}>{children}</code>,
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
    code: ({ children }: ComponentProps) => <pre className={styles.code}><code>{children}</code></pre>,
  },
};

export const PortableText = ({ value = [], templateVars }: PortableTextProps) => (
  <div className={`${styles.portableWrapper} temp-portable-wrapper`}>
    <IPortableText value={templateVars ? renderBlockContent(value, templateVars) : value} components={components} />
  </div>
);
```

Marks can be `link`, `underline`, `em`, `strong`, `strike`, `code`. Blocks can be `h1`–`h6`, `normal`, `blockquote`,
`code`. Lists can be `bullet`, `number`, or any custom style defined in the schema.
