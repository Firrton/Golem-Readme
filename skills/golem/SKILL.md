---
name: golem
description: "Trigger: golem network, yagna, GLM, $GLM, requestor, provider, task-executor, golem-js, gvmkit, Ray on Golem, hoodi testnet, decentralized compute. Build, debug, deploy Golem Network requestor apps."
license: Apache-2.0
metadata:
  author: Golem Network Community
  version: "1.0"
compatibility: "Requires Node.js 18+ and the yagna daemon (>=0.15) running locally."
---

# Golem Network

Domain skill for building, debugging, and deploying Golem Network requestor applications — apps that rent compute power from a decentralized network of Providers in exchange for GLM (testnet: tGLM).

## What this Skill is for

Use this skill when the user wants to:

- Build a Golem **Requestor** app in JS/TS or Python.
- Rent compute, run shell commands on a Provider, collect results.
- Create a custom **Golem VM image** (`.gvmi`) from a Dockerfile via `gvmkit-build`.
- Run distributed Python with **Ray on Golem**.
- Deploy a multi-service app with the **Dapps Framework**.
- Switch a requestor between **hoodi testnet** and **mainnet / polygon**.
- Manage **app-keys**, allocations, payments, or debug a misbehaving yagna daemon.

Do NOT use this skill for: Provider-side setup (`golemsp run`) unless explicitly asked; arbitrary Ethereum dApp work that isn't using Golem compute.

## Default stack decisions (opinionated)

1. **SDK selection.** Default to `@golem-sdk/task-executor` for batch / map-reduce workloads — it implements the Task Model on top of `golem-js`. Drop to `@golem-sdk/golem-js` directly when the user needs market control (custom selectors, filters, agreement lifecycle). Use `@golem-sdk/react` only at the UI boundary. Pick `yapapi` (Python) only when JS is not viable.
2. **Network = hoodi testnet by default.** Free tGLM via `yagna payment fund`. NEVER switch to `polygon` or `mainnet` without explicit user confirmation AND an explicit cost cap. Polygon is preferred over Ethereum mainnet (lower gas).
3. **Images.** Reach for stock Golem Registry images first (`golem/alpine:latest`, `golem/python:3.11`, etc.). Build a custom `.gvmi` with `gvmkit-build` only when stock doesn't cover deps.
4. **Frameworks.** Use **Ray on Golem** for distributed Python (AI/ML, data parallel). Use **Dapps Framework** for docker-compose-style multi-service deploys — flag to the user that it is experimental / early access.

## Mental model

A Golem requestor app is a node that talks to its local `yagna` daemon. yagna negotiates with Providers on the Market, signs an Agreement, runs an Activity inside an ExeUnit, and settles payments from a pre-funded Allocation.

| Concept | Role |
|---|---|
| **Requestor** | The user / your app — rents compute |
| **Provider** | Remote node offering compute for GLM |
| **yagna** | Local daemon; gateway to the network |
| **Market** | Demand ↔ Offer matching layer |
| **Agreement** | Signed contract for a unit of work |
| **Activity** | Execution session on a Provider |
| **ExeUnit** | Handle to run shell commands remotely |
| **Allocation** | Locked budget reserved for invoices |
| **Payment Platform** | (token, network, driver) tuple — e.g. (GLM, polygon, erc20) |
| **GLM / tGLM** | Mainnet / testnet ERC-20 payment token |
| **App-key** | Bearer token for the local yagna REST API |

## Agent safety guardrails

These are non-negotiable. Apply them in every Golem session.

1. **Mainnet = real money.** Never run `yagna payment fund --network=polygon` or `--network=mainnet` without explicit user confirmation. Always print the network name and an estimated GLM ceiling first. Default to `--network=hoodi` (or no flag) for testnet.
2. **App-keys are bearer secrets.** Never `cat`, `echo`, or paste `YAGNA_APPKEY` / `YAGNA_AUTOCONF_APPKEY` into chat or logs. Always `.gitignore` `.env`. Rotate with `yagna app-key drop` after demos.
3. **Bound cost via order pricing.** Always set `maxStartPrice`, `maxCpuPerHourPrice`, `maxEnvPerHourPrice` inside `order.market.pricing`. Never deploy unbounded pricing on mainnet.
4. **Untrusted provider output.** Treat every `exe.run(...)` stdout/stderr as untrusted input. Never `eval`, never shell-interpolate, validate before writing to disk.
5. **No seed phrases / private keys.** yagna manages keys internally. Never ask the user for their wallet seed. `yagna id export` is for local backup only — never to chat.

