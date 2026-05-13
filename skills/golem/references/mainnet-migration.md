# Mainnet migration — pre-flight checklist

Moving a requestor from **hoodi testnet** (free tGLM) to **mainnet** (real GLM) is the single highest-stakes change in a Golem project. This checklist exists to prevent surprise spend.

> **Default recommendation: use `polygon`, not `mainnet`.** Ethereum mainnet has high gas; Polygon has near-zero gas for the same GLM-denominated payments.

## Pre-flight checklist

Run through this list **in order**. Do not skip steps.

### 1. Confirm intent with the user

The user must explicitly say "switch to mainnet" or "deploy to mainnet". A "yes, run it" in response to a previous testnet command is **not** authorization for mainnet.

### 2. Estimate worst-case spend

For the order config you intend to ship:

```
worst_case_GLM = (maxStartPrice + (maxCpuPerHourPrice + maxEnvPerHourPrice) × rentHours) × poolSize × N_runs
```

Multiply by 1.5× as a safety margin. Show this number to the user and get explicit confirmation.

### 3. Acquire GLM in the wallet

```bash
yagna id show
```

Send GLM to the printed address from an exchange or DEX. On Polygon, transfer GLM on the Polygon network (don't bridge from Ethereum until you've confirmed the bridge logistics — wrong-chain GLM is hard to recover).

Verify:

```bash
yagna payment status --network=polygon
```

Balance should show `amount_available > 0`.

### 4. Initialize the mainnet payment account

```bash
yagna payment fund --network=polygon
```

This is **not** a faucet — it only ensures the account is registered on-chain. The GLM you sent in step 3 is what funds activity.

### 5. Update the SDK order

```js
const order = {
  // ...existing demand and market...
  payment: { network: "polygon" },           // ← add this
};
```

For Ray:

```yaml
provider:
  parameters:
    payment_network: polygon
```

For yapapi:

```python
async with Golem(budget=10.0, payment_network="polygon") as golem:
    ...
```

### 6. Lower pricing ceilings AGGRESSIVELY for first run

Testnet ceilings can be loose because tGLM is free. On mainnet, start very low:

```js
pricing: {
  model: "linear",
  maxStartPrice: 0.01,
  maxCpuPerHourPrice: 0.05,
  maxEnvPerHourPrice: 0.01,
},
```

If "no providers found", raise incrementally — but get to the lowest viable price.

### 7. Smoke-test with a single task

Don't run a full batch on first mainnet contact. Run one tiny task first:

- `poolSize: { min: 1, max: 1 }`
- A trivial command like `echo "hello"` or `uname -a`
- `rentHours: 0.1`

Verify the invoice comes in, payment settles, balance decreases.

### 8. Scale gradually

After the smoke test succeeds, scale `poolSize` and `data.length` step-by-step. Watch `yagna payment status --network=polygon` between batches.

### 9. Plan for cleanup

For any long-running rental (Ray cluster, Dapps deployment): document the **stop command** and the **idempotency** of running it. Stale clusters bleed GLM.

## Rollback

Mainnet runs are not reversible — GLM spent is gone. The "rollback" is to:

1. Stop the requestor process.
2. `glm.disconnect()` / `executor.shutdown()` / `ray down` to release rentals.
3. Verify `yagna payment status --network=polygon` shows no locked Allocation.
4. Wait for any in-flight invoices to settle (usually < 1 min).

## Hard rules

- **Never run a mainnet operation in a loop without a wall-clock budget guard.**
- **Never deploy `--network=mainnet`** (Ethereum) without explicit user approval — Polygon is the default mainnet for Golem.
- **Never strip cost ceilings** from `order.market.pricing` on mainnet "to find providers". Find them another way (raise the ceiling slightly, change image, expand search) — never go unbounded.
- **Always have the stop command ready** before starting a mainnet run.

Source: https://docs.golem.network/docs/creators/javascript/guides/switching-to-mainnet — Last verified: 2026-05-13
