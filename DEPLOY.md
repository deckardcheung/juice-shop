# Deploy notes (this fork)

This fork builds and publishes a Docker image to GitHub Container Registry (GHCR) without needing Docker locally.

## CI/CD

- Workflow: [`.github/workflows/ghcr.yml`](.github/workflows/ghcr.yml)
- **Pull requests** (into `master`): build only (no push) to verify the image
- **Push to `master`**: build and push to GHCR with tags `:latest` and short commit SHA
- **Tag push `v*`**: build and push with the version tag (plus SHA)

Watch runs: https://github.com/deckardcheung/juice-shop/actions

## Image

```text
ghcr.io/deckardcheung/juice-shop:latest
ghcr.io/deckardcheung/juice-shop:<short-sha>
```

## Permissions you may need to enable

1. **Repo → Settings → Actions → General → Workflow permissions**
   - Set to **Read and write permissions** (so `GITHUB_TOKEN` can publish packages)
   - Optionally allow GitHub Actions to create/approve pull requests if you use other workflows
2. **Packages**: after the first successful push, open the package under your profile **Packages**, set visibility (public/private) as needed, and link it to this repository if prompted

Upstream `ci.yml` / `release.yml` only publish Docker Hub images for `juice-shop/juice-shop`; they do not publish this fork to GHCR.

## Cloud Run

Deploy to Cloud Run (or another host) comes later — pull the GHCR image once the workflow has produced `:latest`.
