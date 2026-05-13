# `gvmkit-build` — custom Golem VM images

`gvmkit-build` converts a **Docker image** into the `.gvmi` format that Golem Providers can run. Use it when the stock images on the Golem Registry don't carry the binaries your workload needs (FFmpeg, Whisper, scientific libs, custom ML models, etc.).

## When to use it vs. stock images

| Workload | Recipe |
|---|---|
| Trivial shell on Linux | `golem/alpine:latest` (stock) — no build needed |
| Python with stdlib | `golem/python:3.11` (stock) — no build needed |
| FFmpeg / Whisper / OpenCV | Build a custom image |
| Custom Node.js app with deps | Build a custom image (or use `npm install` at runtime) |
| ML model weights baked in | Build a custom image |

## Install

```bash
npm install -g @golem-sdk/gvmkit-build
# or as a dev dependency
npm install --save-dev @golem-sdk/gvmkit-build
```

Requires Docker (or a Docker-compatible runtime like OrbStack / Colima / Podman with the `docker` shim) on the build machine.

## Authoring the Dockerfile

Any Linux Docker image works. Keep it lean — every byte slows down Provider download:

```dockerfile
FROM alpine:3.20

RUN apk add --no-cache ffmpeg python3 py3-pip

WORKDIR /golem
COPY app/ /golem/app/

VOLUME /golem/output

CMD ["/bin/sh"]
```

**Conventions**:
- Set `WORKDIR /golem` — SDK examples assume this.
- Use `VOLUME` for any input/output dir you'll write to from the Provider side.
- Don't include secrets — the image is uploaded to a public registry.
- Prefer `apk` (Alpine) or slim base images. Final size budget: **< 200 MB** for fast provisioning.

## Build & convert

```bash
# Build the Docker image locally
docker build -t my-workload .

# Convert to .gvmi
gvmkit-build my-workload
```

Output: `my-workload-<hash>.gvmi` in the working directory.

## Push to the Golem Registry

```bash
gvmkit-build my-workload --push
```

After upload completes, the tool prints both:

- An **image hash**: `sha3:abcd1234...` — use with yapapi (`vm.repo(image_hash=...)`)
- An **image tag**: `username/repo:latest` — use with the JS SDK (`imageTag: "username/repo:latest"`)

Save both. Hash is immutable; tag can be re-pointed.

## Use the image

### JS SDK

```js
const order = {
  demand: { workload: { imageTag: "username/repo:latest" } },
  // ...
};
```

### Python (yapapi)

```python
payload = await vm.repo(image_hash="sha3:abcd1234...")
```

## Optimization tips

- **Multi-stage builds**: compile in a fat stage, copy artifacts into a slim final stage.
- **Cache wheels / npm**: use BuildKit layer caching to avoid re-downloading deps each build.
- **Hash, don't tag, in prod**: pinning to a hash avoids silent drift if you re-push `:latest`.
- **Verify locally**: run `docker run --rm -v ./out:/golem/output my-workload <your-cmd>` before pushing.

## Common errors

- **`unknown command gvmkit-build`** → not on PATH. Re-install or use `npx @golem-sdk/gvmkit-build`.
- **`Docker daemon not running`** → start Docker Desktop / OrbStack / Colima before `gvmkit-build`.
- **`Image too large`** → trim deps; aim for < 200 MB. Some Providers reject huge images.
- **`No providers offering imageTag`** → tag misspelled or never pushed. Re-run with `--push`. Cross-check at the Golem Registry.

## Registry

The Golem Registry is the public image catalog: https://registry.golem.network. You can browse what others have published before building your own — many common stacks already exist.

Source: https://docs.golem.network/docs/creators/tools/gvmkit — Last verified: 2026-05-13
