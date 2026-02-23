<p align="center">
  <img src="assets/logo.png" width="120" alt="Bug Bounty Center" />
</p>

<h1 align="center">Bug Bounty Center</h1>

<p align="center">
  A private, local-first workspace for bug bounty hunters.<br/>
  Track programs, manage targets, document findings, and generate reports — all from your machine.
</p>

<p align="center">
  <a href="https://github.com/Cyph3R-csec/Bug-Bounty-Center-Deploy/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" /></a>
  <a href="https://ghcr.io/cyph3r-csec/bug-bounty-center"><img src="https://img.shields.io/badge/docker-ghcr.io-blue.svg" alt="Docker" /></a>
  <a href="https://bugbountycenter.com"><img src="https://img.shields.io/badge/website-bugbountycenter.com-emerald.svg" alt="Website" /></a>
</p>

<p align="center">
  <a href="https://bugbountycenter.com">Website</a> ·
  <a href="https://bugbountycenter.com/#features">Features</a> ·
  <a href="https://bugbountycenter.com/#pricing">Pricing</a> ·
  <a href="https://bugbountycenter.com/#install">Install</a>
</p>

---

## What is Bug Bounty Center?

Bug Bounty Center is a self-hosted workspace built for security researchers who participate in bug bounty programs. It runs locally via Docker — your data never leaves your machine.

Instead of juggling spreadsheets, text files, and scattered notes, you get a single interface to manage your entire hunting workflow: from recon and target tracking to vulnerability documentation and report generation.

---

## Quick Start

### Requirements

- [Docker](https://docs.docker.com/get-docker/) installed and running
- 2 GB of available RAM
- Linux, macOS, or Windows

### Option A — Docker Compose (recommended)

```bash
mkdir bugbounty && cd bugbounty
curl -O https://raw.githubusercontent.com/Cyph3R-csec/Bug-Bounty-Center-Deploy/main/docker-compose.yml
docker compose up -d
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

> The included `docker-compose.yml` applies security hardening by default. See the [Security](#security) section for details.

### Option B — Docker Run

```bash
docker run -d \
  --name bugbounty-app \
  -p 127.0.0.1:3000:3000 \
  -v bugbounty-data:/app/data \
  --read-only \
  --tmpfs /tmp:noexec,nosuid,size=64m \
  --tmpfs /app/.next/cache:noexec,nosuid,size=256m \
  --cap-drop ALL \
  --security-opt no-new-privileges:true \
  --restart unless-stopped \
  ghcr.io/cyph3r-csec/bug-bounty-center:latest
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## Features

Bug Bounty Center includes **33+ features** built for the complete hunting workflow:

| Category | Highlights |
|----------|-----------|
| **Program Management** | Track programs, scopes, targets, and subdomains |
| **Vulnerability Tracking** | Document findings with severity, status, and screenshots |
| **Recon & Analysis** | JS analyzer, attack surface graphs, mind maps |
| **Productivity** | Focus timer, hunting streaks, scheduling, checklists |
| **Reporting** | Draft and export professional vulnerability reports |
| **Credentials Vault** | Store API keys and tokens locally with encryption |
| **Mental Health** | Mood tracking and break reminders for long sessions |
| **Security** | Password protection, audit logging, hardened Docker config |

Full feature list at [bugbountycenter.com](https://bugbountycenter.com/#features).

---

## Updating

Pull the latest image and recreate the container:

```bash
docker compose pull
docker compose up -d
```

Your data is stored in a persistent Docker volume and is preserved across updates.

---

## Backup & Restore

### Backup

Your data lives in the `bugbounty-data` Docker volume. To create a backup:

```bash
docker run --rm \
  -v bugbounty-data:/data \
  -v $(pwd):/backup \
  alpine tar czf /backup/bugbounty-backup.tar.gz -C /data .
```

This creates a `bugbounty-backup.tar.gz` file in your current directory.

### Restore

To restore from a backup:

```bash
docker compose down
docker run --rm \
  -v bugbounty-data:/data \
  -v $(pwd):/backup \
  alpine sh -c "rm -rf /data/* && tar xzf /backup/bugbounty-backup.tar.gz -C /data"
docker compose up -d
```

---

## Data & Privacy

- **100% local** — runs entirely on your machine, no cloud dependency
- **Zero telemetry** — no analytics, no tracking, no data collection
- **Your data stays yours** — stored in a Docker volume on your disk
- **Offline capable** — no internet connection required after installation

---

## Security

The included `docker-compose.yml` applies the following hardening out of the box:

| Measure | Description |
|---------|-------------|
| **Localhost binding** | Binds to `127.0.0.1` — not accessible from your local network |
| **Read-only filesystem** | Root filesystem is mounted read-only |
| **No capabilities** | All Linux capabilities are dropped |
| **No privilege escalation** | `no-new-privileges` prevents setuid binaries |
| **Resource limits** | Memory capped at 2 GB, max 256 processes |
| **Log rotation** | Prevents log files from exhausting disk space |

---

## Troubleshooting

<details>
<summary><strong>Port 3000 is already in use</strong></summary>

Edit the port mapping in `docker-compose.yml`:

```yaml
ports:
  - "127.0.0.1:8080:3000"
```

Then access the app at `http://localhost:8080`.

</details>

<details>
<summary><strong>Container won't start</strong></summary>

Check the container logs for errors:

```bash
docker compose logs -f
```

Common causes:
- Docker is not running — start Docker Desktop or the Docker daemon
- Insufficient memory — make sure at least 2 GB of RAM is available
- Port conflict — see the troubleshooting entry above

</details>

<details>
<summary><strong>Permission denied errors</strong></summary>

If you see permission errors on Linux, make sure your user is in the `docker` group:

```bash
sudo usermod -aG docker $USER
```

Log out and back in for the change to take effect.

</details>

<details>
<summary><strong>Reset the application</strong></summary>

This removes all your data and starts fresh:

```bash
docker compose down -v
docker compose up -d
```

> **Warning:** This permanently deletes all your data. Make a backup first if needed.

</details>

---

## Uninstall

Stop the container and remove all associated data:

```bash
docker compose down -v
```

To also remove the downloaded image:

```bash
docker rmi ghcr.io/cyph3r-csec/bug-bounty-center:latest
```

---

## License

The deployment configuration in this repository is released under the [MIT License](LICENSE).

Bug Bounty Center is a commercial product. Visit [bugbountycenter.com](https://bugbountycenter.com/#pricing) for pricing details.
