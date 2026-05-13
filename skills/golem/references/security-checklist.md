# Security checklist

Golem combines local secrets (app-keys, identity), real-money payments (mainnet GLM), and code execution by untrusted Providers. This checklist applies whenever you touch a Golem requestor app.

## Secrets handling

### App-keys are bearer tokens

- **Never** `cat`, `echo`, `console.log`, or paste an app-key into a chat, screenshare, screenshot, or commit.
- After a public demo, `yagna app-key drop <name>` every key you created.
- Use one app-key per project. Don't share across unrelated codebases.
- Treat a leaked app-key like a leaked AWS access key: rotate immediately.

### Identity / wallet

- yagna's identity holds your GLM. The seed is stored locally in yagna's data dir.
- `yagna id export` writes the secret-storage format to disk for backup — **never** to chat, never to a Git repo, never to cloud storage without encryption-at-rest.
- A leaked identity = the attacker can spend your GLM. There is no recovery.

### Environment files

- `.env`, `.envrc`, and any file containing `YAGNA_APPKEY`, `YAGNA_AUTOCONF_APPKEY`, wallet keys, or RPC endpoints MUST be in `.gitignore`.
- Use a tool like `direnv` or `dotenv-safe` to keep an `.env.example` (committed, no values) alongside `.env` (uncommitted, real values).

## Cost controls

### Order-level ceilings

Every order on mainnet MUST set:

```js
market: {
  rentHours: <reasonable bound>,
  pricing: {
    model: "linear",
    maxStartPrice: <bound>,
    maxCpuPerHourPrice: <bound>,
    maxEnvPerHourPrice: <bound>,
  },
}
```

No unbounded pricing. No "let's see what the market gives us" on mainnet.

### Allocation bounds

`yapapi`'s `budget=X` is a hard ceiling for the whole session. Set it lower than what you think you need — the SDK refuses overflows rather than silently overspending.

### Run-time wall-clock guards

For long-lived requestor scripts, wrap the main loop in a hard timeout:

```js
const deadline = Date.now() + 30 * 60 * 1000;   // 30 minutes
while (Date.now() < deadline) { /* work */ }
```

A runaway loop on mainnet at $0.20/CPU-hour × 10 Providers can drain a wallet overnight.

## Provider trust

### All Provider output is untrusted

- `exe.run(...).stdout` and `.stderr` are byte streams from an unknown machine. Treat like user input from the internet.
- Never `eval` Provider output.
- Never shell-interpolate (`` `cmd ${output}` ``) — use args arrays.
- Validate (regex, schema, length checks) before writing to disk.
- If you re-feed Provider output into another command, validate against an allow-list.

### Filter to known-good Providers (when needed)

For high-value workloads, restrict to Providers you trust:

```js
market: {
  offerProposalFilter: (proposal) =>
    KNOWN_GOOD_NODES.includes(proposal.provider.id),
}
```

Maintain `KNOWN_GOOD_NODES` outside the codebase (per-environment config).

## Image supply chain

- A `.gvmi` image built by `gvmkit-build` is **public** once pushed. Never bake secrets into the image.
- Verify the source Dockerfile — base images can contain anything. Prefer official distro bases (`alpine`, `debian-slim`, `golem/*`).
- For production, pin to an **image hash**, not a moving tag — `imageTag: "you/repo@sha256:abc..."` rather than `"you/repo:latest"`.

## Network / yagna posture

- The yagna REST API binds to `127.0.0.1` by default. **Don't** expose it on `0.0.0.0` without an upstream auth proxy.
- Firewall: yagna needs outbound TCP/UDP for the P2P market. Don't block it, but **don't open inbound either** — the daemon doesn't need it.
- Run yagna under a dedicated user account if possible. Not as root, not as your dev user with broad sudo.

## Browser / public-facing apps

- A pure-browser SPA cannot safely hold a `YAGNA_APPKEY`. The browser will leak it (network tab, dev tools, malicious extensions).
- Use a backend proxy. See `references/sdks/react.md`.

## Pre-mainnet final review

Before any mainnet deploy, confirm:

- [ ] All `pricing` ceilings are bounded.
- [ ] Estimated worst-case spend is < user-approved limit.
- [ ] No app-keys in source control.
- [ ] All `await glm.disconnect()` / `executor.shutdown()` / `ray down` paths are reachable from any error.
- [ ] Untrusted Provider output is validated before use.
- [ ] An explicit stop command is documented.
- [ ] The user has been shown and approved the spend estimate.

## Incident response

If you suspect a leak:

1. `yagna app-key drop <name>` — revoke immediately.
2. `yagna payment status --network=polygon` — check for unexpected outflows.
3. If wallet is compromised: `yagna id create` + transfer remaining GLM out.
4. Audit Git history for accidentally committed secrets — and rotate them all even if you "deleted" them later (Git remembers).

Source: synthesized from https://docs.golem.network/ + standard crypto-skill safety practice — Last verified: 2026-05-13
