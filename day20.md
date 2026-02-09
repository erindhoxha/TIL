## Day 20

- If you create an item in Webflow collection when you're on a translation mode, for example `es` for Spanish, then it
  won't be created in the English `en` version. This way, when you try to create an item in `en` with the same slug or
  any unique field, it will say that the name has been taken.

I find it interesting that we can create new Sanity items through:

```
  const sanityCampaign = await sanityClient.create({
    _type: TYPE,
    _id: `drafts.${uuid()}`,
    ...field,
  });
```

- Learned about Codex, a tool that you can vibe code with. Pretty cool and it seems great for small projects.

https://openai.com/codex/
