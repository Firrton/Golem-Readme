# `@golem-sdk/react`

React hooks and provider components wrapping `@golem-sdk/golem-js`. Use it at the UI boundary of an app that needs to expose Golem rentals, tasks, or live execution state to the user.

## When to reach for it

- You're building a frontend (Next.js, Vite, CRA) that has to talk to a local yagna daemon — typically via a backend proxy or Electron-style desktop wrapper.
- You want React-idiomatic state (loading, error, results) instead of raw SDK calls in `useEffect`.

For pure backend / CLI requestor scripts: don't use this — `task-executor` or `golem-js` is simpler.

## Install

```bash
npm install @golem-sdk/react @golem-sdk/golem-js
```

## Provider setup

Wrap your app tree with `GolemProvider`:

```jsx
import { GolemProvider } from "@golem-sdk/react";

export default function App({ children }) {
  return (
    <GolemProvider
      config={{
        api: { key: process.env.NEXT_PUBLIC_YAGNA_APPKEY },
        // browser-safe configs only — never inline mainnet keys
      }}
    >
      {children}
    </GolemProvider>
  );
}
```

## Typical hooks

```jsx
import { useGolem, useTask } from "@golem-sdk/react";

function MyComponent() {
  const { connected, error } = useGolem();
  const { run, isRunning, result } = useTask({
    order: { /* same shape as golem-js */ },
  });

  return (
    <button onClick={() => run(async (exe) => exe.run("uname -a"))}>
      {isRunning ? "Running..." : "Run on Golem"}
    </button>
  );
}
```

> **Note**: exact hook names and signatures evolve. Verify against the package's current `README.md` at https://github.com/golemfactory/golem-js (the `react` workspace) before relying on a specific symbol.

## Browser caveat (critical)

Yagna's REST API is **local-only** by default (binds 127.0.0.1). A pure-browser SPA cannot talk to it directly across the network. Realistic deployment options:

1. **Electron / Tauri desktop app** — the renderer is local-host-effective.
2. **Backend proxy** — Next.js API route / Express server runs on the same host as yagna and proxies signed requests.
3. **Local dev only** — fine for prototypes via `localhost` CORS overrides.

Never ship a public web app that exposes raw `YAGNA_APPKEY` to the browser bundle.

## SSR & hydration (Next.js)

- All Golem hooks must run client-side. Wrap consumers in `"use client"` (App Router) or `dynamic(() => ..., { ssr: false })` (Pages Router).
- The `yagna` connection state is per-tab — there's no shared singleton across SSR + client.

Source: https://github.com/golemfactory/golem-js (react workspace) — Last verified: 2026-05-13
