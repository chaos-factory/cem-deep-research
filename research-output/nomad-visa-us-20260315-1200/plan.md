# Research Plan: Nomad Visa in US — Pain Points Solvable by Micro-SaaS

## Tier: Medium (30–60 searches, 60–140 fetches, 3–10 subagents)

## Discovery Findings

From 5 broad searches (50 results scanned), key themes emerged:

1. **No US digital nomad visa exists** — the US has no dedicated remote work visa. Foreign nomads must use workarounds (B1/B2, ESTA, O-1, H-1B) that don't fit their situation. Massive confusion about what's legal.
2. **Legal gray zone for remote work on tourist visas** — Reddit threads show widespread confusion and contradictory advice. People don't know if working remotely on B1/B2 or ESTA is legal. Risk of denial/deportation.
3. **Tax compliance nightmare** — Multi-country tax obligations, US state tax residency triggers, FEIE eligibility, double taxation. Existing tools (TopTax.ai, MyExpatTaxes, Flamingo) exist but are incomplete or expensive.
4. **Visa tracking & overstay risk** — Nomad app, Notion templates, Flamingo track stays. But nothing integrates visa rules + tax triggers + day counting in one place for US-specific scenarios.
5. **Employer compliance burden** — Companies hiring remote workers who may be in the US face LCA violations (H-1B), permanent establishment risk, payroll tax exposure. Software gap here.
6. **Visa application process is opaque** — No status tracking for most US visa types. Long waits, inconsistent consular decisions. Freelancers/contractors routinely denied because no visa category fits.
7. **Existing SaaS landscape** — NomadApp.io (visa day tracking), Flamingo (compliance), wfa.team (employer-side), CitizenRemote (visa database), Notion templates. Fragmented, nothing US-specific.

## Strategy

Focus exclusively on pain points that a **new micro-SaaS** could solve. Exclude problems requiring government/policy action. Cluster by solvability.

## Research Tracks

### Track 1: Legal Confusion & Visa Eligibility (Subagent A)
**Objective**: Deep-dive into the specific legal confusions nomads face trying to work remotely in/from the US. What questions do they ask? What wrong assumptions do they make? What existing tools/resources try to help and where do they fall short?
**Sources**: Reddit (r/digitalnomad, r/immigration, r/h1b, r/expats), immigration law blogs, Quora, nomad forums.
**Boundary**: Only the "understanding what's legal" problem. Not tax (Track 2) or employer-side (Track 3).

### Track 2: Tax & Financial Compliance (Subagent B)
**Objective**: Map the tax pain points for nomads in/around the US — state tax residency triggers, FEIE, treaty benefits, estimated payments, multi-jurisdiction filing. What tools exist, what gaps remain?
**Sources**: Tax blogs, expat tax services, Reddit tax threads, IRS guidance, existing SaaS tools (TopTax, MyExpatTaxes, Flamingo, NomadCompliance).
**Boundary**: Tax and financial compliance only. Not visa legality (Track 1) or employer compliance (Track 3).

### Track 3: Employer & Contractor Compliance (Subagent C)
**Objective**: What compliance problems do companies face when employees/contractors work remotely from/in the US? Permanent establishment, payroll tax, LCA violations, EOR needs. What tools exist?
**Sources**: HR/mobility blogs, wfa.team, Localyze, TechClass, employer-side forums, LinkedIn discussions.
**Boundary**: Employer/company-side problems only. Not individual nomad tax (Track 2) or visa eligibility (Track 1).

### Track 4: Visa Tracking, Day Counting & Overstay Prevention (Subagent D)
**Objective**: How do nomads currently track visa days, overstay risk, and compliance across multiple countries? What tools exist (NomadApp, Flamingo, spreadsheets)? Where are the gaps, especially for US-specific rules (90/180 ESTA, B1/B2 limits, substantial presence test)?
**Sources**: App stores, Product Hunt, nomad blogs, Reddit threads on tracking tools, Notion template communities.
**Boundary**: Tracking and monitoring tools only. Not the legal questions themselves (Track 1) or tax filing (Track 2).

## Why This Split

These four tracks represent naturally distinct user personas and product surfaces:
- Track 1 = individual nomad pre-decision ("Can I legally do this?")
- Track 2 = individual nomad ongoing compliance ("How do I file/pay?")
- Track 3 = company/employer compliance ("How do we stay legal?")
- Track 4 = individual nomad operational tooling ("Am I about to overstay?")

Each can be researched independently with minimal overlap, and each maps to a potential micro-SaaS product cluster.
