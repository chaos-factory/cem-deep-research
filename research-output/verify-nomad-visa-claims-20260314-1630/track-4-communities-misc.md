## Summary

- r/digitalnomad has ~2.37M subscribers per Reddit's live API, not 2.4M as claimed — close but slightly overstated ([reddit.com/r/digitalnomad](https://www.reddit.com/r/digitalnomad/))
- r/ExpatFIRE has ~128K subscribers per Reddit's live API, not 112K as claimed — the paper understates the actual count ([reddit.com/r/ExpatFIRE](https://www.reddit.com/r/ExpatFIRE/))
- South Dakota did crack down on PMB addresses for payroll/unemployment purposes in 2023, though the mechanism is more nuanced than "disallowed PMB addresses for payroll" ([dakotafreepress.com](https://dakotafreepress.com/2023/06/14/rvers-lose-tax-haven-in-south-dakota-mail-forwarding-addresses-invalid-for-sd-unemployment-tax-purposes/))
- The SD payroll change was driven by enforcement of existing statutes (Title 61) after the Department of Labor found 600+ entities using mail-forwarding addresses for unemployment tax purposes ([dakotafreepress.com](https://dakotafreepress.com/2023/06/14/rvers-lose-tax-haven-in-south-dakota-mail-forwarding-addresses-invalid-for-sd-unemployment-tax-purposes/))
- 2023 House Bill 139 (actually Senate Bill 139) redefined residency for voting purposes; the payroll impact was a separate enforcement action ([worldpost.io](https://www.worldpost.io/blog/blog-post-title-four-8wzzd))
- The slev.life page covers SD residency for nomads generally but does not discuss the 2023 PMB payroll change ([slev.life](https://slev.life/south-dakota-residency-for-nomads))

## Full Findings

**Claim 1: r/digitalnomad has 2.4M members**
- Paper says: r/digitalnomad has 2.4M members (source: subredditstats.com)
- Found: Reddit's live API (`/r/digitalnomad/about.json`) returns 2,365,609 subscribers as of 2026-03-14. This is approximately 2.37M, which rounds to 2.4M but is technically below that threshold.
- Verdict: PARTIALLY CONFIRMED
- Source: https://www.reddit.com/r/digitalnomad/about.json

**Claim 2: r/ExpatFIRE has 112K members**
- Paper says: r/ExpatFIRE has 112K members (source: gummysearch.com)
- Found: Reddit's live API (`/r/ExpatFIRE/about.json`) returns 127,626 subscribers as of 2026-03-14. This is ~128K, significantly higher than the claimed 112K. The paper likely used an outdated figure; the subreddit has grown ~14% since the data was captured.
- Verdict: PARTIALLY CONFIRMED
- Source: https://www.reddit.com/r/ExpatFIRE/about.json

**Claim 3: SD disallowed PMB addresses for payroll purposes in 2023**
- Paper says: South Dakota disallowed PMB addresses for payroll purposes in 2023 (source: slev.life)
- Found: This claim is substantively correct but the details are more nuanced. In 2023, South Dakota's Department of Labor began enforcing existing statutes (SDCL 61-1-3, 61-1-26, 61-1-27) that define whether work is "within" South Dakota, refusing to recognize remote workers using mail-forwarding/PMB addresses as SD workers for unemployment tax purposes. Separately, 2023 Senate Bill 139 (signed by Gov. Noem in March 2023) tightened residency definitions for voting, requiring 30 days of physical presence and disallowing PMB addresses. The WorldPost blog confirms that the 2023 changes made it "more difficult to use a PMB for W2 employment" and that employers now need a residential address to claim SD as the tax state. However, the cited source (slev.life) does not actually discuss this payroll change — the slev.life page is a general guide to SD residency for nomads. The payroll claim itself is well-documented by other sources.
- Verdict: PARTIALLY CONFIRMED
- Source: https://dakotafreepress.com/2023/06/14/rvers-lose-tax-haven-in-south-dakota-mail-forwarding-addresses-invalid-for-sd-unemployment-tax-purposes/, https://www.worldpost.io/blog/blog-post-title-four-8wzzd

## Budget Used

- Searches: 2 (firecrawl search)
- Fetches/scrapes: 3 (slev.life, dakotafreepress.com, worldpost.io) + 2 Reddit API calls = 5
- Total: 2 searches, 5 fetches
