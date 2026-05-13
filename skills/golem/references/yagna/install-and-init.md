# yagna — install and initialize

`yagna` is the **local daemon** every Golem requestor (and provider) talks to. It manages the wallet, payment platform, market negotiation, agreements, and the REST API your SDK uses. Without `yagna` running, no requestor script can do anything.

## Install (Linux / macOS)

```bash
curl -sSf https://join.golem.network/as-requestor | bash -
```

This installs the latest stable `yagna` and the `gftp` helper into `~/.local/bin` (or system-equivalent on macOS). Re-run later to upgrade.

**Windows**: use the official installer from https://github.com/golemfactory/yagna/releases — fetch the `yagna-windows-vX.Y.Z.zip` asset and extract to a directory on `PATH`.

## Verify install

```bash
yagna --version
which yagna
```

The binary should be on your `PATH`. If `which yagna` returns nothing on macOS, add the install dir to your shell rc (`export PATH="$HOME/.local/bin:$PATH"`).

## Initialize and run

```bash
# (Optional but recommended) Pre-create an app-key alias for autoconfig
export YAGNA_AUTOCONF_APPKEY=my_requestor

# Run the daemon (foreground)
yagna service run
```

`yagna service run` blocks the terminal. Keep it open in a dedicated window or run it via your system's process supervisor.

When it boots for the first time, yagna will autocreate an identity (a wallet) and — if `YAGNA_AUTOCONF_APPKEY` is set — generate an app-key with that name. The app-key value is what your SDK passes as `api.key`.

## Fund testnet tokens (hoodi)

In a separate terminal, with `yagna service run` still running:

```bash
yagna payment fund
```

This requests tGLM from the default testnet faucet and credits the requestor identity. Re-run anytime your balance is low.

## Check status

```bash
yagna id show                # current identity / wallet address
yagna payment status         # accrued / locked / available balances
yagna app-key list           # active app-keys
yagna net status             # P2P network status
```

## Log location

- Linux: `~/.local/share/yagna/yagna_rCURRENT.log`
- macOS: `~/Library/Application Support/GolemFactory.yagna/yagna_rCURRENT.log`
- Windows: `%LOCALAPPDATA%\GolemFactory\yagna\yagna_rCURRENT.log`

Tail these when debugging market or payment issues.

## Stop yagna

`Ctrl-C` in the `yagna service run` terminal. There is no separate "stop" command — yagna trapping SIGINT cleanly settles any open agreements.

## Versioning

Newer yagna releases bring SDK-protocol changes. If the JS SDK's `glm.connect()` returns a version-mismatch error, upgrade yagna by re-running the install one-liner. Keep yagna and the `@golem-sdk/*` packages in sync.

## Common pitfalls

- Running two `yagna service run` processes on the same host — they fight for the same ports. Run once.
- `yagna payment fund` without `yagna service run` already running → connection refused. Order matters.
- Firewalls blocking outbound P2P: yagna needs outbound TCP/UDP. On corp networks, this often fails silently — `yagna net status` will tell you.

Source: https://docs.golem.network/docs/creators/javascript/quickstarts/quickstart — Last verified: 2026-05-13
