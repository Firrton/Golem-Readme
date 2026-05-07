# Builders Guide

Technical reference document of the **Builder Programme**. This guide describes the five available tracks, the recommended technical stack, the considerations common to all projects, and the criteria the Golem team uses to evaluate the technical scope of each proposal.

Reading this document is the recommended prior step before writing a pitch. It allows the builder to identify the right track, calibrate the project's scope and understand the level of technical depth expected from the deliverable.

---

## General framework

### How an application on Golem works

An application built on Golem Network operates under a decentralized market model in which two main roles coexist. The **requestor** is the one who requests compute, defines the characteristics of the workload and pays for its execution in $GLM. The **provider** is the one who contributes computational capacity from a machine connected to the network and receives payment corresponding to the service rendered.

The interaction between both roles is managed through a market in which requestors publish orders with their technical and budget requirements, providers respond with proposals, and the negotiation closes via a formal agreement that triggers the execution of the task. The whole life cycle, from negotiation to final payment, is mediated by the **yagna** daemon, which each participant runs locally.

For builders in the programme, this model means that each project must necessarily execute real work on the network, whether testnet or mainnet, and must be able to demonstrate via logs and metrics that the execution actually occurred in a distributed manner.

### Current technical stack

Golem Network currently offers a development stack organized in layers, designed to allow different levels of abstraction depending on the complexity of the use case. The programme recommends builders work with the current stack and avoid deprecated versions.

The central daemon is **yagna**, in version 0.17.4 or higher, which is the component that each builder runs locally to connect to the network. Installing yagna is the first technical step of any project and is documented in detail in the official Golem documentation.

On top of yagna, the programme recommends as the main path the use of **@golem-sdk/task-executor**, a JavaScript and TypeScript library oriented specifically to map-reduce patterns and task parallelization. Given that the five tracks of the programme revolve around parallelizable workloads, this library offers the most appropriate abstraction for most projects: the builder defines what task they want to execute, and the library takes care of orchestrating providers, managing retries and coordinating results.

For builders with more specific needs or prior experience in distributed systems, **@golem-sdk/golem-js** is available in its 3.x version, offering direct access to the protocol's low-level models (`ResourceRental`, `ExeUnit`, fine control of market and negotiation). This option is appropriate for projects that require non-standard orchestration logic, integration with complex frameworks or granular control over provider selection.

Additionally, **@golem-sdk/react** is available for builders who wish to incorporate a frontend into their project, which is particularly relevant for Tracks A and D, where the visual dimension provides demonstrative value.

As a quick reference, builders should assume that the primary language of the programme is JavaScript or TypeScript running on Node.js 20 or higher. Alternative SDKs in other languages exist, but the most up-to-date documentation and official examples concentrate on the JavaScript ecosystem.

### Testnet and mainnet

The programme accepts deliverables executed both on Golem's testnet and on mainnet. Each option has distinct implications worth considering when planning the project.

The testnet, which currently runs on the **hoodi** network, is the recommended environment for most projects in the programme. It allows real work to be executed on the network without the need to acquire $GLM on mainnet, uses test tokens (tGLM) that can be obtained for free from a faucet, and offers the same API surface as mainnet. For demonstration purposes, the testnet is functionally equivalent to mainnet and sufficient to satisfy the programme's requirements.

Mainnet, on the other hand, runs with real $GLM and should be used when the project requires demonstrating real economic behaviour, integrations with production systems or use cases that depend specifically on the marketplace under real conditions. Builders who opt for mainnet should anticipate in their pitch the costs associated with compute usage, which are generally modest but should be documented in the final deliverable.

The choice between testnet and mainnet must be made explicit in the pitch and remain consistent during development. Any change between networks during the execution of the project requires notification to the Golem team.

---

## Track A — Parallel Media Processing

**Parallel processing of audio and video files across multiple providers.**

### Description

Media processing constitutes the classic use case of decentralized compute and the most legible technical demonstration for a wide audience. The logic is straightforward: a large file is split into fragments, each fragment is processed independently on a different provider, and the results are reassembled into a single output file. What would take twenty minutes on a single machine can be completed in a fraction of the time if the load is distributed correctly.

