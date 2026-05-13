# yagna — networks (testnet ↔ mainnet)

Golem supports several **payment networks**. A network is one part of a Payment Platform tuple `(token, network, driver)` — for example, `(GLM, polygon, erc20)`.

## Supported networks

| Network | Type | Token | Notes |
|---|---|---|---|
| `hoodi` | Testnet | tGLM | **Default** for new installs |
| `sepolia` | Testnet | tGLM | Alternative testnet |
| `polygon` | Mainnet | GLM | **Recommended for production** — low gas |
| `mainnet` | Mainnet | GLM | Ethereum mainnet — high gas |

Historical testnets (`rinkeby`, `goerli`, `amoy`) may appear in older docs — they are mostly deprecated. Default to `hoodi` for testnet.

## Check current state

```bash
yagna payment status                       # default network
yagna payment status --network=polygon     # specific network
```

## Fund testnet (free tGLM)

```bash
yagna payment fund                         # defaults to hoodi
yagna payment fund --network=sepolia       # explicit testnet
```

This calls the network's faucet. Re-run when your balance is low.

## Fund / init mainnet (REAL MONEY)

> **⚠️ Before running these commands, confirm with the user. These initialize accounts that will spend real GLM.**

```bash
yagna payment fund --network=polygon       # recommended
yagna payment fund --network=mainnet       # Ethereum (high gas)
```

For mainnet you must already own GLM in the identity's wallet — there is no faucet. `yagna payment fund` here only ensures the account is initialized on-chain; it does not give you tokens.

## Buy GLM (mainnet)

GLM is an ERC-20 token. Acquire it on any major exchange (Bitfinex, KuCoin, etc.) or DEX (Uniswap, QuickSwap on Polygon). Transfer to the address shown by `yagna id show`.

## Switch the SDK to a different network

The yagna daemon can talk to multiple networks at once. The selection happens **in your requestor code**:

### JS SDK (golem-js / task-executor)

```js
const order = {
  demand: { workload: { imageTag: "golem/alpine:latest" } },
  market: { rentHours: 1, pricing: {...} },
  payment: { network: "polygon" },          // ← here
};
```

Combined with `yagna payment fund --network=polygon` once on the host.

### Python (yapapi)

```python
async with Golem(budget=10.0, payment_network="polygon") as golem:
    ...
```

### Ray on Golem

In the cluster YAML:

```yaml
payment_network: "polygon"
```

## Verifying which network a session will use

```bash
yagna payment status --network=polygon
```

Should show `amount_locked` / `amount_available` for the network you intend to use. If the network shows `not initialized`, run `yagna payment fund --network=<name>` first.

## Common errors

- **"Allocation refused — insufficient funds"** → balance too low for the order's `rentHours × pricing`. Fund more or lower the order ceilings.
- **"No providers found"** → the network might have low provider density; or your pricing is below market floor. Raise `maxStartPrice` / `maxCpuPerHourPrice` slightly. See `references/common-errors.md`.
- **"Payment platform unsupported"** → SDK and yagna versions out of sync; upgrade yagna.

Source: https://docs.golem.network/docs/creators/javascript/guides/switching-to-mainnet — Last verified: 2026-05-13
