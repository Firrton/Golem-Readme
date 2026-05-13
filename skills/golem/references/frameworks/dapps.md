# Dapps Framework

The **dApps on Golem** framework deploys multi-service applications on Golem from a declarative YAML descriptor — feels like `docker-compose` but the services run on different Providers.

> **Status**: the docs explicitly mark this framework as **experimental / early access**. Flag this to the user. For long-term production work, evaluate carefully and have a fallback to the JS / Python SDK.

## When to reach for it

- You have a multi-tier app — web frontend + API + database / state — and want each tier on a Provider.
- You prefer **declarative config** over SDK code.
- Examples: a public website + backend, a chat app, a data pipeline with multiple stages.

Don't use it for:
- Pure compute batch — `task-executor` is simpler.
- Anything that requires fine-grained market control.
- Mission-critical production until the framework stabilizes.

## Install

```bash
pip install dapp-manager dapp-runner
```

`dapp-manager` is the CLI you interact with. `dapp-runner` is the underlying executor; the manager invokes it.

## Anatomy of a dApp descriptor

A dApp is one or more YAML files describing the services and how they connect. Conceptually:

```yaml
payload:
  web:
    runtime: vm
    params:
      image_hash: <hash-of-your-web-image>
  api:
    runtime: vm
    params:
      image_hash: <hash-of-your-api-image>

nodes:
  web:
    payload: web
    init:
      - ["/bin/sh", "-c", "nginx"]
    network:
      - api
  api:
    payload: api
    init:
      - ["/bin/sh", "-c", "python app.py"]
```

(Exact schema evolves — verify against current docs and the `dapp-runner` repo before committing to a structure.)

## Commands

```bash
# Start a dApp
dapp-manager start --config config.yaml my-dapp-descriptor.yaml

# List running dApps
dapp-manager list

# Stop a dApp (always do this when done)
dapp-manager stop <dapp-id>

# Inspect logs / state
dapp-manager read <dapp-id> log
dapp-manager read <dapp-id> state
```

## Reference example apps

- **ToDo List App** — React + Flask + RQLite multi-tier deployment.
- **Weather Stats App** — service with outbound internet access.

Both live in `https://github.com/golemfactory` org repos and serve as templates. Clone, adapt the descriptor, replace image hashes.

## Mainnet config

The dApp config carries a `payment_network` field analogous to other frameworks. Default it to `hoodi`; set `polygon` or `mainnet` only with explicit user approval.

## Gotchas

- **Public APIs need outbound network**: provider images must be allowed to make outbound HTTP, which requires the `outbound` capability on the Provider. Not all providers offer it.
- **Inter-service networking**: dApp connects services via a virtual private network. Latency between nodes is highly variable.
- **Image caching**: each Provider in the dApp downloads its own image. Plan for slow first-boot.
- The framework is in active development; APIs and YAML schema can change between minor versions.

## Fallback strategy

If a dApp descriptor doesn't fit the workload, drop down to `@golem-sdk/golem-js` and orchestrate the services manually — you get full control at the cost of more code. The framework is an optimization, not a hard requirement.

Source: https://docs.golem.network/docs/creators/dapps — Last verified: 2026-05-13
