<p align="center">
  <a href="https://github.com/composebox/composebox">
    <img src="https://raw.githubusercontent.com/composebox/.github/main/profile/assets/logo.svg" alt="Composebox Logo" width="96" />
  </a>
</p>

<h1 align="center">Composebox</h1>

<p align="center">
  <strong>Lightweight, single-binary container management tools for self-hosters and modern homelabs.</strong>
</p>

<p align="center">
  <a href="https://github.com/composebox/composebox/releases"><img src="https://img.shields.io/github/v/release/composebox/composebox?style=flat-square&color=0284c7" alt="Release"></a>
  <a href="https://golang.org"><img src="https://img.shields.io/badge/go-1.26+-00ADD8?style=flat-square&logo=go" alt="Go Version"></a>
  <a href="https://github.com/composebox/composebox/pkgs/container/composebox"><img src="https://img.shields.io/badge/docker-ghcr.io%2Fcomposebox%2Fcomposebox-blue?style=flat-square&logo=docker" alt="Container Image"></a>
  <a href="https://github.com/composebox/composebox/blob/master/LICENSE"><img src="https://img.shields.io/badge/license-MIT-38bdf8?style=flat-square" alt="License: MIT"></a>
</p>

---

### Welcome to Composebox

Composebox is dedicated to building minimalist, high-performance developer tools for managing Docker Compose stacks without the operational bloat of traditional heavyweight orchestrators.

### Core Philosophy

* **Single Static Binary:** Bundles a high-performance Go daemon with Svelte 5 & Tailwind CSS v4 assets into a single standalone binary (`//go:embed`). No Node.js runtime, no complex dependencies.
* **Filesystem-as-Database:** Your directory tree is the source of truth (`1 directory = 1 stack`). Direct YAML and `.env` editing with zero proprietary database layers or synchronization drift.
* **Defense-in-Depth:** Engineered for production safety: runs non-root (`USER 1001:1001`), enforces strict Origin/Referer CSRF guards, and uses `.trash/` archival instead of destructive file deletion.
* **Zero Raw Socket Exposure:** First-class compatibility with [`docker-socket-proxy`](https://github.com/composebox/composebox/blob/master/docker-compose.hardened.yml) and Rootless Docker (`/run/user/1000/docker.sock`) for environments that demand least privilege.
* **Zero Telemetry & 100% Offline:** Fully self-contained. No background tracking, no phoning home, and 100% air-gap ready.

---

### Quick Start

Deploy Composebox in seconds with standard Docker Compose:

```yaml
services:
  composebox:
    image: ghcr.io/composebox/composebox:latest
    container_name: composebox
    restart: unless-stopped
    ports:
      - "127.0.0.1:8080:8080"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /path/to/your/stacks:/stacks
    environment:
      - STACKS_DIR=/stacks
      - PORT=8080
```

For security-conscious environments, see the [Hardened Socket-Proxy Deployment](https://github.com/composebox/composebox/blob/master/docker-compose.hardened.yml).
