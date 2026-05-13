# Ray on Golem

**Ray on Golem** runs a [Ray](https://www.ray.io/) cluster on top of Golem Providers. Use it when you have Python code that's already Ray-friendly (or trivial to make Ray-friendly with `@ray.remote`) and you want to scale it out across rented compute.

## When to reach for it

- You have **Python** workloads that fan out: data parallel, ML inference, hyperparameter sweeps.
- You already use Ray locally and want the same code to run distributed without rewriting.
- The unit of work runs for **seconds-to-minutes**, not milliseconds (Ray's actor / task overhead doesn't pay off below that).

Don't use it for:
- One-shot batch in JS — use `task-executor`.
- Long-lived single-Provider sessions — use `golem-js` directly.
- Multi-service web apps — use the Dapps Framework.

## Install

```bash
pip install ray-on-golem
```

This pulls Ray itself and the Golem daemon (`yagna`) as dependencies. Python 3.9+ recommended.

## Cluster YAML (minimal)

```yaml
cluster_name: my-ray-cluster
provider:
  type: external
  module: ray_on_golem.provider.GolemNodeProvider
  parameters:
    payment_network: hoodi          # use polygon for mainnet
    image_tag: golem/ray-on-golem:py3.10
    budget: 1.0                     # GLM ceiling per cluster lifetime
max_workers: 5
upscaling_speed: 2

head_node:
  num_cpus: 1
worker_nodes:
  - num_cpus: 1
    min_workers: 1
    max_workers: 5
```

Save as `golem-cluster.yaml`.

## Lifecycle

```bash
# Start the Ray cluster on Golem
ray up golem-cluster.yaml

# Submit a Ray job (any normal Ray code)
ray submit golem-cluster.yaml my_script.py

# Inspect dashboard
ray dashboard golem-cluster.yaml      # opens local proxy

# Tear down (essential — leaving it up costs GLM)
ray down golem-cluster.yaml
```

> **⚠️ Always run `ray down` when finished.** A live cluster keeps Providers rented and accrues GLM cost until the budget runs out.

## Minimal example Python

```python
import ray
ray.init(address="auto")             # connects to the cluster head

@ray.remote
def square(x):
    return x * x

futures = [square.remote(i) for i in range(100)]
print(ray.get(futures))
```

Run via `ray submit golem-cluster.yaml example.py`.

## Mainnet config

Change in `golem-cluster.yaml`:

```yaml
provider:
  parameters:
    payment_network: polygon
    budget: 20.0                     # cap real GLM spend
```

And ensure `yagna payment fund --network=polygon` has been run once on the host. See `references/yagna/networks.md` and `references/mainnet-migration.md`.

## Gotchas

- `image_tag` must match a `.gvmi` that has Ray pre-installed. Use the official `golem/ray-on-golem:py3.10` (or matching Python version) — building your own from scratch is rarely worth it for Ray.
- **Cluster spin-up is slow** — first time can take a few minutes per node. Cache models / weights inside the `.gvmi` to avoid re-downloading on each `ray up`.
- Ray's autoscaler is conservative; bursty workloads may want `upscaling_speed: 5` or higher.
- Logs live both on the head node (via `ray dashboard`) and on Golem's yagna log — check both when debugging.

Source: https://docs.golem.network/docs/creators/ray — Last verified: 2026-05-13
