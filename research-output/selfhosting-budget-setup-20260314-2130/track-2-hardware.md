# Track 2: Budget Self-Hosting Hardware — Pricing, Specs, and Best Value Options

## Summary

- **Raspberry Pi 5** remains the cheapest entry point: 2GB/$50, 4GB/$60, 8GB/$80, 16GB/$205 from [raspberrypi.com](https://www.raspberrypi.com/products/raspberry-pi-5/). Idle power ~3-5W, load ~8.5W. ARM Cortex-A76 quad-core @ 2.4GHz. Needs case, PSU, storage — total usable kit ~$100-120 for 8GB model.
- **Used Dell OptiPlex Micro** (7060/7070/7080, i5 8th-9th gen) sell for **$65-150 on eBay** with 8-16GB RAM and 256GB SSD included. Best bang-for-buck at the $100 price point per [Reddit r/homelab](https://www.reddit.com/r/homelab/comments/1l0zrdj/for_a_cheapreliable_micromini_computer_is_a_used/). Idle ~10-15W.
- **Lenovo ThinkCentre M720q/M920q Tiny** refurbished units run **$80-150 on eBay** (i5-8400T/8500T, 16GB, 256GB SSD). Similar performance to OptiPlex Micro, slightly better build quality per community consensus. Listed at [Best Buy refurb](https://www.bestbuy.com/product/lenovo-refurbished-thinkcentre-m720q-desktop-intel-core-i5-16gb-memory-256gb-ssd-black/J3P8K578HR) around $170.
- **HP EliteDesk 800 G5 Mini** refurbished: **$130-180** with i5-9500T, 8-16GB RAM, 256GB SSD from [Newegg](https://www.newegg.com/p/N82E16883451961) and Amazon. 6-core processor makes it slightly more capable than older OptiPlex units. Idle ~10W.
- **Intel N100-based mini PCs** (Beelink S12 Pro, GMKtec NucBox) are available **new for $120-180** with 8-16GB RAM and 256-512GB SSD. Idle as low as 6W, peak ~15-20W. Excellent for lightweight services per [PC Build Advisor](https://www.pcbuildadvisor.com/how-much-electricity-does-a-mini-pc-use-do-mini-pcs-use-a-lot-of-electricity-a-2025-cost-efficiency-guide/).
- **Budget NAS devices under $250**: Beelink ME Mini NAS ($209, 6x M.2 NVMe, Intel N150, 12GB LPDDR5), GMKTec G9 NAS, Synology BeeStation 4TB (~$200 all-in-one), UGREEN DXP2800, ZimaBoard 2 per [NASCompares](https://nascompares.com/guide/best-nas-for-under-249-2025-2026/).
- **NAS devices under $500**: Synology DS224+ (~$240-300), DS423+ ($499), UGREEN DXP4800 ($499, Intel N100, 4x SATA + 2x M.2), UniFi UNAS Pro ($499, 7-bay with 10GbE) per [NASCompares](https://nascompares.com/guide/best-nas-for-under-499-2025-2026/).
- **Power consumption hierarchy**: RPi5 (3-8W) < N100 mini PCs (6-20W) < Used enterprise micro PCs (10-25W) < Full NAS devices (15-40W). At $0.17/kWh, a 15W-average mini PC costs ~$22/year to run 24/7.
- **Best value at $50**: Raspberry Pi 5 2GB board only, or a very old used OptiPlex 3020 Micro on eBay.
- **Best value at $100**: Used Dell OptiPlex 7060 Micro or Lenovo M720q with i5, 8-16GB RAM, 256GB SSD from eBay.
- **Best value at $200**: New Intel N100 mini PC (Beelink S12 Pro/EQ12) with 16GB/500GB — or RPi5 8GB full kit + external SSD.
- **Best value at $500**: UGREEN DXP4800 NAS (Intel N100, 4-bay + 2x M.2, excludes drives) or Synology DS423+ for mature software ecosystem, or Minisforum MS-R1 barebones (~$504) for raw compute with dual 10GbE.
- Community consensus per Reddit: used enterprise micro PCs (OptiPlex/ThinkCentre/EliteDesk) offer the best performance-per-dollar; N100 boxes win on power efficiency; RPi5 suits lightweight/learning setups; dedicated NAS only if you need multiple drive bays.

## Full Findings

### Raspberry Pi 5

**Source**: [Official Raspberry Pi product page](https://www.raspberrypi.com/products/raspberry-pi-5/)

| Variant | Price | RAM | CPU | Power (idle/load) |
|---------|-------|-----|-----|-------------------|
| RPi5 2GB | $50 | 2GB LPDDR4X | BCM2712 4x A76 @ 2.4GHz | ~3W / ~7W |
| RPi5 4GB | $60 | 4GB LPDDR4X | Same | ~3W / ~7.5W |
| RPi5 8GB | $80 | 8GB LPDDR4X | Same | ~3W / ~8.5W |
| RPi5 16GB | $205 | 16GB LPDDR4X | Same | ~3.5W / ~9W |

**Accessories needed**: Official 27W USB-C PSU (~$12), case (~$10-15), microSD or M.2 HAT + NVMe SSD ($20-50). Total usable 8GB kit: ~$120-140.

**Strengths**: Lowest power draw, huge community, GPIO for IoT, PCIe for M.2 SSD via HAT.
**Weaknesses**: ARM architecture limits some x86 Docker images, max 16GB RAM, no SATA ports, USB 3.0 bottleneck for external storage.

**Power consumption data**: Per [PCMag review](https://www.pcmag.com/reviews/raspberry-pi-5), idle ~2.7W without fan, up to 8.5W under load with fan installed.

### Used Enterprise Micro PCs

**Dell OptiPlex Micro (7060/7070/7080)**

Pricing from eBay, refurb dealers, and [Discount Computer Depot](https://discountcomputerdepot.com/categories/refurbished-computers/desktop-computers/computer-brands/dell-desktops/dell-optiplex-desktops.html):

| Model | Gen | Typical eBay Price | CPU | RAM (typical) | Storage |
|-------|-----|-------------------|-----|---------------|---------|
| OptiPlex 3060 Micro | 8th | $60-90 | i5-8500T (6C) | 8GB DDR4 | 256GB SSD |
| OptiPlex 7060 Micro | 8th | $80-120 | i5-8500T (6C) | 16GB DDR4 | 256GB NVMe |
| OptiPlex 7070 Micro | 9th | $110-160 | i5-9500T (6C) | 16GB DDR4 | 256-512GB NVMe |
| OptiPlex 7080 Micro | 10th | $150-220 | i5-10500T (6C) | 16GB DDR4 | 512GB NVMe |
| OptiPlex 7010 Mini (13th) | 13th | $425 (new refurb) | i5-13500T | 16GB DDR5 | 256GB NVMe |

TDP: 35W (8th gen) down to 15W (12th gen+). Idle power: ~8-15W depending on generation. Community reports from [Reddit](https://www.reddit.com/r/homelab/comments/1l0zrdj/for_a_cheapreliable_micromini_computer_is_a_used/): "It's hard to beat a $65 grab for a reliable mini pc like an old dell micro."

**Lenovo ThinkCentre M720q/M920q Tiny**

| Model | Typical Price | CPU | RAM | Storage |
|-------|--------------|-----|-----|---------|
| M720q | $80-130 (eBay) | i5-8400T (6C @ 1.7GHz) | 8-16GB DDR4 | 256GB NVMe |
| M920q | $120-180 (eBay) | i5-8500T/9500T (6C) | 16GB DDR4 | 256-512GB NVMe |
| M720q (Best Buy refurb) | ~$170 | i5-8400T | 16GB | 256GB SSD |

Power: Similar to OptiPlex, ~10-15W idle. Supports up to 64GB DDR4 (2 DIMM slots). VESA mountable.

**HP EliteDesk 800 G5 Mini**

| Source | Price | CPU | RAM | Storage |
|--------|-------|-----|-----|---------|
| [Newegg (refurb)](https://www.newegg.com/p/N82E16883451961) | ~$130 | i5-8500T (6C @ 2.1GHz) | 8GB DDR4 | 256GB NVMe |
| Newegg (refurb, upgraded) | ~$160 | i5-9500T (6C @ 2.2GHz) | 8GB DDR4 | 1TB NVMe |
| Amazon (refurb) | ~$150-200 | i5-9500T | 16GB DDR4 | 256-512GB NVMe |

Supports up to 64GB DDR4. Dual M.2 slots in some configurations. WiFi included in some models.

### New Budget Mini PCs (Intel N100/N150 Class)

**Source**: [PC Build Advisor power guide](https://www.pcbuildadvisor.com/how-much-electricity-does-a-mini-pc-use-do-mini-pcs-use-a-lot-of-electricity-a-2025-cost-efficiency-guide/), Amazon listings, [PCMag picks](https://www.pcmag.com/picks/the-best-windows-mini-pcs)

| Model | Price | CPU | RAM | Storage | Power (idle/load) |
|-------|-------|-----|-----|---------|-------------------|
| Beelink S12 Pro | ~$130 | Intel N100 (4C @ 3.4GHz) | 16GB DDR4 | 500GB SSD | 6W / 15-20W |
| Beelink EQ12 | ~$150 | Intel N100 | 16GB DDR5 | 500GB NVMe | 6W / 18W |
| GMKtec NucBox G5 | ~$120 | Intel N97 | 12GB DDR5 | 256GB | 6W / 15W |
| GEEKOM IT13 | ~$350 | i5-13600H (12C) | 16GB DDR4 | 1TB NVMe | 15W / 45W |

N100 advantages: 6W TDP, passively cooled (silent), AES-NI for encryption, enough for 5-10 Docker containers.
N100 disadvantages: Only 16GB max RAM (soldered in many models), single NVMe slot typically, limited expansion.

Per Reddit: "99% of the time you would be better off with an N100 based system. The N100 uses significantly less power and benchmarks higher than a 10 year old i5."

### NAS Devices

**Under $250** — Source: [NASCompares guide](https://nascompares.com/guide/best-nas-for-under-249-2025-2026/)

| Device | Price | CPU | RAM | Bays | Network | Notes |
|--------|-------|-----|-----|------|---------|-------|
| Beelink ME Mini NAS | $209 | Intel N150 (4C) | 12GB LPDDR5 | 6x M.2 NVMe | 2x 2.5GbE + WiFi 6 | No OS, no drives, passive cooling |
| Synology BeeStation 4TB | ~$200 | ARM (unknown) | ~1GB | 1x 3.5" (included) | 1x 1GbE | All-in-one, simplest setup |
| UGREEN DXP2800 | ~$200 | Intel N100 | 8GB | 2x 3.5" SATA | 1x 2.5GbE | UGOS software |
| ZimaBoard 2 (832) | ~$200 | Intel N100 | 8GB | PCIe expansion | 2x 2.5GbE | DIY-friendly, runs anything |
| TerrraMaster F2-425 | ~$230 | Intel N95 | 8GB DDR5 | 2x 3.5" SATA | 2x 2.5GbE | TOS system |

Note: All NAS prices exclude drives. A 4TB NAS HDD (WD Red, Seagate IronWolf) costs ~$90-110 additional.

**Under $500** — Source: [NASCompares guide](https://nascompares.com/guide/best-nas-for-under-499-2025-2026/)

| Device | Price | CPU | RAM | Bays | Network |
|--------|-------|-----|-----|------|---------|
| Synology DS224+ | ~$240-300 | Intel Celeron J4125 | 2GB DDR4 | 2x 3.5" SATA | 2x 1GbE |
| Synology DS423+ | $499 | Intel Celeron J4125 | 2GB DDR4 | 4x 3.5" SATA + 2x M.2 | 2x 1GbE |
| UGREEN DXP4800 | $499 | Intel N100 | 8GB DDR5 | 4x 3.5" SATA + 2x M.2 | 2x 2.5GbE |
| UniFi UNAS Pro | $499 | ARM Cortex-A57 | 8GB DDR4 | 7x 3.5" SATA | 1x 10GbE + 1x 1GbE |
| UniFi UNAS 2 | $199 | ARM | 4GB | 2x 3.5" SATA | 1x 2.5GbE |
| UniFi UNAS 4 | $379 | ARM | 8GB | 4x 3.5" + 2x M.2 | 2x 2.5GbE |

### Power Consumption Comparison

Source: [PC Build Advisor](https://www.pcbuildadvisor.com/how-much-electricity-does-a-mini-pc-use-do-mini-pcs-use-a-lot-of-electricity-a-2025-cost-efficiency-guide/), [Reddit r/homelab](https://www.reddit.com/r/homelab/comments/1o0ig45/whats_the_current_generation_of_low_power_mini_pc/)

| Device Class | Idle Power | Load Power | Annual Cost (24/7 @ $0.17/kWh) |
|-------------|-----------|-----------|-------------------------------|
| Raspberry Pi 5 | 3W | 8W | $4-8 |
| Intel N100 mini PC | 6W | 15-20W | $9-15 |
| Used OptiPlex/ThinkCentre (8th gen) | 10-15W | 35-50W | $15-25 |
| Used OptiPlex/ThinkCentre (12th gen+) | 6-10W | 25-35W | $9-18 |
| Synology 2-bay NAS | 12-18W | 25-30W | $18-25 |
| Synology 4-bay NAS (loaded) | 25-35W | 40-55W | $37-50 |
| Full tower/old server | 60-150W | 200-400W | $89-200+ |

Reddit user note: "6th gen processor has a TDP of 35 watts. 8th gen till 11th can clock down to 25 watts. 12th gen+ are 15 watts for mobile. N100 is 6 watts."

### Best Value at Each Price Point

**~$50**: Raspberry Pi 5 2GB (board only). Very limited — needs accessories. Alternatively, hunt for a free/surplus PC from work.

**~$100**: Used Dell OptiPlex 7060 Micro or Lenovo M720q from eBay. Expect i5-8500T, 8-16GB RAM, 256GB SSD. Immediately usable with Proxmox or Ubuntu Server. Best overall value point.

**~$200**: Two strong options:
1. New Intel N100 mini PC (Beelink S12 Pro / EQ12) — 16GB RAM, 500GB SSD, ultra-low power, silent
2. RPi5 8GB complete kit with NVMe HAT and 256GB SSD — lower power but ARM limitations

**~$500**: Depends on use case:
- **Storage-focused**: UGREEN DXP4800 ($499) or Synology DS423+ ($499) — 4-bay NAS with M.2 cache, excludes drives
- **Compute-focused**: Minisforum MS-R1 ($504 with 32GB RAM, no storage) — 12-core ARM, dual 10GbE, PCIe x16 slot
- **Balanced**: Minisforum MS-01 barebones ($640, slightly over budget) — Intel i5-12600H, dual 10GbE SFP+, 2x 2.5GbE

### High-Performance Mini PCs for Homelabs (>$500)

Source: [VirtualizationHowto](https://www.virtualizationhowto.com/2025/11/the-best-mini-pcs-for-home-labs-in-2025-ranked-by-real-performance/)

For reference, the serious homelab mini PC tier:
- Minisforum MS-01: $640 barebones (i5-12600H, dual 10GbE SFP+)
- Beelink SER9 Max: $669 with 32GB/1TB (Ryzen 7 H 255, 10GbE)
- Minisforum MS-A2: $872 barebones (Ryzen 9 9955HX, dual 2.5GbE)
- Minisforum MS-02: $1199 barebones (Core Ultra 9 285HX, dual 25GbE, full GPU slot)

## Execution Log

1. **Search**: firecrawl search "budget self-hosting hardware 2025 2026 mini PC NUC ThinkCentre price" — Found PCMag, TechRadar, ZDNET, YouTube, Amazon results for mini PCs. Identified key models and price ranges.

2. **Search**: firecrawl search "Raspberry Pi 5 price buy 2026 NAS Synology budget" — Found RPi5 official page, NASCompares guides for under-$249 and under-$499 NAS, Reddit comparison threads.

3. **Search**: firecrawl search "Dell OptiPlex used server homelab 2025 price specs" — Found Reddit r/homelab thread on used OptiPlex pricing, Discount Computer Depot listings, Best Buy and eBay results.

4. **Scrape**: NASCompares under-$249 NAS guide — Got detailed specs for Beelink ME Mini NAS ($209), TerraMaster F2-425, GMKTec G9, Synology BeeStation, UGREEN DXP2800, ZimaBoard 2.

5. **Scrape**: NASCompares under-$499 NAS guide — Got UniFi UNAS Pro ($499), UGREEN DXP4800 ($499), Synology DS425+ pricing and full specs.

6. **Scrape**: Discount Computer Depot OptiPlex page — Got refurbished Dell OptiPlex pricing (7010 Mini at $425 for 13th gen).

7. **Search**: firecrawl search "Raspberry Pi 5 price buy 2026 8GB 4GB specs power consumption" — Confirmed official pricing tiers ($50/$60/$80/$205), power data from PCMag.

8. **Search**: firecrawl search "Lenovo ThinkCentre M720q M920q tiny used refurbished price homelab 2025" — Found eBay listings ($80-150), Best Buy refurb ($170), Facebook marketplace posts, community feedback.

9. **Scrape**: Official Raspberry Pi 5 product page — Confirmed 16GB variant at $205, BCM2712 specs, PCIe support.

10. **Search**: firecrawl search "HP EliteDesk 800 G5 mini refurbished price homelab" — Found Newegg ($130), Best Buy, Amazon pricing for refurb units. Confirmed i5-9500T 6-core specs.

11. **Search**: firecrawl search "best mini PC homelab power consumption watt idle 2025 comparison" — Found PC Build Advisor guide (6-45W range for mini PCs), Reddit thread on power optimization, blog post on N100 server choice.

12. **Scrape**: PC Build Advisor power consumption guide — Got detailed power draw data: N100 class 6-15W, mainstream 15-45W, high-performance 45-120W. Annual cost calculations at $0.17/kWh.

13. **Scrape**: Best Buy HP EliteDesk listing — Failed (HTTP/2 protocol error). Used search snippet data instead.

14. **Scrape**: VirtualizationHowto best mini PCs for homelabs — Got full specs and pricing for Minisforum MS-02 ($1199), MS-A2 ($872), MS-01 ($640), MS-S1 Max ($2560), Beelink SER9 Max ($669), MINIX 715 AI ($940), MS-R1 ($504).

15. **Fetch**: Reddit r/homelab thread on used Dell OptiPlex (JSON API) — Got community pricing consensus: $65 for old Dell micro, N100 vs used i5 debate, power consumption tiers by CPU generation.

16. **Search**: firecrawl search "Synology DS224+ DS423+ price buy 2026" — Confirmed DS224+ at $240-300, DS423+ at $499, price history data.

## Budget Used

| Resource | Soft Limit | Actual Used |
|----------|-----------|-------------|
| Searches | ~8 | 8 |
| Fetches/Scrapes | ~18 | 9 (7 scrapes + 1 Reddit JSON + 1 failed) |
| **Total** | **~26** | **17** |
