# Track 3: Self-Hosting Software Stack for Beginners

## Summary

- **Docker + Docker Compose is the universal foundation** for self-hosting; virtually every recommended app ships a `docker-compose.yml`. Beginners should learn Compose before anything else. ([SSD Nodes guide](https://www.ssdnodes.com/blog/self-hosting-docker-compose/), [DoTheEvo GitHub](https://github.com/DoTheEvo/selfhosted-apps-docker))
- **Proxmox VE is the standard hypervisor** for home servers, letting you run VMs and LXC containers to isolate services. Tailscale has an official guide walking through Proxmox installation and integration. ([Tailscale blog](https://tailscale.com/blog/guide-self-hosting-proxmox))
- **Portainer or Dockge** provide a web UI for Docker container management, consistently recommended as the first thing beginners should install. ([Android Authority](https://www.androidauthority.com/best-open-source-self-hosting-apps-3602604/))
- **Caddy v2 is the easiest reverse proxy** for beginners (automatic HTTPS, simple config files); Traefik is the alternative with tighter Docker integration. Nginx Proxy Manager is a third option with a GUI. ([DoTheEvo GitHub](https://github.com/DoTheEvo/selfhosted-apps-docker), [Perfect Media Server](https://perfectmediaserver.com/04-day-two/top10apps/))
- **Tailscale (private access) and Cloudflare Tunnel (public access)** are complementary, not competing. Tailscale creates a WireGuard mesh VPN for personal device access; Cloudflare Tunnel exposes services publicly without port forwarding. Use both. ([XDA Developers](https://www.xda-developers.com/switching-from-cloudflare-tunnels-tailscale-hated-it/), [DEV Community](https://dev.to/mechcloud_academy/cloudflare-tunnel-vs-ngrok-vs-tailscale-choosing-the-right-secure-tunneling-solution-4inm))
- **Jellyfin** is the top media server pick (fully open-source, no subscription); Plex remains popular but has proprietary licensing concerns. ([Perfect Media Server](https://perfectmediaserver.com/04-day-two/top10apps/), [Android Authority](https://www.androidauthority.com/best-open-source-self-hosting-apps-3602604/))
- **Immich** is the consensus pick for self-hosted Google Photos replacement, with local ML-based face/object recognition. ([Perfect Media Server](https://perfectmediaserver.com/04-day-two/top10apps/), [Tailscale blog](https://tailscale.com/blog/guide-self-hosting-proxmox))
- **Home Assistant** is the dominant home automation platform with 3000+ integrations, local control, and privacy-first design. ([Perfect Media Server](https://perfectmediaserver.com/04-day-two/top10apps/), [Android Authority](https://www.androidauthority.com/best-open-source-self-hosting-apps-3602604/))
- **Vaultwarden** (lightweight Bitwarden server in Rust) is the standard self-hosted password manager, replacing cloud password services. ([DB Tech](https://dbtechreviews.com/2025/08/27/5-self-hosted-apps-i-use-every-day-in-my-homelab/), [Pinggy](https://pinggy.io/blog/best_self_hosted_apps/))
- **Pi-hole or AdGuard Home** for network-wide DNS ad blocking; AdGuard Home is increasingly preferred for its modern UI and DoH/DoT support. ([DB Tech](https://dbtechreviews.com/2025/08/27/5-self-hosted-apps-i-use-every-day-in-my-homelab/))
- **Nextcloud** is the most-mentioned self-hosted app across all sources (file sync, calendar, contacts, collaboration), though 2025 saw lighter alternatives like Sync-in emerge due to Nextcloud's resource hunger. ([Pinggy](https://pinggy.io/blog/best_self_hosted_apps/), [selfh.st](https://selfh.st/post/2025-favorite-new-apps/))
- **Paperless-NGX** (document OCR and management) and **Uptime Kuma** (service monitoring) round out the commonly recommended starter apps. ([Android Authority](https://www.androidauthority.com/best-open-source-self-hosting-apps-3602604/), [LowEndBox](https://lowendbox.com/blog/what-apps-should-you-be-self-hosting-is-2026/))
- **2025 trends**: Pangolin as a self-hosted Cloudflare Tunnel alternative, growing dissatisfaction with *arr suite leading to consolidation tools, and multiple Nextcloud-lighter alternatives. ([selfh.st](https://selfh.st/post/2025-favorite-new-apps/))

## Full Findings

### Infrastructure Layer: Hypervisor

**Proxmox VE** is the consensus hypervisor for home self-hosting. It runs on bare metal and provides both KVM virtual machines and LXC lightweight containers. Key advantages for beginners:
- Free and open-source (enterprise subscription optional)
- Web UI at `https://<ip>:8006` for all management
- Snapshot and backup capabilities built-in
- Proxmox VE Helper-Scripts community project simplifies post-install setup (disabling enterprise repos, subscription nags)
- Tailscale can run on the host, inside VMs, or in LXC containers

Source: [Tailscale self-hosting guide](https://tailscale.com/blog/guide-self-hosting-proxmox) walks through the full process: flash ISO with balenaEtcher, boot, set static IP, run helper scripts, update kernel.

### Infrastructure Layer: Containers

**Docker + Docker Compose** is the de facto standard. Every major self-hosted app provides a `docker-compose.yml`. The learning curve is modest:
- `docker-compose.yml` defines services, networks, and volumes declaratively
- `docker compose up -d` starts everything
- `.env` files separate configuration from compose files
- Named Docker networks provide automatic DNS resolution between containers

Management tools:
- **Portainer**: Most popular, full-featured web GUI for Docker. Good for beginners who want to avoid CLI.
- **Dockge**: Simpler alternative, focused on compose file management.
- **Dockpeek**: Dashboard providing clickable links to running containers.

Source: [SSD Nodes Docker Compose tutorial](https://www.ssdnodes.com/blog/self-hosting-docker-compose/), [DoTheEvo guide](https://github.com/DoTheEvo/selfhosted-apps-docker)

### Networking Layer

**Reverse Proxy** (required to route traffic to containers with HTTPS):
| Option | Best For | Key Feature |
|--------|----------|-------------|
| **Caddy v2** | Beginners | Automatic HTTPS, simplest config syntax |
| **Traefik** | Docker-heavy setups | Auto-discovers Docker containers via labels |
| **Nginx Proxy Manager** | GUI lovers | Web UI for proxy configuration |

**Remote Access / Tunneling**:

| Solution | Type | Best For | Free Tier |
|----------|------|----------|-----------|
| **Tailscale** | WireGuard mesh VPN | Private access from your devices | 3 users, 100 devices |
| **Cloudflare Tunnel** | Reverse tunnel | Public access without port forwarding | Unlimited bandwidth |
| **Pangolin** | Self-hosted tunnel | Those wanting to avoid Cloudflare dependency | Fully self-hosted |

Key insight from [XDA Developers](https://www.xda-developers.com/switching-from-cloudflare-tunnels-tailscale-hated-it/): Tailscale and Cloudflare Tunnel solve different problems. Tailscale is for private mesh networking (accessing your home server from your phone). Cloudflare Tunnel is for exposing services publicly (sharing a Jellyfin library with family). Many self-hosters run both.

**DNS-level ad blocking**:
- **Pi-hole**: The original, widely documented, large community
- **AdGuard Home**: Modern alternative with DNS-over-HTTPS/TLS, slightly better UI

### Application Layer: The Recommended Starter Stack

Based on frequency across all sources, here is the consensus beginner stack ordered by how often each app was recommended:

| App | Category | Mentioned In | Notes |
|-----|----------|-------------|-------|
| **Nextcloud** | Cloud/Files | 5 sources | Google Drive/Workspace replacement. Resource-heavy but feature-complete. |
| **Jellyfin** | Media Server | 5 sources | Fully FOSS Plex alternative. No account required, no telemetry. |
| **Immich** | Photo Management | 4 sources | Google Photos replacement with ML face/object search. Active development. |
| **Home Assistant** | Home Automation | 3 sources | 3000+ integrations, local control. Often run in its own VM. |
| **Vaultwarden** | Password Manager | 3 sources | Lightweight Bitwarden-compatible server. Critical to back up. |
| **Portainer** | Docker Management | 3 sources | First install for beginners. Web UI for all Docker operations. |
| **Uptime Kuma** | Monitoring | 3 sources | Simple, beautiful uptime monitoring dashboard. |
| **Paperless-NGX** | Document Mgmt | 2 sources | OCR-powered document scanner and organizer. |
| **Pi-hole/AdGuard** | DNS Ad Blocking | 2 sources | Network-wide ad/tracker blocking at DNS level. |
| **Grafana + Prometheus** | Metrics | 2 sources | Infrastructure monitoring and visualization. |

### Additional Notable Apps

- **Navidrome**: Self-hosted Spotify alternative for music libraries
- **Homepage**: Customizable dashboard for all your services (React/Next.js, 40+ integrations)
- **Mealie**: Recipe management and meal planning
- **Bookstack**: Wiki/documentation platform
- **Gitea**: Lightweight self-hosted Git with CI/CD

### Beginner Strategy

Multiple sources converge on this advice:
1. **Start with one problem** — don't try to replace everything at once
2. **Learn Docker Compose first** — it's the lingua franca of self-hosting
3. **Install Portainer early** — visual feedback helps learning
4. **Use Tailscale for remote access** — simplest secure networking, no port forwarding needed
5. **Add a reverse proxy when ready** — Caddy is the easiest starting point
6. **Back up religiously** — especially Vaultwarden and any data you care about

### Key Resources

- [awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted) — Comprehensive catalog of FOSS self-hosted software
- [selfh.st](https://selfh.st/apps/) — Curated self-hosted app directory with reviews
- [DoTheEvo/selfhosted-apps-docker](https://github.com/DoTheEvo/selfhosted-apps-docker) — Guide-by-example with 40+ Docker Compose configs
- [mikeroyal/Self-Hosting-Guide](https://github.com/mikeroyal/Self-Hosting-Guide) — Comprehensive guide covering cloud, LLMs, networking, and automation
- [Perfect Media Server](https://perfectmediaserver.com/04-day-two/top10apps/) — Focused guide for media-centric setups

## Execution Log

| # | Action | Target | Result | Reasoning |
|---|--------|--------|--------|-----------|
| 1 | WebSearch | "best self-hosted apps 2025 2026 beginner guide" | 10 results including Perfect Media Server, Pinggy, awesome-selfhosted, selfh.st, LowEndBox, Android Authority | Broad search to find top recommendation lists |
| 2 | WebSearch | "self-hosting beginner guide docker compose starter stack" | 10 results including SSD Nodes tutorial, DoTheEvo GitHub, mikeroyal guide | Focused on Docker Compose infrastructure |
| 3 | WebSearch | "Proxmox Docker Tailscale self-hosting setup guide 2025" | 10 results including official Tailscale guide, Proxmox forum, Headscale guides | Targeted hypervisor + networking layer |
| 4 | WebFetch | perfectmediaserver.com/04-day-two/top10apps/ | Extracted top 10 apps list (Jellyfin, HA, Immich, Nextcloud, Traefik, Gitea, etc.) | High-authority curated list |
| 5 | WebFetch | squaredtech.co/7-best-self-hosted-apps | Failed (JS-rendered page, no content extracted) | Attempted but page not scrapable |
| 6 | WebFetch | tailscale.com/blog/guide-self-hosting-proxmox | Full Proxmox setup guide with hardware recs, step-by-step install | Official guide from Tailscale |
| 7 | WebFetch | ssdnodes.com/blog/self-hosting-docker-compose/ | Docker Compose tutorial with nginx-proxy, Let's Encrypt, Portainer | Infrastructure setup reference |
| 8 | WebFetch | pinggy.io/blog/best_self_hosted_apps/ | 15 apps listed for 2026 including Hoarder, Homepage, Postiz, Beszel | Broad app catalog with descriptions |
| 9 | WebFetch | lowendbox.com/blog/what-apps-should-you-be-self-hosting-is-2026/ | 7 apps including Monica, Uptime Kuma, Change Detection, Serpbear | Niche/personal picks, less mainstream |
| 10 | WebFetch | github.com/DoTheEvo/selfhosted-apps-docker | 40+ apps with Caddy as reverse proxy, Arch Linux as docker host | Excellent reference for Docker configs |
| 11 | WebSearch | "self-hosting networking Cloudflare Tunnel vs Tailscale reverse proxy beginners 2025" | 10 results comparing tunneling solutions | Networking layer research |
| 12 | Bash/curl | Reddit /r/selfhosted thread | 404 — thread URL invalid | Attempted Reddit community data |
| 13 | WebFetch | dev.to Cloudflare vs Tailscale vs ngrok comparison | Clear comparison table with pros/cons | Networking decision framework |
| 14 | WebSearch | "reddit selfhosted must have apps beginner starter 2025" | 10 results including Android Authority, DB Tech, selfh.st | Additional beginner-focused sources |
| 15 | WebFetch | androidauthority.com 7 open-source apps | Portainer, Nextcloud, HA, Jellyfin, Navidrome, Paperless-NGX, Dockpeek | High-quality beginner recommendations |
| 16 | WebFetch | selfh.st/post/2025-favorite-new-apps/ | 24 new apps from 2025, trends (Pangolin, Nextcloud alternatives, *arr fatigue) | Trend analysis |
| 17 | WebFetch | xda-developers.com Cloudflare vs Tailscale | Author preferred CF Tunnels for public access behind CGNAT | Key networking insight |
| 18 | WebFetch | dbtechreviews.com 5 daily homelab apps | VaultWarden, AdGuard Home, Postiz, DumbPad, Maretta | Daily-use perspective |

## Budget Used

| Resource | Soft Limit | Actual | Notes |
|----------|-----------|--------|-------|
| Searches | ~7 | **5** | Under budget |
| Fetches | ~17 | **14** (13 successful, 1 failed) | Under budget |
| Reddit attempts | — | 1 (failed, 404) | Thread URL was invalid |
