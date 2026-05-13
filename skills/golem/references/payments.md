# Payments, allocations, and GLM accounting

Golem uses a **pay-as-you-go** model. Requestors lock GLM in an Allocation, Providers issue debit notes and invoices, yagna settles them automatically on the configured payment platform.

## Core concepts

| Term | Meaning |
|---|---|
| **GLM** | ERC-20 mainnet payment token (Ethereum / Polygon) |
| **tGLM** | Testnet equivalent (no monetary value) |
| **Payment Platform** | `(token, network, driver)` — e.g. `(GLM, polygon, erc20)` |
| **Allocation** | Locked GLM reserved to pay invoices for a specific budget |
| **Debit Note** | Mid-agreement interim charge from a Provider |
| **Invoice** | Final charge from a Provider at agreement termination |
| **Payment Driver** | Code that executes on-chain transfers (default: `erc20`) |

## Payment Platform tuple

Every order targets one Payment Platform. The default for testnet:

```
GLM × hoodi × erc20
```

For mainnet (recommended):

```
GLM × polygon × erc20
```

For mainnet (Ethereum, high gas):

```
GLM × mainnet × erc20
```

Set in the order: `payment: { network: "polygon" }` (JS SDK).

## How payment flows

1. **Allocation created** — when your SDK starts a session, yagna locks an amount of GLM as an Allocation. This is *your* upper bound for that run.
2. **Agreement signed** — Provider accepts; both sides commit to terms.
3. **Activity runs** — Provider executes your commands.
4. **Debit notes** — Provider can issue periodic interim charges (configurable). yagna deducts from the Allocation.
5. **Activity ends** — final Invoice. yagna pays from remaining Allocation balance.
6. **Allocation released** — leftover GLM returns to your spendable balance.

## Sizing allocations

The SDK auto-creates an allocation sized to `rentHours × pricing-ceilings × poolSize`. Always set explicit ceilings in `order.market.pricing`:

```js
market: {
  rentHours: 0.5,
  pricing: {
    model: "linear",
    maxStartPrice: 0.05,
    maxCpuPerHourPrice: 0.2,
    maxEnvPerHourPrice: 0.05,
  },
}
```

Worst-case spend ≈ `(maxStartPrice + (maxCpuPerHourPrice + maxEnvPerHourPrice) × rentHours) × poolSize`. Compute this before mainnet.

## Inspect payment state

```bash
yagna payment status                          # default network
yagna payment status --network=polygon

yagna payment accounts                        # list configured payment platforms
yagna payment invoices                        # list invoices (paid + unpaid)
yagna payment debit-notes                     # list debit notes
```

## Batching (cost optimization on mainnet)

Each on-chain transfer costs gas. yagna can batch transfers via `ERC20_SENDOUT_INTERVAL_SECS`:

```bash
export ERC20_SENDOUT_INTERVAL_SECS=3600    # send hourly
```

Earlier transfers happen if any Provider's payment deadline forces them. On Polygon, gas is cheap enough that batching matters less; on Ethereum mainnet, it's important.

## Provider-side (for context)

Providers configure their payment network via `golemsp run --payment-network <network>`. As a requestor, you don't run this — but if you're debugging a "no providers found" issue, mismatched networks on the two sides is a common cause.

## Refunds and disputes

There is no automated dispute mechanism. If a Provider misbehaves (doesn't deliver, returns garbage), the protocol still charges you for the rented time. Mitigations:

- Use `offerProposalFilter` to scope to reputed Providers.
- Set short `rentHours` and validate output before extending.
- For mainnet, start with low-value pilots before scaling.

## Common errors

- **"Insufficient allocation"** → balance too low for the order. Fund more or lower ceilings.
- **"Payment platform not initialized"** → run `yagna payment fund --network=<name>` once on the host.
- **"Allocation released early"** → SDK cleanup ran but agreement was still active. Check that `glm.disconnect()` / `executor.shutdown()` is awaited.

Source: https://docs.golem.network/docs/golem/payments — Last verified: 2026-05-13
