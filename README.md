<p align="center">
  <img src="https://bugbountycenter.com/icon.png" width="80" alt="Bug Bounty Center" />
</p>

<h1 align="center">Bug Bounty Center</h1>

<p align="center">
  A private, local-first workspace for bug bounty hunters and security researchers.<br/>
  Track programs, manage targets, document findings, and generate reports — all from your machine.
</p>

<p align="center">
  <a href="https://bugbountycenter.com">Website</a> ·
  <a href="https://bugbountycenter.com/#features">Features</a> ·
  <a href="https://bugbountycenter.com/#pricing">Pricing</a> ·
  <a href="https://bugbountycenter.com/#faq">FAQ</a>
</p>

---

## Quick Start

### Requirements

- [Docker](https://docs.docker.com/get-docker/) installed and running
- 2 GB of available RAM
- Any OS that supports Docker (Linux, macOS, Windows)

### Option A — Docker Compose (recommended)

```bash
mkdir bugbounty && cd bugbounty
curl -O https://raw.githubusercontent.com/Cyph3R-csec/bug-bounty-center-deploy/main/docker-compose.yml
docker compose up -d
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Option B — Docker Run

```bash
docker run -d \
  --name bugbounty-app \
  -p 127.0.0.1:3000:3000 \
  -v bugbounty-data:/app/data \
  --restart unless-stopped \
  ghcr.io/cyph3r-csec/bug-bounty-center:latest
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## Features

Bug Bounty Center includes **33+ features** designed for the complete hunting workflow:

| Category | Highlights |
|----------|-----------|
| **Program Management** | Track programs, scopes, targets, and subdomains |
| **Vulnerability Tracking** | Document findings with severity, status, and evidence |
| **Recon & Analysis** | JS analyzer, attack surface graphs, mind maps |
| **Productivity** | Focus timer, hunting streaks, scheduling, checklists |
| **Reporting** | Draft and export professional reports |
| **Security** | Password protection, credentials vault, audit logging |

Full feature list at [bugbountycenter.com/#features](https://bugbountycenter.com/#features).

---

## Updating

Pull the latest image and restart:

```bash
docker compose pull
docker compose up -d
```

Your data is stored in a Docker volume and persists across updates.

---

## Data & Privacy

- **100% local** — the app runs entirely on your machine
- **Zero telemetry** — no data is sent anywhere, ever
- **Your data stays yours** — stored in a local Docker volume (`bugbounty-data`)
- **Offline capable** — no internet connection required after installation

---

## Security

The included `docker-compose.yml` applies the following hardening:

- Binds to `127.0.0.1` only (not accessible from your network)
- Read-only root filesystem
- All Linux capabilities dropped
- Privilege escalation disabled
- Memory and process limits enforced
- Log rotation enabled

---

## Troubleshooting

**Port 3000 already in use**

Change the port mapping in `docker-compose.yml`:

```yaml
ports:
  - "127.0.0.1:8080:3000"
```

Then access the app at `http://localhost:8080`.

**Container won't start**

Check logs:

```bash
docker compose logs -f
```

**Reset the application**

Remove the data volume (this deletes all your data):

```bash
docker compose down -v
docker compose up -d
```

---

## Uninstall

```bash
docker compose down -v
```

This stops the container and removes all associated data.

---

## License

This deployment configuration is released under the [MIT License](LICENSE).

Bug Bounty Center is a commercial product. See [pricing](https://bugbountycenter.com/#pricing) for details.
