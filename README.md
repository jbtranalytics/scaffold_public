# scaffold_public

This repository/folder contains the **public** Docker image for the Scaffold monorepo. The image is built from `Dockerfile.public`, which installs the **Python 3.14** runtime and all production dependencies using **uv**. It does **not** contain any of your application source code.

## How it works

1. **CI workflow** – `.github/workflows/build-public.yml` automatically builds the image on every push to `main` (or when triggered manually) and pushes it to the GitHub Container Registry (GHCR) under the name:
   ```
   ghcr.io/<owner>/base-public:latest
   ```
   Replace `<owner>` with your GitHub account or organization name, or let the workflow use `${{ github.repository_owner }}`.

2. **Public image** – The image is published **publicly**, so anyone can pull it without authentication and without any data‑transfer quota.

## Building locally (optional)

If you want to build the image locally for testing, run:
```bash
cd /home/josht/src/scaffold_public
docker build -f Dockerfile.public -t base-public:latest .
```
You can then run a container:
```bash
docker run --rm -it base-public:latest python --version
```

## Next steps

- Ensure the `Dockerfile.public` is present in this folder. The provided `copy_dockerfiles.sh` script will copy it from the main monorepo.
- Add any additional OS packages you need in the `RUN apt-get install …` line of `Dockerfile.public`.
- If you want to change the image name, edit the `tags:` line in the CI workflow.

---
*This folder follows the project’s architecture guidelines: it contains only the Dockerfile and CI workflow; all runtime code lives in the core monorepo.*
