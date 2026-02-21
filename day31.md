## Day 31

Today I learned about **avoiding an uncaught error when clicking "Add New Page" in Sanity CMS**, caused by the
multilingual plugin auto-patching empty string values.

## Context

In Sanity, we have the `languages` plugin configured like this:

```ts
languages: [
  { id: 'en', title: 'English' },
  { id: 'es', title: 'Spanish' },
],
```

The plugin also has a defaultLanguages option. Previously, it was set to:

```ts
defaultLanguages: ['en'],
```

The issue: When adding a new page, the plugin auto-patched new documents with empty string values for the default
language fields. This caused uncaught errors.

### Solution

Set defaultLanguages to an empty array to prevent auto-patching:

```tsx
defaultLanguages: [],
```

Other plugin options remain the same:

```tsx
fieldTypes: ['string', 'blockContent', 'text'],
```

### Benefit

- Prevents uncaught errors when creating new pages.
- Gives more control over how multilingual fields are initialized.
- Avoids unnecessary empty string data in the CMS.
