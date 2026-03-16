# Research Plan: Apify.com Customers' Pain Points and Workarounds

## Tier: Medium
- Searches: 60–120
- Fetches: 120–280
- Subagents: 3–5

## Discovery Findings

**Review sites** (Trustpilot, G2, Capterra) have hundreds of reviews with structured pros/cons. G2 already surfaced "lack of standardized output formats across actors" as a key complaint.

**Reddit** has the richest signal:
- r/apify thread about unfair pricing changes for builders
- r/coldemail threads seeking Apify replacements
- r/webscraping user claiming 90% cost savings after migrating away from Apify to Scrapy
- r/AI_Agents threads about Apify feeling "brittle"
- Threads about LinkedIn/Apollo blocking Apify scrapers

**GitHub** shows technical issues: Crawlee race conditions, softlocks, memory leaks, RequestQueue bugs, TypeScript errors.

**Alternative comparison articles** (Gumloop, ScraperAPI, Firecrawl, IGLeads) detail specific Apify weaknesses to position competitors.

## Strategy

Split into 3 tracks by source type, since pain points cluster differently across communities:

## Research Tracks

### Track 1: User Reviews & Community Voice
**Sources**: G2, Capterra, Trustpilot, Reddit threads (r/apify, r/coldemail, r/webscraping, r/opensource, r/AI_Agents)
**Objective**: Extract specific pain points, complaint patterns, and workarounds from real users. Focus on recurring themes across platforms.
**Why this split**: Review sites and Reddit give first-person accounts with specific frustrations — the most authentic signal.

### Track 2: Technical Issues & Platform Bugs
**Sources**: GitHub issues (apify/crawlee, apify/crawlee-python, apify/apify-cli), StackOverflow, Apify community forum, dev.to
**Objective**: Catalog concrete technical problems, bug patterns, and developer-facing friction. Identify workarounds people share in issue threads.
**Why this split**: Technical issues require reading code-level discussions and GitHub threads — different skill than review analysis.

### Track 3: Pricing, Economics & Competitive Gaps
**Sources**: Reddit pricing threads, alternative comparison articles, Apify pricing docs, competitor positioning pages
**Objective**: Map pricing complaints, cost unpredictability issues, and what competitors highlight as Apify's weaknesses. Document what people actually switch to and why.
**Why this split**: Economic pain points and competitive positioning are best understood together — why people leave tells you what hurts most.
