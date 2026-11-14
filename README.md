# bottle-public-images

Publishing vehicle for the **public duplicates** of the Bottle CRM container
images. Packages published by this repo's workflow:

- `ghcr.io/cicadialabs/bottle-backend-public`
- `ghcr.io/cicadialabs/bottle-frontend-public`

The originals (`ghcr.io/cicadialabs/bottle-backend`,
`ghcr.io/cicadialabs/bottle-frontend`) remain **private** and are untouched.

## Usage

Run the **Mirror Bottle images to public packages** workflow
(Actions → Run workflow) with the tag to publish.

The workflow copies the source image **pinned by manifest digest** using
`skopeo copy --all` (multi-arch preserved, byte-identical) and fails the run
if the pushed digest differs from the source digest.

## Secrets

| Secret | Purpose |
|---|---|
| `MIRROR_GHCR_USER` | GitHub username that owns the pull token |
| `MIRROR_GHCR_TOKEN` | Classic PAT with `read:packages`, used only to pull the private source images from GHCR |

Push to the public `-public` packages uses the workflow's own `GITHUB_TOKEN`
(`permissions: packages: write`).
