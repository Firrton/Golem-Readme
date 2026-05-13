# `@golem-sdk/golem-js`

The **core JavaScript / TypeScript SDK** for Golem Network. Exposes both the high-level *Renting Compute Resources* model and the low-level primitives (Market, Agreement, Activity, Allocation). `@golem-sdk/task-executor` is built on top of it.

## When to reach for it

- You need direct control over the **Market**: custom offer filters, scoring, geography selectors.
- You manage long-lived rentals (sessions, dApps) rather than discrete tasks.
- You want a single Provider held for the duration of a workflow.

For batch / map-reduce: prefer `@golem-sdk/task-executor` (see `task-executor.md`).

## Install

```bash
npm install @golem-sdk/golem-js @golem-sdk/pino-logger
```

Requires Node.js 18+ and a running yagna daemon. See `references/yagna/install-and-init.md`.

## Canonical quickstart (verified from docs)

```js
import { GolemNetwork } from "@golem-sdk/golem-js";
import { pinoPrettyLogger } from "@golem-sdk/pino-logger";

const order = {
  demand: {
    workload: { imageTag: "golem/alpine:latest" },
  },
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

(async () => {
  const glm = new GolemNetwork({
    logger: pinoPrettyLogger({ level: "info" }),
    api: { key: "try_golem" },
  });

  try {
    await glm.connect();

    const pool = await glm.manyOf({
      poolSize: { min: 1, max: 3 },
      order,
    });

    const data = [...Array(5).keys()];
    const results = await Promise.allSettled(
      data.map((i) =>
        pool.withRental((rental) =>
          rental
            .getExeUnit()
            .then((exe) =>
              exe.run(`echo "Part #${i}" && cat /proc/cpuinfo | grep 'model name'`),
            ),
        ),
      ),
    );

    results.forEach((r) =>
      r.status === "fulfilled"
        ? console.log("Success:", r.value.stdout)
        : console.log("Failure:", r.reason),
    );
  } catch (err) {
    console.error("Failed to run the example", err);
  } finally {
    await glm.disconnect();
  }
})().catch(console.error);
```

Save as `requestor.mjs` and run with `node requestor.mjs`.

## Core primitives

| Primitive | Role |
|---|---|
| `GolemNetwork` | Top-level entrypoint; wraps yagna connection |
| `glm.connect()` / `glm.disconnect()` | Open / close the yagna session |
| `glm.oneOf({ order })` | Rent one Provider for sequential work |
| `glm.manyOf({ poolSize, order })` | Pool of Providers for parallel work |
| `ResourceRental` | Wraps an Agreement + Activity for a single Provider |
| `rental.getExeUnit()` | Get the handle to run commands |
| `pool.withRental(fn)` | Auto-acquire / release a rental for `fn` |

## Filtering the market

```js
const order = {
  demand: { workload: { imageTag: "golem/alpine:latest" } },
  market: {
    rentHours: 1,
    pricing: { model: "linear", maxStartPrice: 0.1, maxCpuPerHourPrice: 0.2, maxEnvPerHourPrice: 0.05 },
    offerProposalFilter: (proposal) => proposal.provider.name.startsWith("trusted-"),
    offerProposalSelector: (offers) => offers.sort((a, b) => a.pricing.cpuSec - b.pricing.cpuSec)[0],
  },
};
```

## Mainnet payment platform

Switch the payment platform inside the order:

```js
const order = {
  // ...
  payment: { network: "polygon" },
};
```

Combined with `yagna payment fund --network=polygon`. See `references/yagna/networks.md` and `references/mainnet-migration.md`.

## Gotchas

- `glm.disconnect()` MUST be awaited inside a `finally` — leaking it leaves a Provider rented and accruing GLM cost.
- `api.key` must match an existing yagna app-key (or `YAGNA_AUTOCONF_APPKEY` value at startup).
- `imageTag` resolves against the Golem Registry (see `references/images/gvmkit-build.md`).

Source: https://docs.golem.network/docs/creators/javascript/quickstarts/quickstart — Last verified: 2026-05-13
