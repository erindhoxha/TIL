## Day 12

Read more about Crypto trading and trying to refresh my memory on this. Just started watching this video:
https://www.youtube.com/watch?v=UYnCQEHx7ZU

Also started trading a bit on Binance, trading with BTC/USD / 2x, also just refreshing with how to stop/loss and do
limits.

WIP - More incoming

## Day 12

Learned more about AI Assist. We can also set singular field actions.

To set `AI Assist` from Sanity to a field, we'd need to set it in options example:

```
 options: {
   aiAssist: {
     translateAction: true,
   },
 }
```

Also, there's a challenge. If we use Translation plugin with `internationalizedStringArray` values, then the AI Assist
works on the whole block e.g. (Input `en` and Input `es`), but what about a single input, just Input `es` for example?

Then we can set an action to those inputs, which we could translate these manually. How it works is, adding this in the
`sanity.config.ts` file:

```
    fieldActions: {
      title: 'Translate Actions',
      useFieldActions: (props) => {
        const { actionType, schemaId, documentIdForAction, path, getConditionalPaths } = props;
        const client = useClient({ apiVersion: process.env.NEXT_SANITY_API_VERSION || 'vX' });

        return useMemo(() => {
          if (actionType !== 'field') return [];

          return [
            defineAssistFieldAction({
              title: 'Translate to Spanish',
              onAction: async () => {
                await client.agent.action.transform({
                  schemaId,
                  documentId: documentIdForAction,
                  instruction: 'Translate this text to Spanish',
                  instructionParams: {
                    field: { type: 'field', path },
                  },
                  target: path.length ? { path } : undefined,
                  conditionalPaths: { paths: getConditionalPaths() },
                });
              },
            }),
            defineAssistFieldAction({
              title: 'Translate to English',
              onAction: async () => {
                await client.agent.action.transform({
                  schemaId,
                  documentId: documentIdForAction,
                  instruction: 'Translate this text to English',
                  instructionParams: {
                    field: { type: 'field', path },
                  },
                  target: path.length ? { path } : undefined,
                  conditionalPaths: { paths: getConditionalPaths() },
                });
              },
            }),
          ];
        }, [actionType, schemaId, documentIdForAction, path, getConditionalPaths, client]);
      },
    }
```
