# Docker (GPU)

This repository includes a `Dockerfile` for building an NVIDIA-GPU-enabled image that bundles:
 - `lc0` engine (built from source)
 - `lc0-training-client` (downloaded from GitHub releases)

The container expects a single persistence mount at `/data`:
 - `/data/config` (XDG config home)
 - `/data/cache`  (XDG cache home)

Build:

    docker build -t lc0-training-client:test .

Test (no GPU required):

    docker run --rm lc0-training-client:test --help
    docker run --rm --entrypoint /app/lc0 lc0-training-client:test --help

Run (persist config/cache on host):

    mkdir -p ~/.lc0-training
    docker run --gpus all \
      --user $(id -u):$(id -g) \
      -v ~/.lc0-training:/data \
      lc0-training-client:test \
      --user=USERNAME --password=PASSWORD

Override versions:

    docker build -t lc0-training-client:test \
      --build-arg LC0_VERSION=v0.32.1 \
      --build-arg CLIENT_VERSION=v34 \
      .
