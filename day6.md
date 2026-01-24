## Day 6

- Learned that we can set dynamic datasets in Next.js with Sanity
- Learned that we cannot use `js-cookie` library in SSR

Also, when we want to initialise a state/data in Frontend, we'd need to initialise with `useEffect` if the state can
come from SSR. Example:

```
  useEffect(() => {
    const initialDataset = (Cookies.get(DATASET) as Dataset) || APP_ENVIRONMENTS.STAGING;
    setDataset(initialDataset);
  }, []);Expand comment
```

If we don't do this, we'll get a hydration warning, which says that the data from SSR and FE is not similar, which will
cause hydration issues.

Also, I learned about `imageUrlBuilder` from `@sanity/image-url`, this is used to build the images that come from the
Sanity's CDN.

Example:

```
export async function urlFor(source?: SanityImageSource) {
  if (!source) {
    return null;
  }
  const dataset = await getServerDataset();
  const client = getSanityClient(dataset);
  const builder = imageUrlBuilder(client);
  return builder.image(source).auto('format');
}
```

In this scenario, I'm using a dynamic dataset that is set from a `DatasetToggle` component, which basically adds a
cookie `dataset` to `staging` or `production` and then it uses the correct dataset to grab the right image.
