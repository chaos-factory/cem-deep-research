# Research Plan: Best Budget Self-Hosting Setup for Beginners

## Tier: Medium
- **Strategy**: Breadth — cover hardware, software, and community recommendations
- **Total budget (soft)**: ~20 searches, ~50 fetches, 3 subagents

## Research Tracks

### Track 1: Reddit community recommendations (r/selfhosted, r/homelab, r/homeserver)
- **Objective**: Mine top posts and comments for hardware recommendations, common beginner setups, and recurring advice
- **Primary source**: Reddit JSON API (curl)
- **Budget**: ~5 searches, ~15 fetches
- **Output**: `track-1-reddit.md`

### Track 2: Hardware options and pricing
- **Objective**: Find current pricing and specs for commonly recommended hardware (mini PCs, used enterprise gear, Raspberry Pi, NAS devices)
- **Primary source**: Firecrawl (product pages, review sites)
- **Budget**: ~8 searches, ~18 fetches
- **Output**: `track-2-hardware.md`

### Track 3: Software stack and guides
- **Objective**: Research most recommended self-hosting software (Proxmox, Docker, Tailscale, specific apps) and beginner guides
- **Primary source**: Firecrawl (docs, blogs, guides)
- **Budget**: ~7 searches, ~17 fetches
- **Output**: `track-3-software.md`

## Subagent Boundaries
- Track 1 focuses on **community sentiment** — what real people recommend and warn about
- Track 2 focuses on **current hardware facts** — pricing, specs, availability
- Track 3 focuses on **software ecosystem** — what to run and how to get started
