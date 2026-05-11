# Builders Guide

Technical reference for the **Builder Programme**: five tracks, recommended stack, and evaluation criteria. Required reading before the pitch.

---

## General framework

### Network model

Golem runs as a decentralized marketplace with two roles: the **requestor** asks for compute and pays in $GLM; the **provider** contributes capacity and earns. Both sides run the **yagna** daemon locally. Every project in the programme must execute real work on the network (testnet or mainnet) and prove it with logs and metrics.

→ Reference: [Golem Overview](https://docs.golem.network/docs/golem/overview).

### Current stack

| Layer | Component | When to use it |
|---|---|---|
| Daemon | **yagna** ≥ 0.17.4 | Always. Entry point to the network. [Installation](https://docs.golem.network/docs/quickstarts/js-quickstart). |
| High-level orchestration | **@golem-sdk/task-executor** | Default. Map-reduce patterns and parallelization. [Task Model](https://docs.golem.network/docs/creators/javascript/guides/task-model). |
| Low-level orchestration | **@golem-sdk/golem-js** 3.x | Fine-grained market control, custom provider selection. [API Reference](https://docs.golem.network/docs/golem-js/reference/overview). |
| Frontend | **@golem-sdk/react** | When the project has UI (mainly Tracks A and D). |

Primary language: **JavaScript / TypeScript on Node.js ≥ 20**. SDKs exist in other languages, but the documentation and examples live in the JS ecosystem.

### Testnet vs mainnet

- **Testnet (`hoodi`)** — Recommended by default. Free tGLM via the CLI command `yagna payment fund`, same API as mainnet, functionally equivalent for demonstration purposes. Alternatives also supported: sepolia, rinkeby, amoy. [Quickstart with `payment fund`](https://docs.golem.network/docs/quickstarts/js-quickstart).
- **Mainnet (Polygon)** — Only if the project requires real economic behavior or production integration. Runs on **Polygon** (`erc20-polygon-glm`), not Ethereum L1. Typical costs: units to tens of $GLM per project. Document costs in the final deliverable. [Switching to mainnet](https://docs.golem.network/docs/creators/javascript/examples/switching-to-mainnet) · [Payments model](https://docs.golem.network/docs/golem/payments).

The choice is declared in the pitch and kept throughout development. Any change must be notified to the team.

---

## Track A — Parallel Media Processing

**Parallel processing of audio and video files across multiple providers.**

The classic use case for decentralized compute and the most readable demo for a broad audience. Ideal as a first project for Web2 builders with backend or media processing experience.

**Suggested directions:**
- **Parallel transcoding with FFmpeg** — Split video, transcode segments in parallel, reassemble. Key metric: total time vs sequential execution. *Complexity: basic-intermediate.*
- **Parallel transcription with Whisper** — Long audio segmented into chunks, distributed transcription, merge with time markers. Reference: [gScribe](https://gscribe.ai/). *Intermediate.*
- **Image pipeline at scale** — Hundreds/thousands of images with parallel transformations (resize, format, filters, metadata). *Basic-intermediate.*
- **Web app with upload and processing** — UI to upload a file, choose processing, show progress per provider. *Intermediate-advanced.*

**Stack:** task-executor + FFmpeg/Whisper/ImageMagick in custom Golem images via Gvmkit-build. Optional frontend with @golem-sdk/react. Start from images in the [Golem Registry](https://registry.golem.network) or your own Dockerfile.

**Resources:** [Parallel tasks tutorial](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) · [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image) (FFmpeg, Whisper) · [Transferring data](https://docs.golem.network/docs/creators/javascript/examples/transferring-data) (chunks) · [Running in browser](https://docs.golem.network/docs/creators/javascript/tutorials/running-in-browser) (web app) · [tesseract-ocr-golem](https://github.com/golemfactory/tesseract-ocr-golem) · [Golem Registry](https://registry.golem.network)

**Success criterion:** Does the project demonstrate a measurable and reproducible time improvement on Golem vs a single machine, with metrics in the README?

---

## Track B — Compute-Intensive Simulation

**Numerical simulations, Monte Carlo, and scientific computation at scale.**

Parallelizable workloads where each unit of work is independent. The technical value is in the design of the parallelization: how to split, how to aggregate results, how to present outputs. Suitable for builders with quantitative backgrounds (finance, physics, statistics, engineering).

**Suggested directions:**
- **Monte Carlo for option pricing** — Tens/hundreds of thousands of distributed paths. Validate against Black-Scholes for European options. *Intermediate.*
- **Portfolio risk analysis** — VaR or Expected Shortfall via distributed simulation. *Intermediate-advanced.*
- **Physical or mathematical simulation** — Particle dynamics, fractals, cellular automata, epidemiological models. Visualizable output. *Intermediate.*
- **Matrix multiplication benchmark** — Block partitioning, comparison with local hardware. *Advanced.*

**Stack:** task-executor for orchestration. Language within providers is free (Python+NumPy/SciPy common, C++/Rust if CPU-bound). Package with Gvmkit-build. Local visualization: matplotlib, Plotly, D3.js.

**Resources:** [Running parallel tasks](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) · [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image) (Python+NumPy/SciPy) · [Task API Quickstarts](https://docs.golem.network/docs/creators/javascript/quickstarts) · [Golem Workers](https://github.com/golemfactory/golem-workers) (alternative API for direct CPU/GPU)

**Success criterion:** Does it execute real parallel computation across multiple providers, produce results validatable against a known baseline or convergence analysis, and document the parallelization decisions?

---

## Track C — Provider Reputation & Benchmarking

**Measurement, observability, and analysis tools for the provider ecosystem.**

Golem already has official reputation via AgreementSelector. This track does not replace it: it complements it with dashboards, benchmarking suites, audits, and visualizations. Unlike demo tracks, deliverables here can become tools for continuous use.

**Suggested directions:**
- **Public metrics dashboard** — Network status, active providers, prices, latencies, hardware. *Intermediate.*
- **Benchmarking suite per workload** — Standardized tests (rendering, transcoding, ML, compute) with periodic execution and rankings. *Intermediate-advanced.*
- **Independent audit tool** — Validate official metrics with random tests on providers. *Advanced.*
- **Discord bot / notification agent** — Periodic alerts or summaries: new providers, downtime, pricing changes. *Basic-intermediate.*

**Stack:** **golem-js directly** (preferable to task-executor for fine-grained provider selection control) + backend for structured storage (Postgres, SQLite, serverless) + presentation layer matching the format (dashboard, bot, API).

**Resources:** [Selecting providers](https://docs.golem.network/docs/creators/javascript/examples/selecting-providers) · [golem-js API Reference](https://docs.golem.network/docs/golem-js/reference/overview) · [Golem AgreementSelector](https://blog.golem.network/agreementselector/) · [yagna API](https://docs.golem.network/docs/golem/yagna)

**Success criterion:** Does it produce real data about the network state, present it usefully, and complement the official system without duplicating it?

---

## Track D — Chess Engine / Game AI at Scale

**Distributed game AI as a readable demonstration of parallelism.**

Distributing a game AI engine (chess, Go, Othello, strategy) works surprisingly well as a public demo: visually understandable logic, technically non-trivial, readable even for non-technical audiences. High viral potential.

**Suggested directions:**
- **Distributed Stockfish** — Wrapper that distributes analysis via Stockfish-MPI or search-tree partitioning. *Intermediate-advanced.*
- **Visual analysis interface** — UI showing in real time how providers evaluate lines and results consolidate. *Advanced.*
- **Distributed engine tournament** — Automatic games between Stockfish, Komodo, and custom engines, one per provider. *Intermediate.*
- **Alternative game AI** — Go with distributed MCTS, poker with hand simulation, strategy games with deep search. *Intermediate-advanced.*

**Stack:** task-executor for orchestration + the chosen game engine (Stockfish compiled from source for advanced integrations). For UI: @golem-sdk/react + chess.js or equivalent.

**Resources:** [Running parallel tasks](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) · [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image) (Stockfish compiled from source) · [Stockfish](https://stockfishchess.org/) · [chess.js](https://github.com/jhlywa/chess.js)

**Success criterion:** Does it genuinely distribute compute across multiple providers, produce a visually comprehensible deliverable, and document performance and cost metrics?

---

## Track E — Open Track

**Builder's own proposal, validated before kickoff.**

For builders with their own idea that uses Golem in an interesting way and doesn't fit tracks A-D. Conditions: it runs on real Golem, produces a public deliverable, and demonstrates the capabilities of decentralized compute.

**Eligible:** integrations with other ecosystems (Ethereum, IPFS, other Web3), exploratory demos for technical audiences, reusable libraries, artistic or experimental projects.

**Not eligible:** marginal or decorative use of Golem, duplication of previous work by the team or past builders, scope unfeasible in 4 weeks with 500 USD.

**Process:** pitch with more detail than A-D. Include justification for why it doesn't fit the defined tracks, explicit description of the parallelizable component, and references to similar prior work the builder has considered.

**Success criterion:** Does it concretely demonstrate a Golem capability that no previous programme project has shown, and produce a public deliverable that the community can study, replicate, or use?

---

## Common technical notes

- **Task granularity** — The minimum unit should run in the order of **seconds to minutes** per provider. Smaller = negotiation overhead erodes the benefit. Larger = wastes network capacity.
- **Errors and retries** — Providers can fail or produce invalid outputs. task-executor ships with default retry logic; tune parameters and document decisions.
- **Logging and observability** — Credible metrics require structured logs (timestamps, provider ID, costs, errors). Recommended: Node's `debug` package with namespace `golem-js:*`.
- **task-executor vs golem-js** — task-executor when it's classic map-reduce. golem-js when you need fine market control, long sessions, or custom selection logic.
- **Costs** — Testnet: negligible. Mainnet: typically units to tens of $GLM for programme scopes. Always document.
- **Limitations** — Golem optimizes embarrassingly parallel workloads, not low-latency communication between providers. Specific GPUs may have variable availability. Very large transfers between requestor and providers add overhead.

---

## If something breaks

Before asking on Discord, check the official troubleshooting docs — most frequent issues are already covered there.

- **yagna, app-key, payments, and file transfer errors** — [JS Requestor Troubleshooting](https://docs.golem.network/docs/troubleshooting/js-requestor). Covers `ECONNREFUSED 127.0.0.1:7465` (yagna not running), `Invalid application key`, `Insufficient funds` (missing `yagna payment fund`), `There is no requestor account...` (missing `yagna payment init`), `Transfer error: send failed because receiver is gone` (missing `VOLUME` in the Dockerfile), and CORS errors when running from the browser.
- **Images that won't build or broken transfers** — [Golem Images FAQ](https://docs.golem.network/docs/creators/javascript/guides/golem-images-faq) and [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image). Reminder: any directory that will be written to or uploaded must be declared as `VOLUME` in the Dockerfile.
- **Unexpected task-executor behavior** — [Task Model](https://docs.golem.network/docs/creators/javascript/guides/task-model) to understand the Activity lifecycle, retries, and provider selection.
- **Payments and allocations** — [Payments model](https://docs.golem.network/docs/golem/payments) to understand pay-as-you-go, batching, and differences between testnet and mainnet.

If the issue persists and isn't in the documentation, open a question in the builders channel of the [Golem Discord](https://discord.gg/golem) including: the failing command, exact error, yagna version (`yagna --version`), and network (testnet hoodi / mainnet polygon).
