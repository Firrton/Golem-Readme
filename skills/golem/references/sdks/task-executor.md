# `@golem-sdk/task-executor`

The **Task Model** SDK on top of `@golem-sdk/golem-js`. Use it when you have a list of inputs and want each one processed on a Golem Provider as an independent task, with retries and pooling handled for you.

## When to reach for it

- Batch / map-reduce workloads: process N files, run N simulations, transcribe N audio clips.
- Each unit of work is independent — no cross-task state.
- You want the SDK to manage retries and provider pool size for you.

For market-control (custom filters, agreement lifecycle, long-lived rentals): use `@golem-sdk/golem-js` directly (see `golem-js.md`).

## Install

```bash
npm install @golem-sdk/task-executor @golem-sdk/pino-logger
```

Requires Node.js 18+ and a running yagna daemon. See `references/yagna/install-and-init.md`.

## Minimal example

```js
import { TaskExecutor, pinoPrettyLogger } from "@golem-sdk/task-executor";

const executor = await TaskExecutor.create({
  logger: pinoPrettyLogger({ level: "info" }),
  api: { key: process.env.YAGNA_APPKEY ?? "try_golem" },
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
  task: { maxParallelTasks: 3 },
});

try {
  const inputs = ["one", "two", "three"];
  const results = await Promise.all(
    inputs.map((label) =>
      executor.run(async (exe) => {
        const out = await exe.run(`echo "processing ${label}"`);
        return out.stdout;
      }),
    ),
  );
  console.log(results);
} finally {
  await executor.shutdown();
}
```

## Lifecycle

1. `TaskExecutor.create(...)` — connect to yagna, open the market with your demand, build a pool.
2. `executor.run(async (exe) => { ... })` — pick (or rent) a Provider, run your function with the ExeUnit, return the result. Auto-retries on transient failures.
3. `executor.shutdown()` — settle invoices, release rentals, disconnect. Always put it in `finally`.

## Common ExeUnit operations

```js
await exe.run("ls /workspace");                // shell command
await exe.uploadFile("./local.txt", "/in.txt"); // local → provider
await exe.downloadFile("/out.txt", "./out.txt"); // provider → local
await exe.uploadJson({ x: 1 }, "/in.json");
await exe.beginBatch().run("a").run("b").end(); // batch multiple commands
```

## Cost control

The `market.pricing` block is the single most important cost lever. On mainnet, set conservative ceilings:

```js
pricing: {
  model: "linear",
  maxStartPrice: 0.05,
  maxCpuPerHourPrice: 0.2,
  maxEnvPerHourPrice: 0.05,
}
```

Combine with `task.maxParallelTasks` to cap concurrency.

## Retries & filters

`TaskExecutor` retries failed tasks by default (configurable via `task.maxTaskRetries`). To narrow the provider pool (geography, reputation, name allow-list), pass a `market.offerProposalFilter` — see `golem-js.md` for filter primitives.

## Gotchas

- Don't share `TaskExecutor` instances across modules — keep one per app run.
- `shutdown()` MUST be awaited or you'll leak rentals and overpay on mainnet.
- The Task Model assumes idempotent tasks. If `executor.run` is retried, your function must tolerate re-execution.

Source: https://docs.golem.network/docs/creators/javascript — Last verified: 2026-05-13
