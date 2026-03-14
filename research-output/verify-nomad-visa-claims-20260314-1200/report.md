# Verification Report: Phase 2 Cluster #2 — State Tax Exit & Domicile Setup

**Date:** 2026-03-14
**Paper verified:** `chaos-factory/ideator-docs` — `phase-2-cluster-2.md`

---

## Verification Summary

| # | Claim | Verdict | Key Discrepancy |
|---|-------|---------|----------------|
| 1 | SavvyNomad $55/$85/$245/mo, 42 reviews, 5 stars | PARTIALLY CONFIRMED | Trustpilot rating is 4.8 stars, not 5.0. Upper-tier prices unverifiable (JS-rendered page). |
| 2 | Americas Mailbox $170–$249/yr + $25 setup | PARTIALLY CONFIRMED | Actual range $169.99–$249.99/yr. Close enough. Google review count unverified. |
| 3 | Escapees $110–$150/yr + $50 enrollment + $50 deposit | CONFIRMED | All figures match exactly. |
| 4 | DakotaPost $155/mo, $210/mo | CONTRADICTED | Current pricing is $199/yr and $259/yr (annual plans), not monthly. |
| 5 | Nomad Tax $450 + $200 FEIE, merging into Basta+Croop | CONFIRMED | nomadtax.io 301-redirects to bastacroop.com. |
| 6 | TaxDay $9.99/mo, 30-day trial | PARTIALLY CONFIRMED | App Store shows 45-day trial, website says 30 days. |
| 7 | TaxBird $4.99/mo or $39.99/yr, 30-day trial | CONFIRMED | All details match. |
| 8 | Domicile365 free trial, pricing "not disclosed" | PARTIALLY CONFIRMED | 60-day trial correct, but pricing IS disclosed ($19.99/mo). |
| 9 | Flamingo ~$30/yr | CONFIRMED | Settler tier $29.99/yr. Site now flamingo.tax. |
| 10 | 18.1M digital nomads, up 147% from 2019 | PARTIALLY CONFIRMED | That's the 2024 data; MBO Partners 2025 report says 18.5M / 153%. |
| 11 | 102.4% expatriation jump Q1 2025 | CONFIRMED | CS Global Partners data matches. |
| 12 | CA FTB 520 audits, 32% penalty surge | PARTIALLY CONFIRMED | 520 audits confirmed. "32% penalty surge in 2025" could not be verified anywhere. |
| 13 | FEIE $130K (2025), $132.9K (2026) | CONFIRMED | Confirmed across multiple IRS-citing sources. |
| 14 | r/digitalnomad 2.4M members | PARTIALLY CONFIRMED | Actual: ~2.18M (10% lower than claimed). |
| 15 | r/ExpatFIRE 112K members | CONTRADICTED | Actual: ~51.8K (less than half claimed). Cited source (gummysearch.com) returns 403. |
| 16 | SD PMB policy change in 2023 | PARTIALLY CONFIRMED | Enforcement began Nov 2022, continued through 2023. Cited source (slev.life) doesn't discuss this. |

---

## Scorecard

- **CONFIRMED:** 6 of 16 (37.5%)
- **PARTIALLY CONFIRMED:** 8 of 16 (50%)
- **CONTRADICTED:** 2 of 16 (12.5%)
- **UNCONFIRMED:** 0 of 16

---

## High-Priority Issues

### Contradicted Claims

1. **DakotaPost pricing (Claim 4):** The paper states $155/mo and $210/mo for monthly/weekly forwarding. Current pricing is $199/yr and $259/yr — annual plans, not monthly. Either the pricing changed or was incorrectly recorded.

2. **r/ExpatFIRE size (Claim 15):** The paper claims 112K members; actual count is ~51.8K. The cited source (gummysearch.com) is inaccessible (403). This is a >2x overstatement that inflates the perceived channel size.

### Notable Partial Confirmations

- **SavvyNomad Trustpilot (Claim 1):** 4.8 stars, not 5.0 — minor but worth correcting.
- **Digital nomad count (Claim 10):** Paper uses 2024 data (18.1M) while attributing it to the "2025 Trends Report." The actual 2025 figure is 18.5M.
- **FTB penalty surge (Claim 12):** The "32% penalty notice surge in 2025" has no verifiable source. The audit count (520) is confirmed.

---

## Impact on Paper's Conclusions

The contradictions and inaccuracies do **not materially affect** the paper's NO BUILD verdict:

- DakotaPost pricing error is cosmetic — it's a minor competitor, and the annual pricing actually strengthens the point about low-cost alternatives.
- r/ExpatFIRE overstatement makes channels appear larger than they are, but the verdict already notes channels are "general nomad/expat channels, not specific to state tax exit."
- The digital nomad count being 18.5M (vs 18.1M) actually slightly strengthens the market size argument, but the paper already scores Gate 1 at 2 (pass).

The core analytical conclusions — gap is mostly closed, SavvyNomad dominates, software-only components are low-value — are unaffected by these factual discrepancies.

---

## Sources Consulted

- [savvynomad.io/pricing](https://savvynomad.io/pricing)
- [Trustpilot — SavvyNomad](https://www.trustpilot.com/review/savvynomad.io)
- [americasmailbox.com/rates-and-plans](https://americasmailbox.com/rates-and-plans)
- [escapeesmailservice.com](https://escapeesmailservice.com)
- [dakotapost.net](https://dakotapost.net/rates-services/mail-forwarding/get-started)
- [nomadtax.io → bastacroop.com](https://bastacroop.com/digital-nomads/)
- [taxday.com](https://www.taxday.com/)
- [taxbird.com](https://www.taxbird.com/)
- [domicile365.com/pricing](https://www.domicile365.com/pricing.html)
- [flamingo.tax](https://flamingo.tax/)
- [MBO Partners Digital Nomads](https://www.mbopartners.com/state-of-independence/digital-nomads/)
- [CS Global Partners](https://csglobalpartners.com/news/us-expat-numbers-double-in-2025-as-americans-seek-new-lives-abroad/)
- [yourtaxbase.com](https://yourtaxbase.com/blog/terminate-california-residency-avoid-ftb-audit)
- [IRS — FEIE](https://www.irs.gov/individuals/international-taxpayers/foreign-earned-income-exclusion)
- [subredditstats.com — r/digitalnomad](https://subredditstats.com/r/digitalnomad)
- [subredditstats.com — r/ExpatFIRE](https://subredditstats.com/r/expatfire)
- [Dakota Free Press — SD PMB](https://dakotafreepress.com/2023/06/14/rvers-lose-tax-haven-in-south-dakota-mail-forwarding-addresses-invalid-for-sd-unemployment-tax-purposes/)
