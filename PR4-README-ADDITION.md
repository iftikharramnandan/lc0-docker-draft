# README.md Docker Section

Add this section to README.md after the "Running" section (around line 277, before "# Cross-compiling"):

---

# Docker (GPU)

See [`docs/DOCKER.md`](docs/DOCKER.md) for the full guide on running the official GPU Docker image and the host-side auto-updater script.

Quick start:

    mkdir -p ~/.lc0-training
    docker run --gpus all \
      --user $(id -u):$(id -g) \
      -v ~/.lc0-training:/data \
      ghcr.io/leelachesszero/lc0-training-client:latest \
      --user=USERNAME --password=PASSWORD

---

## Git commands for PR4

```bash
# Make script executable in git
git add --chmod=+x scripts/auto-update.sh

# Add all PR4 files
git add scripts/auto-update.sh docs/DOCKER.md

# Edit README.md to add the Docker section above, then:
git add README.md
```

## TODO (pre-merge checklist)

Before merging to production:

1. **In `docs/DOCKER.md`**: Change the download URL from raw GitHub to releases:
   ```bash
   # FROM (testing):
   curl -fLO https://raw.githubusercontent.com/LeelaChessZero/lczero-client/master/scripts/auto-update.sh

   # TO (production):
   curl -fLO https://github.com/LeelaChessZero/lczero-client/releases/latest/download/auto-update.sh
   ```

2. **In `.github/workflows/docker-publish.yml`**: Uncomment the asset upload step at the bottom of the file.
