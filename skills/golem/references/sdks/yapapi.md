# `yapapi` — Python SDK

The Python SDK for Golem Network. Mirrors the JS SDK's concepts (Market, Activity, ExeUnit) but in idiomatic Python `async` style.

## When to reach for it

- The user's existing stack is Python and porting to JS is not viable (heavy numeric / ML deps, lab code).
- Per-task glue is in Python; the workload itself runs in a Python image on the Provider.

For most new projects, the JS SDK is the better-documented and more actively maintained surface. If you want Python **at scale**, prefer **Ray on Golem** (`references/frameworks/ray-on-golem.md`) — it gives true distributed-Python semantics on top of Golem.

## Install

```bash
pip install yapapi
```

Requires Python 3.8+ and a running yagna daemon (`yagna service run`).

## Minimal pattern

```python
import asyncio
from yapapi import Golem, Task
from yapapi.payload import vm

async def worker(ctx, tasks):
    async for task in tasks:
        ctx.run("/bin/echo", f"processing {task.data}")
        output = yield ctx.commit()
        task.accept_result(result=output)

async def main():
    payload = await vm.repo(
        image_hash="<image-hash-from-golem-registry>",
    )
    async with Golem(budget=1.0, subnet_tag="public") as golem:
        async for completed in golem.execute_tasks(
            worker,
            [Task(data=i) for i in range(5)],
            payload=payload,
        ):
            print("Done:", completed.result)

asyncio.run(main())
```

## Concept mapping (JS ↔ Python)

| JS SDK | Python (yapapi) |
|---|---|
| `GolemNetwork` | `Golem` |
| `order.demand.workload.imageTag` | `vm.repo(image_hash=...)` |
| `manyOf` / pool | `golem.execute_tasks(...)` |
| `exe.run("...")` | `ctx.run("/bin/...", ...)` then `yield ctx.commit()` |
| `pricing.maxStartPrice` etc. | `budget=` (single ceiling) |

## Gotchas

- yapapi historically used `image_hash` (not `imageTag`) — fetch the hash from the Registry via `gvmkit-build push` output. See `references/images/gvmkit-build.md`.
- `subnet_tag="public"` is the default network; testnet/mainnet selection happens via yagna's payment platform, not the SDK call.
- yapapi is less actively iterated than the JS SDK. Always cross-check the current README at https://github.com/golemfactory/yapapi before architectural decisions.

## When to NOT use yapapi

- If the workload is naturally Python-distributed: use **Ray on Golem**.
- If team JS skills exist: use the JS SDK and call out to Python via the Provider's image (i.e. ship a Python `.gvmi` and `exe.run("python script.py")`).

Source: https://github.com/golemfactory/yapapi — Last verified: 2026-05-13
