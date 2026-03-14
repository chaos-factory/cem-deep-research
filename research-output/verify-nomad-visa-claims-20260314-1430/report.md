# Verification Report: Phase 2 Cluster #2 — State Tax Exit & Domicile Setup

**Date:** 2026-03-14
**Paper verified:** `chaos-factory/ideator-docs` — `phase-2-cluster-2.md`
**Method:** Multi-agent verification using firecrawl CLI (primary), firecrawl MCP, WebSearch/WebFetch (fallback)

---

## Verification Summary

| # | Claim | Verdict | Key Finding |
|---|-------|---------|-------------|
| 1 | SavvyNomad $55/$85/$245/mo, 42 reviews, 5 stars | PARTIALLY CONFIRMED | Prices increased to $60/$90/$265. Trustpilot is 4.8 stars, not 5.0. Review count (42) correct. |
| 2 | Americas Mailbox $170–$249/yr + $25 setup | CONFIRMED | Actual $169.99–$249.99/yr with $25 setup. |
| 3 | Escapees $110–$150/yr + $50 enrollment + $50 deposit | CONFIRMED | All figures match exactly. |
| 4 | DakotaPost $155/mo, $210/mo | CONTRADICTED | Current pricing $199/mo and $259/mo. Third-party source corroborates old $155/$210 — likely a price increase. |
| 5 | Nomad Tax $450 + $200 FEIE, merging into Basta+Croop | UNCONFIRMED | Basta+Croop now uses monthly retainer model ($500–$6,500/mo). No evidence of per-return pricing. |
| 6 | TaxDay $9.99/mo, 30-day trial | PARTIALLY CONFIRMED | Price correct. Trial is 45 days per App Store (or 90 days per [Fortune](https://fortune.com/2026/03/11/how-ultrawealthy-use-smartphone-apps-to-avoid-millions-in-taxes/)), not 30. |
| 7 | TaxBird $4.99/mo or $39.99/yr, 30-day trial | CONFIRMED | All details match per [App Store](https://apps.apple.com/us/app/taxbird-residency-tracker/id1238166926). |
| 8 | Domicile365 free trial, pricing "not disclosed" | CONFIRMED | 60-day trial confirmed. Individual pricing not publicly listed on main site. |
| 9 | Flamingo ~$30/yr | PARTIALLY CONFIRMED | Auto movement recording confirmed. Pricing not publicly listed on [flamingo.tax](https://flamingo.tax/); ~$30/yr unverifiable. |
| 10 | 18.1M digital nomads, up 147% from 2019 | PARTIALLY CONFIRMED | 18.1M/147% is 2024 data. MBO Partners 2025 report shows [18.5M](https://www.facebook.com/mbopartners/photos/1451615482994137/). |
| 11 | 102.4% expatriation jump Q1 2025 | CONFIRMED | [CS Global Partners](https://csglobalpartners.com/news/us-expat-numbers-double-in-2025-as-americans-seek-new-lives-abroad/) confirms all figures exactly. |
| 12 | CA FTB 520 audits, 32% penalty surge | PARTIALLY CONFIRMED | 520/230 audit numbers unverifiable from any web source. 32% penalty surge confirmed via [ietaxattorney.com](https://ietaxattorney.com/california-ftb-audit-defense-how-state-tax-audits-differ-from-irs-audits/), but not from the paper's cited sources. |
| 13 | FEIE $130K (2025), $132.9K (2026) | CONFIRMED | Confirmed via [Greenback Tax](https://www.greenbacktaxservices.com/blog/irs-tax-inflation-adjustments-2026/) and [TaxesForExpats](https://www.taxesforexpats.com/articles/tax-saving-strategies/foreign-earned-income-exclusion.html). |
| 14 | r/digitalnomad 2.4M members | PARTIALLY CONFIRMED | Reddit API shows [~2.37M](https://www.reddit.com/r/digitalnomad/about.json). Close but ~1.4% overstated. |
| 15 | r/ExpatFIRE 112K members | PARTIALLY CONFIRMED | Reddit API shows [~127.6K](https://www.reddit.com/r/ExpatFIRE/about.json). Paper understated — community has grown. Cited source (gummysearch.com) returns 404. |
| 16 | SD PMB policy change in 2023 | CONFIRMED | Enforcement began Nov 2022, continued through 2023. Cited source (slev.life) is wrong — it's an unrelated personal blog. Correct sources: [Dakota Free Press](https://dakotafreepress.com/2023/06/14/rvers-lose-tax-haven-in-south-dakota-mail-forwarding-addresses-invalid-for-sd-unemployment-tax-purposes/), [SavvyNomad blog](https://blog.savvynomad.io/domicile-in-south-dakota-for-digital-nomads/). |

---

## Scorecard

- **CONFIRMED:** 6 of 16 (37.5%)
- **PARTIALLY CONFIRMED:** 8 of 16 (50%)
- **CONTRADICTED:** 1 of 16 (6.25%)
- **UNCONFIRMED:** 1 of 16 (6.25%)

---

## High-Priority Issues

### Contradicted Claims

1. **DakotaPost pricing (Claim 4):** Paper says $155/mo and $210/mo. Current site shows $199/mo and $259/mo. A third-party blog ([roadbits.net](https://roadbits.net/mail-forwarding/)) corroborates the old $155/$210 pricing, suggesting a recent price increase rather than a research error. The paper's billing frequency (monthly) appears correct — v1 run incorrectly reported annual billing.

### Unconfirmed Claims

2. **Nomad Tax pricing (Claim 5):** The per-return pricing ($450 + $200 FEIE) cannot be verified. Basta+Croop now operates on a monthly retainer model ($500–$6,500/mo). The Nomad Tax brand and its original pricing structure appear to have been fully absorbed.

### Wrong Source Citations

3. **FTB audit numbers (Claim 12):** The specific numbers (520 audits in 2023, 230 in 2019) could not be found on the cited source yourtaxbase.com or any other web source. The 32% penalty surge is real but sourced from ietaxattorney.com, not corporatedirect.com.

4. **SD PMB policy (Claim 16):** The cited source slev.life is a personal blog about cult history and Serbian language — it has no content about SD payroll policy. The correct sources are Dakota Free Press and SavvyNomad's blog.

5. **r/ExpatFIRE (Claim 15):** The cited source gummysearch.com returns a 404.

---

## Changes from v1 Run

This v2 run used firecrawl CLI as primary tool (v1 used WebSearch/WebFetch only). Key differences:

| Claim | v1 Verdict | v2 Verdict | What changed |
|-------|-----------|-----------|--------------|
| DakotaPost | CONTRADICTED (annual pricing) | CONTRADICTED (monthly pricing) | Firecrawl extracted $199/$259 per month (not per year). Third-party source confirmed old $155/$210 was monthly. |
| Nomad Tax | CONFIRMED | UNCONFIRMED | Firecrawl scraped Basta+Croop's actual packages page — monthly retainer model, no per-return pricing. v1 relied on cached/search-result snippets. |
| r/ExpatFIRE | CONTRADICTED (51.8K) | PARTIALLY CONFIRMED (127.6K) | v2 used Reddit's JSON API directly vs subredditstats.com. Reddit API is authoritative. |
| Domicile365 pricing | PARTIALLY CONFIRMED (pricing is $19.99/mo) | CONFIRMED (pricing not disclosed on main site) | v2 found enterprise.domicile365.com doesn't show individual pricing; main site has no prices listed. The v1 finding of $19.99/mo may have been from a different page or cached data. |
| FTB 520 audits | PARTIALLY CONFIRMED | PARTIALLY CONFIRMED | v2 could not find the 520/230 numbers anywhere; v1 claimed yourtaxbase.com confirmed them. |
| Flamingo pricing | CONFIRMED ($29.99/yr) | PARTIALLY CONFIRMED | v2 could not find pricing on flamingo.tax; v1 found $29.99/yr on App Store. Pricing may have been removed from public listing. |

---

## Impact on Paper's Conclusions

The findings do **not materially affect** the paper's NO BUILD verdict. The core analytical framework holds:

- The gap remains mostly closed by existing services
- SavvyNomad's price increases ($55→$60, $85→$90, $245→$265) slightly strengthen the "too expensive" dissatisfaction pattern noted in the paper
- DakotaPost's price increases ($155→$199, $210→$259) also support this
- The community size corrections don't change the channel assessment
- Nomad Tax's absorption into Basta+Croop's retainer model is a consolidation signal consistent with the paper's analysis

---

## Sources Consulted

- [savvynomad.io/pricing](https://savvynomad.io/pricing)
- [Trustpilot — SavvyNomad](https://www.trustpilot.com/review/savvynomad.io)
- [americasmailbox.com/rates-and-plans](https://americasmailbox.com/rates-and-plans/)
- [escapeesmailservice.com](https://escapeesmailservice.com/escapees-mail-service-rates-and-categories/)
- [escapees.com/benefits](https://www.escapees.com/benefits)
- [dakotapost.net](https://www.dakotapost.net/services/mail-forwarding)
- [roadbits.net/mail-forwarding](https://roadbits.net/mail-forwarding/)
- [bastacroop.com/packages](https://bastacroop.com/packages/)
- [TaxDay App Store](https://apps.apple.com/us/app/taxday/id1045026503)
- [taxday.com/product](https://www.taxday.com/product/)
- [TaxBird App Store](https://apps.apple.com/us/app/taxbird-residency-tracker/id1238166926)
- [domicile365.com](https://www.domicile365.com/)
- [flamingo.tax](https://flamingo.tax/)
- [Fortune — smartphone tax apps](https://fortune.com/2026/03/11/how-ultrawealthy-use-smartphone-apps-to-avoid-millions-in-taxes/)
- [MBO Partners via SIA](https://www.staffingindustry.com/news/global-daily-news/digital-nomads-move-from-niche-to-normal-with-181m-workers)
- [MBO Partners via Facebook](https://www.facebook.com/mbopartners/photos/1451615482994137/)
- [CS Global Partners](https://csglobalpartners.com/news/us-expat-numbers-double-in-2025-as-americans-seek-new-lives-abroad/)
- [ietaxattorney.com — FTB audits](https://ietaxattorney.com/california-ftb-audit-defense-how-state-tax-audits-differ-from-irs-audits/)
- [Greenback Tax — FEIE 2026](https://www.greenbacktaxservices.com/blog/irs-tax-inflation-adjustments-2026/)
- [TaxesForExpats — FEIE](https://www.taxesforexpats.com/articles/tax-saving-strategies/foreign-earned-income-exclusion.html)
- [Reddit API — r/digitalnomad](https://www.reddit.com/r/digitalnomad/about.json)
- [Reddit API — r/ExpatFIRE](https://www.reddit.com/r/ExpatFIRE/about.json)
- [Dakota Free Press — SD PMB](https://dakotafreepress.com/2023/06/14/rvers-lose-tax-haven-in-south-dakota-mail-forwarding-addresses-invalid-for-sd-unemployment-tax-purposes/)
- [SavvyNomad blog — SD domicile](https://blog.savvynomad.io/domicile-in-south-dakota-for-digital-nomads/)
