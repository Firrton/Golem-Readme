# yagna app-keys

An **app-key** is a bearer token that grants access to your local yagna REST API. Every requestor script authenticates with one. App-keys are local-only by default but **must still be treated as secrets** — anyone who reads one can spend your GLM.

## Create

### Option A: autoconfig at first start (simplest)

```bash
export YAGNA_AUTOCONF_APPKEY=my_requestor
yagna service run
```

If yagna sees this env var on first run, it creates an app-key with that name automatically. Your SDK passes `api.key: "my_requestor"`.

### Option B: explicit create (after yagna is already running)

```bash
yagna app-key create my_requestor
```

Output:

```
e.g.  c3a4f1e8b2... (a long hex token)
```

The token value is what your code uses — `YAGNA_AUTOCONF_APPKEY` lets you alias it via the name, but for explicit creation you'd use the hex value.

## List

```bash
yagna app-key list
```

Shows name, key, identity, role, and `created` timestamp.

## Revoke (always do this after demos)

```bash
yagna app-key drop my_requestor
```

After a public demo or a workshop, drop every app-key you created. They are bearer tokens — if a screenshare captured one, treat it as compromised.

## Pass to the SDK

### JS / TS

```js
import { GolemNetwork } from "@golem-sdk/golem-js";

const glm = new GolemNetwork({
  api: { key: process.env.YAGNA_APPKEY },  // value from `yagna app-key list`
});
```

Or set `YAGNA_APPKEY` in `.env` and load with `dotenv`. Or stick with `YAGNA_AUTOCONF_APPKEY` and the SDK reads it automatically when `api.key` is omitted (depends on SDK version — set explicitly to be safe).

### Python (yapapi)

yapapi typically reads `YAGNA_APPKEY` from the environment. Set it before running your script:

```bash
export YAGNA_APPKEY=$(yagna app-key list --json | jq -r '.[0].key')
python my_script.py
```

## Security rules

1. **Never `cat`, `echo`, or paste an app-key into chat or a screenshare.** If you do, immediately `yagna app-key drop` it.
2. **Never commit `.env`.** Add to `.gitignore`:
   ```
   .env
   .env.*
   *.appkey
   ```
3. **Don't ship browser bundles that contain an app-key.** Browsers cannot safely hold bearer tokens for a backend service. Use a backend proxy. See `references/sdks/react.md`.
4. **Rotate per project.** Use a distinct app-key name per project (`yagna app-key create proj-alpha`) so revoking one doesn't break another.
5. **Drop in CI.** If a CI job creates an app-key, drop it as the last step (even on failure) — use a trap.

## Recovery from a leak

1. `yagna app-key drop <name>` — immediately revoke.
2. `yagna payment status` — check if any unexpected outgoing payments were made.
3. Rotate the underlying identity if the loss is severe: `yagna id create` + `yagna id set --no-default <old-id>`.

Source: https://docs.golem.network/docs/creators/javascript — Last verified: 2026-05-13
