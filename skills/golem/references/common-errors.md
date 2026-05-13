# Common errors — symptom → cause → fix

A field guide for the errors a Golem requestor app hits most often. Each entry: what you see, what's actually happening, what to do.

## Yagna daemon issues

### `Error: connect ECONNREFUSED 127.0.0.1:7465`

**Cause**: yagna daemon is not running, or the REST API port (default `7465`) is bound by something else.

**Fix**:
1. Open a terminal and run `yagna service run`.
2. Verify with `yagna --version` and `yagna id show`.
3. If port conflict: `lsof -i :7465` to find the conflicting process.

### `Error: app-key not found` / `401 Unauthorized`

**Cause**: SDK is passing an `api.key` that doesn't match any active yagna app-key.

**Fix**:
1. `yagna app-key list` — what keys exist?
2. Pass the actual hex value or set `YAGNA_AUTOCONF_APPKEY=<name>` BEFORE `yagna service run` to autocreate.

### `Yagna version mismatch`

**Cause**: `@golem-sdk/golem-js` (or `task-executor`) is newer than your yagna build, or vice versa.

**Fix**: Re-run the install one-liner:
```bash
curl -sSf https://join.golem.network/as-requestor | bash -
```
Then restart yagna.

## Market / providers

### `No providers found` (or zero offers received)

**Cause**: usually one of:
- Pricing ceilings too low — Providers won't bid.
- `imageTag` doesn't resolve in the Registry.
- Network mismatch: you set `payment: { network: "polygon" }` but only have hoodi providers.
- Low Provider density on the chosen testnet.

**Fix**:
1. Confirm the image: `imageTag` exists, hash matches.
2. Raise pricing ceilings slightly:
   ```js
   maxStartPrice: 0.5, maxCpuPerHourPrice: 1.0, maxEnvPerHourPrice: 0.5
   ```
3. Check the network matches: `yagna payment status --network=<x>`.
4. If on hoodi: providers are sparser than mainnet — try sepolia or wait.

### `Agreement rejected by provider`

**Cause**: Provider crashed, network instability, or it accepted a competing offer faster.

**Fix**: usually transient. `TaskExecutor` retries automatically. If you're using `golem-js` directly, wrap in a retry loop or use `pool.withRental` (auto-retries pool acquisition).

## Payments / allocations

### `Insufficient allocation` / `Cannot create allocation`

**Cause**: not enough GLM/tGLM in the wallet for the requested rent × pricing × pool.

**Fix**:
- Testnet: `yagna payment fund` again.
- Mainnet: send more GLM to `yagna id show` address, or lower order ceilings.

### `Payment platform not initialized`

**Cause**: you're using `--network=polygon` but never ran `yagna payment fund --network=polygon`.

**Fix**:
```bash
yagna payment fund --network=polygon
```

### Wallet balance shows tokens but allocation fails

**Cause**: GLM is on a different network than the order's `payment.network`. E.g. you have hoodi tGLM but the order says polygon.

**Fix**: align the order's `payment.network` with where your tokens live, or fund the other side.

## Image / .gvmi issues

### `Image hash not found in Registry`

**Cause**: image was never pushed, or you typoed the hash/tag.

**Fix**:
1. `gvmkit-build <name> --push` (re-push).
2. Browse https://registry.golem.network to confirm the tag/hash exists.

### `Image too large / Provider rejected`

**Cause**: `.gvmi` over a Provider-imposed size threshold (usually a few hundred MB).

**Fix**: trim the Dockerfile (multi-stage builds, slimmer base, `--no-cache` on package managers, drop dev deps).

### `Activity failed to start` after agreement signs

**Cause**: image incompatible with the Provider's environment, or a `CMD` / `ENTRYPOINT` that doesn't exist.

**Fix**: test the image locally with `docker run` first. The first command run by the SDK must be invocable inside the image.

## SDK / runtime

### `SyntaxError: Cannot use import statement outside a module`

**Cause**: Node.js running the file as CommonJS but the script uses `import` syntax.

**Fix**:
- Save as `requestor.mjs` (auto-treated as ESM).
- OR add `"type": "module"` to `package.json`.

### `TypeError: glm.disconnect is not a function` (or similar shape errors)

**Cause**: mixing major versions of `@golem-sdk/*` packages. golem-js 2.x and 3.x have different shapes.

**Fix**:
```bash
npm ls @golem-sdk/golem-js
```
Pin all `@golem-sdk/*` to compatible majors. The 3.x line is current.

### `Process exits before shutdown completes`

**Cause**: `await glm.disconnect()` or `executor.shutdown()` missing in a `finally` — a rejection or `Ctrl-C` skips cleanup.

**Fix**: always:
```js
try { /* work */ } finally { await glm.disconnect(); }
```
And handle `SIGINT`:
```js
process.on("SIGINT", async () => { await glm.disconnect(); process.exit(0); });
```

## Network / firewall

### `Connection timeout to relay servers` / `Net status: not connected`

**Cause**: outbound P2P blocked by a firewall (corporate / hotel / VPN).

**Fix**: switch network, use a personal hotspot for testing, or get IT to allow outbound TCP/UDP. There's no fixed allow-list — yagna talks to a dynamic relay mesh.

## When in doubt

1. `yagna service run` is running? `yagna --version` and `yagna id show` both work?
2. Tail `~/.local/share/yagna/yagna_rCURRENT.log` (or platform equivalent — see `references/yagna/install-and-init.md`).
3. Reduce to the minimal example from `references/sdks/golem-js.md` and confirm it works.
4. Ask in Discord: https://chat.golem.network — the community is responsive.

Source: synthesized from https://docs.golem.network/ + community channels — Last verified: 2026-05-13
