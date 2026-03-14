# Track 2: Day-Count / Residency Tracking Apps — Pricing Verification

## Summary

- TaxDay pricing of $9.99/mo is **confirmed** per the Apple App Store listing, but the free trial is 45 days (not 30 as the paper claimed); a Fortune article from March 2026 states "90-day trial" ([App Store](https://apps.apple.com/us/app/taxday/id1045026503))
- TaxDay GPS tracking across all 50 US states is **confirmed** via [taxday.com/product](https://www.taxday.com/product/), which also mentions 250+ countries
- TaxBird pricing of $4.99/mo or $39.99/yr is **confirmed** per both the [Apple App Store](https://apps.apple.com/us/app/taxbird-residency-tracker/id1238166926) and [Google Play](https://play.google.com/store/apps/details?id=com.ware2now.taxbird) listings
- TaxBird 30-day free trial is **confirmed** per the App Store description
- TaxBird tracks US states, Canadian provinces, and countries worldwide — **confirmed** per App Store description
- Domicile365 60-day free trial (no credit card) is **confirmed** per [domicile365.com](https://www.domicile365.com/)
- Domicile365 15-minute GPS interval recording is **confirmed** per [domicile365.com](https://www.domicile365.com/)
- Domicile365 individual paid pricing is not disclosed on the website, consistent with the paper's claim — **confirmed**
- Flamingo Compliance ~$30/yr (basic) claim is **unconfirmed**; the homepage at [flamingo.tax](https://flamingo.tax/) does not list prices, and the "flamingotracker.com" URL from the paper redirects to flamingo.tax; an unrelated "Flamingo" Slack app at flamingoapp.com charges $30/month (not per year), suggesting possible confusion
- Note: a third-party source (daysofstay.com, Feb 2026) lists TaxBird at $6.99/mo or $59.99/yr, which differs from the current App Store pricing of $4.99/mo or $39.99/yr — prices may have changed or the third-party data may be outdated

## Full Findings

**Claim 1: TaxDay pricing — $9.99/mo (30-day free trial), GPS tracking, all 50 state tax rules**
- Paper says: $9.99/mo with a 30-day free trial. GPS tracking. All 50 state tax rules.
- Found: The Apple App Store listing confirms $9.99/mo. However, the free trial is described as **45 days** ("All new TaxDay members enjoy a risk-free 45-day trial to start"), not 30 days. A Fortune article (March 11, 2026) states "$9.99 for TaxDay after a 90-day trial." GPS tracking is confirmed. The product page states tracking in "all 50 US States, including Puerto Rico and the US Virgin Islands" plus "over 250 countries." The App Store description confirms "a comprehensive database of state-by-state residency tax rules."
- Verdict: PARTIALLY CONFIRMED — price is correct, GPS and 50-state coverage confirmed, but the trial period is 45 days per the App Store (or 90 days per Fortune), not 30 days as claimed.
- Source: https://apps.apple.com/us/app/taxday/id1045026503, https://www.taxday.com/product/, https://fortune.com/2026/03/11/how-ultrawealthy-use-smartphone-apps-to-avoid-millions-in-taxes/

**Claim 2: TaxBird pricing — $4.99/mo or $39.99/yr (30-day free trial), US state + country tracking**
- Paper says: $4.99/mo or $39.99/yr with a 30-day free trial. US state + country tracking.
- Found: The Apple App Store listing confirms: "Annual @ $39.99, Monthly @ $4.99" and "Take advantage of our free 30-day trial, prior to subscribing." The description confirms tracking at country level worldwide, state level in the US, and province level in Canada.
- Verdict: CONFIRMED
- Source: https://apps.apple.com/us/app/taxbird-residency-tracker/id1238166926, https://play.google.com/store/apps/details?id=com.ware2now.taxbird

**Claim 3: Domicile365 — Free (60-day trial); paid pricing not disclosed; 15-min GPS intervals**
- Paper says: Free with a 60-day trial. Paid pricing not disclosed. 15-minute GPS intervals.
- Found: The domicile365.com homepage states: "Sixty (60) day free trial -- no credit card required." It also states: "Location generally recorded in 15 minute increments using the highest level of accuracy supported by your phone." Individual paid pricing is not listed on the main site (an enterprise pricing page exists at enterprise.domicile365.com but does not disclose individual rates). The app is listed as free with in-app purchases on the App Store.
- Verdict: CONFIRMED
- Source: https://www.domicile365.com/, https://enterprise.domicile365.com/EnterprisePricing.php

**Claim 4: Flamingo Compliance — ~$30/yr (basic), auto movement recording**
- Paper says: ~$30/yr for a basic plan. Auto movement recording. Source: flamingotracker.com.
- Found: The actual product is at flamingo.tax (flamingotracker.com redirects there per the Fortune article link). The homepage confirms "Auto Trip Recording" — "Flamingo Compliance automatically determines when you cross the border and accurately records your trip details." However, pricing is not displayed on the homepage. The site mentions subscription tiers (Settler, Resident, Globetrotter) but does not list prices publicly. A search result for "flamingoapp.com/pricing" shows a completely different product (a Slack leave-management tool called "Flamingo" at $30/month, not $30/year). No web source was found confirming the ~$30/yr price point for Flamingo Compliance. Auto movement recording is confirmed.
- Verdict: PARTIALLY CONFIRMED — auto movement recording is confirmed, but the ~$30/yr pricing claim could not be verified from any web source. The paper's cited URL (flamingotracker.com) does resolve to the correct product (flamingo.tax), but pricing is not publicly listed.
- Source: https://flamingo.tax/, https://fortune.com/2026/03/11/how-ultrawealthy-use-smartphone-apps-to-avoid-millions-in-taxes/

## Budget Used

- Searches: 3/3 (TaxDay, TaxBird, Domicile365+Flamingo)
- Fetches: 8/8 (taxday.com/product, TaxDay App Store, taxbird.com, TaxBird App Store, domicile365.com, flamingo.tax, Fortune article, daysmonitor.com comparison)
