# Verification Report: Phase 2 Cluster #2 — State Tax Exit & Domicile Setup (v3)

**Date:** 2026-03-14
**Paper verified:** `chaos-factory/ideator-docs` — `phase-2-cluster-2.md`
**Method:** Multi-agent verification using firecrawl CLI (primary), with stale-snippet rule enforced

---

## Verification Summary

| # | Claim | Verdict | Key Finding |
|---|-------|---------|-------------|
| 1 | SavvyNomad $55/$85/$245/mo, 42 reviews, 5 stars | CONTRADICTED | Prices now $60/$90/$265. Both yearly and quarterly billing (not quarterly-only). Trustpilot 4.8 stars, not 5.0. [Source](https://savvynomad.io/pricing) |
| 2 | Americas Mailbox $170–$249/yr + $25 setup | PARTIALLY CONFIRMED | Actual $169.99–$249.99/yr. $25 setup confirmed. [Source](https://americasmailbox.com/rates-and-plans) |
| 3 | Escapees $110–$150/yr + $50 enrollment + $50 deposit | CONFIRMED | All figures match exactly. [Source](https://escapeesmailservice.com) |
| 4 | DakotaPost $155/mo, $210/mo | CONTRADICTED | Current pricing $199/yr and $259/yr — annual, not monthly. [Source](https://www.dakotapost.net/sign-up) |
| 5 | Nomad Tax $450 + $200 FEIE, merging into Basta+Croop | PARTIALLY CONFIRMED | Merger confirmed (full redirect). But returns now start at $565, not $450. [Source](https://bastacroop.com/expat-digital-nomad-tax-returns/) |
| 6 | TaxDay $9.99/mo, 30-day trial | PARTIALLY CONFIRMED | Price correct. Trial is 45 days per [App Store](https://apps.apple.com/us/app/taxday/id1045026503), 30 per website. |
| 7 | TaxBird $4.99/mo or $39.99/yr, 30-day trial | CONFIRMED | All details match. [Source](https://apps.apple.com/us/app/taxbird-residency-tracker/id1238166926) |
| 8 | Domicile365 free trial, pricing "not disclosed" | PARTIALLY CONFIRMED | 60-day trial correct. But pricing IS disclosed: $19.99/mo. [Source](https://www.domicile365.com/FrequentlyAskedQuestions.html) |
| 9 | Flamingo ~$30/yr | PARTIALLY CONFIRMED | Settler tier is $22.99/yr (not ~$30). Auto tracking confirmed. URL should be flamingo.tax. [Source](https://apps.apple.com/ge/app/flamingo-compliance/id1631680437) |
| 10 | 18.1M digital nomads, up 147% from 2019 | PARTIALLY CONFIRMED | That's 2024 data. MBO Partners 2025 report says [18.5M / 153%](https://www.mbopartners.com/state-of-independence/digital-nomads/). |
| 11 | 102.4% expatriation jump Q1 2025 | CONFIRMED | [CS Global Partners](https://csglobalpartners.com/news/us-expat-numbers-double-in-2025-as-americans-seek-new-lives-abroad/) confirms all figures exactly. |
| 12 | CA FTB 520 audits, 32% penalty surge | PARTIALLY CONFIRMED | 520/230 audits confirmed via [SF Chronicle](https://www.sfchronicle.com/california/article/state-tax-people-who-move-19416847.php) and [Corporate Direct](https://www.corporatedirect.com/blog/does-california-have-an-exit-tax). "32% penalty surge" unverified from any source. |
| 13 | FEIE $130K (2025), $132.9K (2026) | CONFIRMED | Confirmed via [IRS Rev. Proc. 2025-32](https://www.irs.gov/pub/irs-drop/rp-25-32.pdf) and [Greenback Tax](https://www.greenbacktaxservices.com/blog/irs-tax-inflation-adjustments-2026/). |
| 14 | r/digitalnomad 2.4M members | PARTIALLY CONFIRMED | Reddit API shows [~2.37M](https://www.reddit.com/r/digitalnomad/about.json). Close but slightly below. |
| 15 | r/ExpatFIRE 112K members | PARTIALLY CONFIRMED | Reddit API shows [~128K](https://www.reddit.com/r/ExpatFIRE/about.json). Paper understated — community has grown. |
| 16 | SD PMB policy change in 2023 | PARTIALLY CONFIRMED | Substance correct. Cited source (slev.life) doesn't discuss this. Correct sources: [Dakota Free Press](https://dakotafreepress.com/2023/06/14/rvers-lose-tax-haven-in-south-dakota-mail-forwarding-addresses-invalid-for-sd-unemployment-tax-purposes/), [WorldPost](https://www.worldpost.io/blog/blog-post-title-four-8wzzd). |

---

## Scorecard

- **CONFIRMED:** 4 of 16 (25%)
- **PARTIALLY CONFIRMED:** 10 of 16 (62.5%)
- **CONTRADICTED:** 2 of 16 (12.5%)
- **UNCONFIRMED:** 0 of 16

---

## High-Priority Issues

### Contradicted Claims

1. **SavvyNomad pricing (Claim 1):** All three prices are wrong ($55→$60, $85→$90, $245→$265). "Quarterly-only billing" is wrong (yearly also available). Trustpilot is 4.8, not 5.0. This is the paper's most-cited competitor — three errors in one entry.

2. **DakotaPost pricing (Claim 4):** Paper says $155/mo and $210/mo (monthly billing). Actual pricing is $199/yr and $259/yr (annual billing). The billing frequency and amounts are both wrong.

### Wrong Source Citations

3. **FTB 32% penalty surge (Claim 12):** This statistic could not be verified from any web source, including the paper's cited sources (yourtaxbase.com, corporatedirect.com).

4. **SD PMB policy (Claim 16):** Cited source slev.life is a general nomad residency guide — it doesn't discuss the 2023 payroll change.

5. **r/ExpatFIRE (Claim 15):** Cited source gummysearch.com returns 404.

---

## Cross-Run Comparison (v1 → v2 → v3)

| Claim | v1 (WebSearch) | v2 (firecrawl CLI) | v3 (firecrawl + stale rule) |
|-------|---------------|--------------------|-----------------------------|
| SavvyNomad | PARTIALLY CONFIRMED | PARTIALLY CONFIRMED | CONTRADICTED |
| DakotaPost billing | Annual (wrong) | Monthly (right) | Annual (right) |
| Nomad Tax price | CONFIRMED ($450) | UNCONFIRMED | PARTIALLY CONFIRMED ($565 now) |
| r/ExpatFIRE | CONTRADICTED (51.8K) | PARTIALLY CONFIRMED (127.6K) | PARTIALLY CONFIRMED (128K) |
| FTB 520 audits | Confirmed via yourtaxbase | Not found on yourtaxbase | Confirmed via SF Chronicle |
| Flamingo price | CONFIRMED ($29.99/yr) | PARTIALLY CONFIRMED (unverifiable) | PARTIALLY CONFIRMED ($22.99/yr) |
| Domicile365 pricing | $19.99/mo (contradicts paper) | Not disclosed (agrees with paper) | $19.99/mo (contradicts paper) |

**Notable v3 improvements:**
- SavvyNomad upgraded to CONTRADICTED — firecrawl scraped the JS-rendered pricing page and found all three prices differ
- FTB 520 audits now sourced to SF Chronicle and Corporate Direct (v1/v2 couldn't find authoritative sources)
- Flamingo pricing found at $22.99/yr via App Store (more precise than v1's $29.99 or v2's "unverifiable")
- Nomad Tax now shows $565 starting price at Basta+Croop (v1 saw $450 from cached snippets)

---

## Impact on Paper's Conclusions

The factual errors do **not materially affect** the paper's NO BUILD verdict:

- SavvyNomad price increases ($55→$60, etc.) slightly strengthen the "too expensive" dissatisfaction pattern
- DakotaPost being annual ($199–$259/yr) rather than monthly makes it a cheaper alternative than the paper portrayed, which actually reinforces the "gap is closed at multiple price points" argument
- The core analysis — that existing services cover the workflow, the software-only gap is narrow, and SavvyNomad dominates — remains sound

---

## Sources Consulted

- [savvynomad.io/pricing](https://savvynomad.io/pricing)
- [Trustpilot — SavvyNomad](https://www.trustpilot.com/review/savvynomad.io)
- [americasmailbox.com/rates-and-plans](https://americasmailbox.com/rates-and-plans)
- [escapeesmailservice.com](https://escapeesmailservice.com)
- [escapees.com/join](https://escapees.com/join/)
- [dakotapost.net/sign-up](https://www.dakotapost.net/sign-up)
- [bastacroop.com/expat-digital-nomad-tax-returns](https://bastacroop.com/expat-digital-nomad-tax-returns/)
- [TaxDay App Store](https://apps.apple.com/us/app/taxday/id1045026503)
- [taxday.com](https://www.taxday.com/)
- [TaxBird App Store](https://apps.apple.com/us/app/taxbird-residency-tracker/id1238166926)
- [domicile365.com FAQ](https://www.domicile365.com/FrequentlyAskedQuestions.html)
- [flamingo.tax](https://flamingo.tax/)
- [Flamingo App Store](https://apps.apple.com/ge/app/flamingo-compliance/id1631680437)
- [MBO Partners — Digital Nomads](https://www.mbopartners.com/state-of-independence/digital-nomads/)
- [US Chamber — Digital Nomads](https://www.uschamber.com/co/grow/thrive/what-is-a-digital-nomad)
- [CS Global Partners](https://csglobalpartners.com/news/us-expat-numbers-double-in-2025-as-americans-seek-new-lives-abroad/)
- [SF Chronicle — FTB Audits](https://www.sfchronicle.com/california/article/state-tax-people-who-move-19416847.php)
- [Corporate Direct — CA Exit Tax](https://www.corporatedirect.com/blog/does-california-have-an-exit-tax)
- [IRS Rev. Proc. 2025-32](https://www.irs.gov/pub/irs-drop/rp-25-32.pdf)
- [Greenback Tax — FEIE 2026](https://www.greenbacktaxservices.com/blog/irs-tax-inflation-adjustments-2026/)
- [Reddit API — r/digitalnomad](https://www.reddit.com/r/digitalnomad/about.json)
- [Reddit API — r/ExpatFIRE](https://www.reddit.com/r/ExpatFIRE/about.json)
- [Dakota Free Press — SD PMB](https://dakotafreepress.com/2023/06/14/rvers-lose-tax-haven-in-south-dakota-mail-forwarding-addresses-invalid-for-sd-unemployment-tax-purposes/)
- [WorldPost — SD Residency](https://www.worldpost.io/blog/blog-post-title-four-8wzzd)
