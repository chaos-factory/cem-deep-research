# Research Plan: Nomad Visa US — Pain Points Rankable by Micro-SaaS Revenue Potential

## Tier: Deep
- **Strategy**: Depth — quantify pain points and size the addressable market for each
- **Total budget (soft)**: ~40 searches, ~120 fetches, 6 subagents

## Research Tracks

### Track 1: Reddit pain point mining (r/digitalnomad, r/USExpatTaxes, r/expats, r/tax, r/personalfinance)
- **Objective**: Mine top threads for the most emotionally intense pain points — what makes people angry, confused, or scared. Quantify by upvotes/engagement.
- **Primary source**: Reddit JSON API (curl) + firecrawl search for discovery
- **Budget**: ~8 searches, ~25 fetches
- **Output**: `track-1-reddit-pain.md`

### Track 2: Tax compliance pain points — depth
- **Objective**: Deep dive on FBAR, FEIE, state tax severance, SE tax, Form 5471. Quantify penalty amounts, filing costs, error rates. Find what CPAs charge for nomad-specific filings.
- **Primary source**: Firecrawl (IRS, tax advisory sites, CPA directories)
- **Budget**: ~7 searches, ~20 fetches
- **Output**: `track-2-tax-depth.md`

### Track 3: Existing tools & their gaps
- **Objective**: Map every existing tool (TaxBird, TaxDay, Flamingo, SavvyNomad, Nomad Tax, Bright!Tax, etc), their pricing, ratings, and specific user complaints. Find the gaps no tool covers.
- **Primary source**: Firecrawl (app stores, review sites, product pages) + Reddit for complaints
- **Budget**: ~7 searches, ~20 fetches
- **Output**: `track-3-tool-gaps.md`

### Track 4: Market sizing — TAM for each pain point
- **Objective**: Find number of US digital nomads, expats filing FBAR/FEIE, people using state domicile services. Estimate willingness to pay and price sensitivity.
- **Primary source**: Firecrawl (MBO Partners reports, State Dept data, IRS statistics)
- **Budget**: ~6 searches, ~18 fetches
- **Output**: `track-4-market-size.md`

### Track 5: Domicile, mail, banking, insurance logistics
- **Objective**: Deep dive on the non-tax pain points: establishing domicile (SD/FL/TX), virtual mailbox limitations, banking Patriot Act issues, health insurance gaps.
- **Primary source**: Firecrawl + Reddit
- **Budget**: ~6 searches, ~18 fetches
- **Output**: `track-5-logistics.md`

### Track 6: Competitor revenue & business model analysis
- **Objective**: Find revenue/user estimates for existing players (SavvyNomad, Nomad Tax, TaxBird, Escapees, America's Mailbox). Understand pricing models and what customers pay annually.
- **Primary source**: Firecrawl (Crunchbase, LinkedIn, press, pricing pages)
- **Budget**: ~6 searches, ~19 fetches
- **Output**: `track-6-competitor-revenue.md`

## Subagent Boundaries
- Track 1: raw community sentiment and pain intensity
- Track 2: tax-specific technical details and costs
- Track 3: existing product landscape and gaps
- Track 4: market size numbers
- Track 5: non-tax logistics pain points
- Track 6: competitor business models and revenue benchmarks
