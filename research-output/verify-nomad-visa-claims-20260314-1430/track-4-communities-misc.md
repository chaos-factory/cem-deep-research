## Summary

- r/digitalnomad currently has ~2.37M subscribers per [Reddit API data](https://www.reddit.com/r/digitalnomad/), close to the paper's claim of 2.4M — PARTIALLY CONFIRMED (actual count is ~2.37M, not 2.4M)
- r/ExpatFIRE currently has ~127.6K subscribers per [Reddit API data](https://www.reddit.com/r/ExpatFIRE/), higher than the paper's claim of 112K — PARTIALLY CONFIRMED (actual count exceeds the stated figure, likely grew since the paper was written)
- South Dakota's Department of Labor began enforcing rules against PMB addresses for payroll/unemployment tax purposes starting November 2022, continuing through 2023, per [Dakota Free Press](https://dakotafreepress.com/2023/06/14/rvers-lose-tax-haven-in-south-dakota-mail-forwarding-addresses-invalid-for-sd-unemployment-tax-purposes/) and [SavvyNomad](https://blog.savvynomad.io/domicile-in-south-dakota-for-digital-nomads/) — CONFIRMED
- The SD PMB enforcement was based on existing unemployment insurance statutes (SDCL 61-1-3, 61-1-26, 61-1-27), not new legislation, though SB 139 (March 2023) tightened voting residency definitions separately
- The paper cited slev.life as the source for the SD PMB claim, but slev.life is a personal blog about cult history, Serbian language learning, and travel — it does not appear to contain content about SD payroll policy
- subredditstats.com (cited as source for r/digitalnomad) has degraded data since Reddit's 2023 API pricing changes and no longer reliably shows current subscriber counts
- gummysearch.com (cited as source for r/ExpatFIRE) returned a 404 page for the r/ExpatFIRE URL

## Full Findings

**Claim 1: r/digitalnomad has 2.4M members**
- Paper says: r/digitalnomad has 2.4M members (source: subredditstats.com)
- Found: Reddit's JSON API reports 2,365,597 subscribers as of March 2026. The cited source subredditstats.com has degraded data quality since Reddit's API pricing changes in 2023 and includes a disclaimer warning against relying on its accuracy.
- Verdict: PARTIALLY CONFIRMED
- Source: https://www.reddit.com/r/digitalnomad/about.json

**Claim 2: r/ExpatFIRE has 112K members**
- Paper says: r/ExpatFIRE has 112K members (source: gummysearch.com)
- Found: Reddit's JSON API reports 127,623 subscribers as of March 2026. The cited source gummysearch.com returns a 404 for the r/ExpatFIRE page. The discrepancy likely reflects community growth since the paper's data was collected — 112K was plausibly accurate at an earlier date.
- Verdict: PARTIALLY CONFIRMED
- Source: https://www.reddit.com/r/ExpatFIRE/about.json

**Claim 3: SD disallowed PMB addresses for payroll purposes in 2023**
- Paper says: South Dakota disallowed PMB addresses for payroll purposes in 2023 (source: slev.life)
- Found: The SD Department of Labor began enforcing existing unemployment insurance law against PMB/mail-forwarding address users in November 2022, notifying over 600 entities. This continued through 2023. Employers could no longer claim workers using PMB addresses as SD employees for unemployment tax purposes. The SavvyNomad blog corroborates this, stating: "according to a recent policy change in 2023, you cannot use a personal mailbox address for payroll purposes." However, the cited source slev.life does not appear to contain any content related to SD payroll policy — it is a personal blog covering unrelated topics.
- Verdict: CONFIRMED (substance is correct, but the cited source appears wrong)
- Sources: https://dakotafreepress.com/2023/06/14/rvers-lose-tax-haven-in-south-dakota-mail-forwarding-addresses-invalid-for-sd-unemployment-tax-purposes/ and https://blog.savvynomad.io/domicile-in-south-dakota-for-digital-nomads/

## Budget Used

- Searches: 3 of 3 (firecrawl search for SD PMB on slev.life, firecrawl search for r/digitalnomad members, firecrawl search for SD PMB payroll)
- Fetches: 6 of 6 (subredditstats.com scrape, gummysearch.com scrape, savvynomad scrape, slev.life scrape, Dakota Free Press WebFetch, Reddit JSON API x2 via curl)