This track is especially suitable as a first project on Golem for Web2 builders with experience in backend or media processing. The chunking and merge logic is relatively intuitive, the auxiliary tools (FFmpeg, Whisper) are widely known, and the final deliverable allows the benefit of parallelization to be demonstrated visually.

### Suggested project directions

**Parallel video transcoding with FFmpeg.** Build a tool that takes a video file as input, splits it into segments of fixed duration, runs FFmpeg on each segment on a different provider to transcode it into one or several output formats (for example, H.264 in different resolutions for adaptive streaming), and reassembles the segments into a coherent final file. The key metric to document is the total processing time compared to sequential execution on a single machine. Estimated complexity: basic to intermediate.

**Parallel audio transcription with Whisper.** Take a long audio file (a conference, a podcast, an interview), segment it into chunks with minimal overlap to preserve continuity, run Whisper on each chunk in parallel across multiple providers, and combine the resulting transcripts into a single text with correct timestamps. The reference project [gScribe](https://gscribe.ai/) implements this direction and can be consulted as an example. Estimated complexity: intermediate.

**Image processing pipeline at scale.** Build a tool that receives a large set of images (for example, several hundred or thousand) and applies transformations in parallel: resizing, format conversion, application of filters, metadata extraction, thumbnail generation. The technical interest lies in designing the minimum unit of work and in efficiently managing file transfers between the requestor and the providers. Estimated complexity: basic to intermediate.

**Web application with upload and processing on Golem.** Build a simple web interface in which a user can upload a file, choose a type of processing, and get the processed result back. The application should transparently demonstrate that the processing occurs on Golem, ideally showing in the UI the progress of the individual providers. This direction combines distributed backend with frontend, and is particularly suitable for builders with full-stack experience. Estimated complexity: intermediate to advanced.

### Recommended technical stack

The most direct path is @golem-sdk/task-executor for parallel task orchestration, in combination with FFmpeg, Whisper, ImageMagick or other open-source tools installed inside custom Golem images via Gvmkit-build. Builders can start from existing images in the [Golem Registry](https://registry.golem.network) or build their own from a Dockerfile. For projects with frontend, @golem-sdk/react offers hooks that simplify integration between the interface and execution on the network.

### Deliverables

The deliverable consists of a public GitHub repository with functional code, a detailed README that includes reproducible installation and execution instructions, at least one documented run with real metrics comparing the execution time on Golem against a single-machine baseline, and a brief write-up published on the Golem Discord that explains in accessible language what was built and what was learned.

### Relevant resources

- [Tutorial: Running tasks in parallel](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) in the official documentation.
- [Tesseract OCR on Golem](https://github.com/golemfactory/tesseract-ocr-golem) as an example of a library that parallelizes a CLI tool over the network.
- [Golem Registry](https://registry.golem.network) for pre-existing images usable in the project.

### Success criterion

Does the project demonstrate a measurable and reproducible improvement in processing time when running on Golem compared to a single machine, with metrics documented in the README?

---

## Track B — Compute-Intensive Simulation

**Numerical simulations, Monte Carlo and scientific computation at scale.**

### Description

Golem is particularly well-suited for workloads that benefit from large-scale parallelism: Monte Carlo simulations, numerical experiments, combinatorial analysis and any computation in which each unit of work is independent of the others. The technical interest of this track lies less in the tool used and more in the design of the parallelization: how to divide the problem into units of work, how to aggregate the partial results, and how to present the outputs in a comprehensible way.

This track is suitable for builders with technical or academic background in quantitative disciplines (finance, physics, applied mathematics, statistics, engineering) who want to use Golem as compute infrastructure for a concrete experiment. It is also attractive for Web2 developers interested in high-performance computing who are looking for a decentralized alternative to traditional clusters.

### Suggested project directions

**Monte Carlo simulation for option pricing.** Implement a pricing model for European or Asian options via Monte Carlo simulation, distributing tens or hundreds of thousands of simulation paths across multiple providers. The deliverable should include comparison of results against known analytical formulas (Black-Scholes for European options) as correctness validation, and convergence metrics showing how the error decreases as the number of simulations grows. Estimated complexity: intermediate.

**Portfolio risk analysis.** Build a tool that takes the composition of a portfolio of assets and runs a Value at Risk (VaR) or Expected Shortfall analysis via distributed simulation. The interest of the project lies in demonstrating how Golem allows analyses of greater granularity or over a greater number of scenarios than would be feasible on an individual machine. Estimated complexity: intermediate to advanced.

**Parallelizable physical or mathematical simulation.** Implement a classical simulation in which each unit of work is independent: particle dynamics with random initial conditions, distributed generation of fractals with variable parameters, search for patterns in cellular automata, exploration of parameter spaces in epidemiological models. The choice of problem is free as long as the parallelization component is genuine and the output is visualizable or presentable in a clear manner. Estimated complexity: intermediate.

**Large-scale matrix multiplication benchmark.** Implement distributed multiplication of large matrices via block partitioning, comparing the performance of Golem against local hardware at different input sizes. This project is more technical than applied, but produces useful quantitative data on the characteristics of the network and can become a reference for future builders. Estimated complexity: advanced.

### Recommended technical stack

@golem-sdk/task-executor is again the main option for orchestration. The choice of computation language inside the providers is free and depends on the problem: Python with NumPy and SciPy is common for scientific problems, while C++ or Rust are preferable when the bottleneck is pure CPU. Builders can package their dependencies in custom Golem images via Gvmkit-build. For visualization of results, standard libraries such as matplotlib, Plotly or D3.js are appropriate and do not need to run on Golem.

### Deliverables

The repository must include functional code with reproducible instructions, the results of at least one real run with visualization or table of results, a section in the README documenting what was parallelized, what was kept sequential and why, and notes on the technical challenges encountered during parallelization (granularity of tasks, error handling, aggregation of results).

### Relevant resources

- [Task API Quickstarts](https://docs.golem.network/docs/creators/javascript/quickstarts) for basic parallelization patterns.
- [Golem Workers](https://github.com/golemfactory/golem-workers) as a high-level alternative API for direct CPU and GPU access.

### Success criterion

Does the project effectively run computations in parallel across multiple providers, produce results validatable against a known baseline or a convergence analysis, and document in a comprehensible way the design decisions of the parallelization?

---

## Track C — Provider Reputation & Benchmarking

**Measurement, observability and analysis tools for the provider ecosystem.**

### Description

As the number of providers connected to the network grows, the question of which ones are fast, reliable, economical or suitable for specific workloads becomes increasingly relevant. Golem already has an official reputation system implemented in the AgreementSelector component, which means this track does not aim to replace that infrastructure, but rather to build complementary tools that enrich it: public dashboards, specialized benchmarking suites, audit tools and visualizations that make ecosystem data more accessible.

This track is suitable for builders with experience in data engineering, observability, dashboards or distributed systems. It produces deliverables with clear differential value: unlike demo-oriented tracks, projects in this track can become tools of continuous use within the ecosystem.

### Suggested project directions

**Public dashboard of network metrics.** Build a web application that queries the state of the Golem network, gathers data on active providers, price distribution, latencies, hardware capabilities offered, and presents them in an accessible and up-to-date dashboard. The project can consume data from the existing AgreementSelector and enrich it with its own metrics. Estimated complexity: intermediate.

**Benchmarking suite for specific workloads.** Design and implement a battery of standardized tests that measure the performance of providers in concrete workload categories: rendering, transcoding, ML inference, numerical computation. The suite should run periodically, store results in a structured way, and publish rankings or comparatives that allow other builders to choose providers suitable for their use cases. Estimated complexity: intermediate to advanced.

**Independent audit tool.** Build a tool that externally validates the metrics reported by the official reputation system, running random tests on selected providers and comparing the observed results against those expected according to the AgreementSelector. The value of the project lies in providing additional transparency to the ecosystem. Estimated complexity: advanced.

**Discord bot or notification agent.** Build a bot that monitors the state of the network continuously and publishes on the Golem Discord alerts or periodic summaries: new providers, detected outages, significant changes in pricing, top performers of the week. The project combines monitoring infrastructure with accessible presentation for the community. Estimated complexity: basic to intermediate.

### Recommended technical stack

The project requires use of the Golem SDK for executing tests on providers (@golem-sdk/golem-js is preferable to task-executor in this track because projects usually need fine control over provider selection and market filters), a backend for structured storage of results (PostgreSQL, SQLite, or a serverless database depending on the scope), and a frontend or presentation layer appropriate to the format of the deliverable (web dashboard, Discord bot, public API).

### Deliverables

The repository must include functional code, at least one complete execution with real data gathered from the network, a visualization or summary of the data obtained, and documentation that allows other builders to run the tool or consume its outputs.

### Relevant resources

- [Golem AgreementSelector](https://blog.golem.network/agreementselector/) as reference of the official reputation system.
- [yagna API](https://docs.golem.network/docs/golem/yagna) for programmatic access to the state of the network.

### Success criterion

Does the project produce real data on the state of the Golem network, present it in a comprehensible and useful way, and provide value that complements the official reputation system without duplicating it?

---

## Track D — Chess Engine / Game AI at Scale

**Game artificial intelligence as a legible demonstration of parallelism.**

### Description

Distributing a game artificial intelligence engine (chess, Go, Othello, strategy games) across multiple providers turns out to be surprisingly effective as a public demonstration of Golem. The logic is visually comprehensible, technically non-trivial, and the result is legible even for non-technical audiences. This track uses game AI as a vehicle for demonstrating parallelism, not as an end in itself.

It is suitable for builders interested in games, AI, search in decision trees or distributed systems, and produces deliverables with high viral potential on social networks and community. A well-built demo in this track can become one of the most effective marketing resources of the programme.

### Suggested project directions

**Distributed Stockfish on Golem.** Implement a wrapper that distributes Stockfish's analysis (the strongest open-source chess engine) across multiple providers, allowing several positions to be analysed simultaneously or the analysis of a single position to be deepened by partitioning the search tree. The Stockfish-MPI variant is particularly suitable for distributed parallelization. Estimated complexity: intermediate to advanced.

**Visual interface for distributed analysis.** Build a web application that shows in real time how the analysis is distributed across providers: a chess position on screen, individual providers evaluating different lines, and the results consolidating into a final recommendation. The visual dimension makes the project particularly demonstrative. Estimated complexity: advanced.

**Distributed engine tournament.** Implement a system that runs automatic tournaments between different chess engines (Stockfish, Komodo, custom engines) on Golem, with each game running on a different provider. The deliverable includes the tournament results, time and cost metrics, and an interface to visualize the games. Estimated complexity: intermediate.

**Distributed alternative game AI.** Instead of chess, implement parallelization for another game: Go with distributed Monte Carlo Tree Search, poker with hand simulation at scale, or a strategy game with deep search. The choice of game is free as long as the parallelizable component is genuine. Estimated complexity: intermediate to advanced.

### Recommended technical stack

@golem-sdk/task-executor for orchestration of parallel evaluations, together with the chosen game engine (Stockfish is usually compiled from source for advanced integrations). For the visual interface, @golem-sdk/react allows the game state to be linked with execution on the network in a natural way. Libraries such as chess.js or equivalents facilitate the representation of the game state in the frontend.

### Deliverables

The repository must include functional code with execution instructions, a recording or screenshots showing the system in operation, metrics documenting the cost in $GLM and the execution times observed, and a write-up for Discord that explains in an accessible way what was built.

### Relevant resources

- [Stockfish](https://stockfishchess.org/) as the reference chess engine.
- [chess.js](https://github.com/jhlywa/chess.js) for game state manipulation in JavaScript.

### Success criterion

Does the project genuinely distribute computation across multiple providers, produce a deliverable visually comprehensible to a wide audience, and document concrete metrics of performance and cost?

---

## Track E — Open Track

**Builder's free proposal, validated before kickoff.**

### Description

Track E is reserved for builders who have their own idea that uses Golem's compute in an interesting way and that does not naturally fit into the four previous tracks. The flexibility is deliberate: the Golem team prefers to fund well-oriented work coming from the builder's own initiative rather than forcing projects to fit into predefined tracks.

The only substantive conditions are that the project effectively runs on Golem, produces a public and shareable deliverable, and demonstrates what decentralized compute makes possible. The procedural condition is that the pitch must be reviewed and approved before the start of development, which is valid for all tracks but takes on particular importance in this case.

### Eligible directions

Any project that requires non-trivially parallelizable distributed compute qualifies for this track. This includes tools and integrations that connect Golem with other ecosystems (Ethereum mainnet, IPFS, other Web3 protocols), exploratory demos showing protocol capabilities to a specialized technical audience, reusable libraries that facilitate the use of Golem for specific use cases, or artistic and experimental projects that use the network in a creative way.

Proposals that use Golem only in a marginal or decorative way do not qualify for this track, nor do projects that duplicate work already done by the Golem team or by previous participants of the programme, nor projects of such a wide scope that they cannot be carried out in four weeks with a 500 USD bounty.

### Specific process

Since the track has no predefined directions, the Golem team requires more detail in the pitch to evaluate viability. It is recommended to include, in addition to the standard elements of the [pitch-template](./pitch_template.md), a brief section justifying why the project does not fit into tracks A to D, an explicit description of the parallelizable component, and any reference to similar prior work that the builder has considered.

### Deliverables

The deliverables are the same as for the specific tracks: public repository with functional code, clear README, execution metrics on Golem, and write-up for Discord. The specific form of the deliverable is agreed upon during pitch approval.

### Success criterion

Does the project concretely demonstrate a capability of Golem that no previous project in the programme had shown, and does it produce a public deliverable that the community can study, replicate or use?

---

## Common technical notes

Beyond the particularities of each track, there are cross-cutting considerations that apply to any project in the programme and are worth keeping in mind from the design phase.

### Granularity of tasks

The correct design of the minimum unit of work is probably the most important technical decision of any project. Tasks too small generate negotiation and communication overhead that erodes the benefit of parallelization. Tasks too large waste the capacity of the network by concentrating work on few providers. As an initial heuristic, a reasonable unit of work runs on the order of seconds to minutes on an individual provider, not milliseconds or hours.

### Error handling and retries

Providers in a decentralized network may fail, disconnect or produce invalid results. Any serious project on Golem must contemplate retry mechanisms, output validation, and eventually exclusion of problematic providers. @golem-sdk/task-executor includes default retry logic, but builders should verify that the parameters are appropriate to their use case and document the decisions taken.

### Logging and observability

The metrics of the final deliverable must be credible and reproducible. This requires structured logging during the execution of the project: timestamps of each task, provider identifiers, individual costs, captured errors. Deliverables that report metrics without supporting logs have less demonstrative value. It is recommended to use the `debug` package of Node.js or equivalent, configuring the `golem-js:*` namespaces to capture relevant SDK activity.

### Choice between task-executor and golem-js

As a general rule, task-executor is the right option when the problem fits a map-reduce pattern: independent tasks, the same type of computation, simple aggregation of results. golem-js directly is preferable when the project requires fine control over provider selection, custom market logic, management of long-running sessions, or integration with frameworks that are not compatible with the task-based model.

### Costs and budget

A typical project of the programme, executed mostly on testnet, has negligible compute costs. For projects on mainnet, costs vary depending on the volume of work and the providers selected, but generally remain in the order of single digits to tens of $GLM for the expected scopes. Builders running on mainnet should anticipate this cost and document it in the deliverable.

### Limitations to keep in mind

Golem is a general-purpose network, but there are certain use cases where its performance may be suboptimal. Workloads that require very low-latency communication between providers during execution are not ideal for Golem, given that the network optimises for embarrassingly parallel workloads rather than fine synchronization. Workloads that require specific GPUs may encounter limited or variable availability. Very large file transfers between requestor and providers introduce overhead that must be considered in the architecture.

These limitations do not rule out any track of the programme, but they should be kept in mind when defining the scope of the project during the pitch phase.
