# AGENTS.md

## Project Overview
Static single-page HTML tool ("Merge Octopus CSV Reports") that merges Octopus merchant settlement CSV files from emailed ZIP archives. All processing is client-side (browser-only) — no backend, no database, no build step.

## Tech Stack
- Single `index.html` file with inline JavaScript
- CDN-hosted libraries: Tailwind CSS, Font Awesome, zip.js (AES/ZipCrypto decryption), PapaParse (CSV parsing)
- No package.json, no dependencies to install

## Running in Base44 Sandbox
- `docker-compose.base44.yml` serves the static files via `nginx:alpine` on port 3000
- A custom `nginx.dev.conf` is mounted because the sandbox repo directory has restrictive (700) permissions; nginx runs as `user root` to read the bind-mounted files
- Source is bind-mounted read-only, so edits to `index.html` appear on browser refresh (no build step, no hot reload server)
- No external credentials or secrets required

## Verification
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` should return 200
- The page title is "Merge Octopus CSV Reports"
