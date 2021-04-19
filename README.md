
# Svelte / Supabase 'payload is undefined' error

This repository demonstrated a minimal example of a `payload is undefined` error which occurs when trying to create a Supabase / Realtime subscription in a SvelteKit app.

## Reproducing the error

In order to use it:

1. Clone repo and run `npm install`.

2. add a `.env` file to the root of your clone with the following environment variables:

```bash
VITE_SUPABASE_URL="https://<your-id>.supabase.co"
VITE_SUPABASE_KEY="<your-key>"
```

3. Add a table called `items` to your Supabase with some test data.

4. Run `npm run dev` and browse to `localhost:3000` with the browser console open.

The full error, shown below, is produced in the browser console when starting the dev server with `npm run dev`; it does *not* occur when refreshing the page.

## Detailed error

```
Uncaught TypeError: payload is undefined
    trigger RealtimeSubscription.ts:186
    trigger RealtimeSubscription.ts:183
    _triggerChanError RealtimeClient.ts:342
    _triggerChanError RealtimeClient.ts:341
    _onConnClose RealtimeClient.ts:328
    onclose RealtimeClient.ts:128
    connect RealtimeClient.ts:128
    on SupabaseQueryBuilder.ts:40
    instance Test.svelte:191
    init index.mjs:1474
    Test Test.svelte:246
    createProxiedComponent svelte-hooks.js:245
    ProxyComponent proxy.js:240
    Proxy<Test> proxy.js:340
    create_fragment index.svelte:23
    init index.mjs:1489
    Routes index.svelte:78
    createProxiedComponent svelte-hooks.js:245
    ProxyComponent proxy.js:240
    Proxy<Index> proxy.js:340
    create_if_block_2 root.svelte:62
    create_default_slot root.svelte:37
    create_slot index.mjs:61
    create_fragment layout.svelte:19
    init index.mjs:1489
    Layout layout.svelte:86
    createProxiedComponent svelte-hooks.js:245
    ProxyComponent proxy.js:240
    Proxy<Layout> proxy.js:340
    create_fragment root.svelte:507
    init index.mjs:1489
    Root root.svelte:695
    createProxiedComponent svelte-hooks.js:245
    ProxyComponent proxy.js:240
    Proxy<Root> proxy.js:340
    _init start.js:593
    start start.js:496
    start start.js:1018
    <anonymous> (index):15
RealtimeSubscription.ts:186:10
```