## Quick start (hoodi testnet)

```bash
# 1. Install yagna (Linux / macOS)
curl -sSf https://join.golem.network/as-requestor | bash -

# 2. Pick an app-key name (any string)
export YAGNA_AUTOCONF_APPKEY=my_requestor

# 3. Start the yagna daemon (keep this terminal running)
yagna service run

# 4. In another terminal, fund testnet tokens
yagna payment fund

# 5. Initialize a project
mkdir my-golem-app && cd my-golem-app
npm init -y
npm install @golem-sdk/golem-js @golem-sdk/pino-logger

# 6. Run a minimal example (see references/sdks/golem-js.md)
node requestor.mjs
```

## Decision tree — what kind of workload?

| Workload | SDK | Image strategy |
|---|---|---|
| Parallel media (FFmpeg, Whisper, transcoding) | task-executor | `gvmkit-build` from FFmpeg / Whisper base |
| Monte Carlo / scientific compute | task-executor | `gvmkit-build` with Python + numerics |
| Network metrics / benchmarking | golem-js | Stock alpine image |
| AI / ML inference at scale | Ray on Golem | Ray ML base image |
| Multi-service app (web + API + DB) | Dapps Framework | docker-compose-style recipe |
| Frontend with live Golem control | golem-js + react | Depends on workload |
| Python distributed compute (general) | Ray on Golem (or yapapi) | Python base image |

## Quick reference

### SDK comparison

| Package | Language | Level | Best for |
|---|---|---|---|
| `@golem-sdk/task-executor` | JS / TS | High (Task Model) | Batch / map-reduce |
| `@golem-sdk/golem-js` | JS / TS | Core (low + high) | Fine-grained control |
| `@golem-sdk/react` | JS / TS | UI boundary | Hooks for frontends |
| `@golem-sdk/pino-logger` | JS / TS | Logging | Pretty pino output |
| `@golem-sdk/cli` | JS / TS | CLI | Operational tooling |
| `yapapi` | Python | Low + High | Python-only stacks |

### Networks

| Network | Type | Token | yagna flag | Default? |
|---|---|---|---|---|
| `hoodi` | Testnet | tGLM | `--network=hoodi` (or none) | ✅ |
| `sepolia` | Testnet | tGLM | `--network=sepolia` | — |
| `polygon` | Mainnet | GLM | `--network=polygon` | — (recommended for prod) |
| `mainnet` | Mainnet | GLM | `--network=mainnet` | — (Ethereum, high gas) |

### Minimal `order` shape (JS SDK)

```js
const order = {
  demand: { workload: { imageTag: "golem/alpine:latest" } },
  market: {
    rentHours: 0.5,
    pricing: {
      model: "linear",
      maxStartPrice: 0.5,
      maxCpuPerHourPrice: 1.0,
      maxEnvPerHourPrice: 0.5,
    },
  },
};
```

## Operating procedure

1. **Classify the workload** against the decision tree above.
2. **Pick the SDK** — `task-executor` for batch, `golem-js` for control, `Ray on Golem` for Python at scale, `Dapps` for multi-service.
3. **Design task granularity** — each unit should run in seconds-to-minutes; larger = fewer market round-trips, smaller = finer parallelism.
4. **Run on hoodi first.** Always validate end-to-end on testnet before touching real money.
5. **Set explicit pricing caps** in `order.market.pricing` even on testnet — surfaces mispriced offers early.
6. **Measure** time / GLM / success rate per task before any mainnet switch.

## Progressive disclosure — read these references when…

- Building a requestor app → `references/sdks/task-executor.md` or `references/sdks/golem-js.md`
- Wiring Golem into a React UI → `references/sdks/react.md`
- Working in Python without Ray → `references/sdks/yapapi.md`
- Installing or operating yagna → `references/yagna/install-and-init.md`
- Managing app-keys safely → `references/yagna/app-keys.md`
- Switching networks (testnet ↔ mainnet) → `references/yagna/networks.md`
- Building a custom VM image → `references/images/gvmkit-build.md`
- Running Python at scale → `references/frameworks/ray-on-golem.md`
- Deploying multi-service apps → `references/frameworks/dapps.md`
- Understanding allocations, invoices, GLM accounting → `references/payments.md`
- About to ship to mainnet → `references/mainnet-migration.md`
- Hit an error / debugging → `references/common-errors.md`
- Handling keys, costs, untrusted output → `references/security-checklist.md`
- Official docs, GitHub orgs, Discord, Registry → `references/resources.md`

Source: https://docs.golem.network/ — Last verified: 2026-05-13
