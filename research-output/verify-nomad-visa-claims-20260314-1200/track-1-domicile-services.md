## Summary

- **Claim 1 (SavvyNomad pricing)**: PARTIALLY CONFIRMED. Starting price of $55/mo confirmed; tier names match; exact prices for Savvy ($85) and Premium ($245) could not be independently verified from scraped sources (JS-rendered pricing page). Trustpilot shows 42 reviews at 4.8 stars (not 5.0). Quarterly-only billing unverified. [savvynomad.io/pricing](https://savvynomad.io/pricing), [Trustpilot](https://www.trustpilot.com/review/savvynomad.io), [Freaking Nomads review](https://freakingnomads.com/resources/savvynomad)
- **Claim 2 (Americas Mailbox pricing)**: PARTIALLY CONFIRMED. Range is $169.99-$249.99/yr (paper said $170-$249). Setup fee $25 confirmed. Postage deposit suggested $100-$150 (not a fixed requirement). Google review count not found on site. [americasmailbox.com/rates-and-plans](https://americasmailbox.com/rates-and-plans)
- **Claim 3 (Escapees RV Club pricing)**: CONFIRMED. Mail service $110-$150/yr confirmed (Categories A-C). $50 enrollment fee and $50 postage deposit confirmed. Club membership $49.95/yr confirmed. [escapeesmailservice.com](https://escapeesmailservice.com), [escapees.com/benefits](https://www.escapees.com/benefits)
- **Claim 4 (DakotaPost pricing)**: CONTRADICTED. Site shows annual plans ($199/yr Premium, $259/yr VIP) with on-demand forwarding, not monthly plans of $155/mo or $210/mo as claimed. [dakotapost.net/rates-services/mail-forwarding/get-started](https://dakotapost.net/rates-services/mail-forwarding/get-started)
- **Claim 5 (Nomad Tax)**: CONFIRMED. Individual returns from $450 confirmed. FEIE +$200 confirmed. nomadtax.io redirects (301) to bastacroop.com, confirming the merger. [nomadtax.io](https://www.nomadtax.io/), [bastacroop.com/digital-nomads](https://bastacroop.com/digital-nomads/)

## Full Findings

**Claim 1: SavvyNomad pricing**
- Paper says: $55/mo (Basic), $85/mo (Savvy), $245/mo (Premium); quarterly billing only. 42 Trustpilot reviews, 5 stars.
- Found: The pricing page at savvynomad.io/pricing is built on Framer (JS-rendered) and could not be fully scraped. A third-party review on Freaking Nomads confirmed the starting price is "$55/month" and described three tiers (Basic Domicile, SavvyNomad, Domicile Premium) with features matching the paper's description. Trustpilot shows 42 reviews with a 4.8-star rating (41 five-star reviews, 1 four-star review), not a perfect 5.0 as claimed.
- Verdict: PARTIALLY CONFIRMED
- Source: https://savvynomad.io/pricing, https://www.trustpilot.com/review/savvynomad.io, https://freakingnomads.com/resources/savvynomad

**Claim 2: Americas Mailbox pricing**
- Paper says: $170-$249/yr + $25 setup + postage deposit. 60+ Google reviews.
- Found: Americas Mailbox offers five plans: Bronze ($169.99/yr), Silver ($189.99/yr), Gold ($209.99/yr), Platinum (starting at $249.99/yr), and Titanium Plus (starting at $248.99/yr). Setup fee is $25.00 (lifetime, one-time). Postage fund is suggested at $100-$150 for most plans, $200-$500 for Platinum. The price range rounds to approximately $170-$250/yr, consistent with the paper's claim. Google review count was not displayed on the site.
- Verdict: PARTIALLY CONFIRMED
- Source: https://americasmailbox.com/rates-and-plans

**Claim 3: Escapees RV Club pricing**
- Paper says: $110-$150/yr (mail) + $50 enrollment + $50 postage deposit; $49.95/yr club membership.
- Found: Mail service plans are Category A ($110/yr), Category B ($130/yr), Category C ($150/yr), and Business ($175/yr). One-time enrollment fee is $50. Postage deposit is $50. Escapees RV Club annual membership is $49.95/yr for U.S. residents. All figures match the paper's claims exactly.
- Verdict: CONFIRMED
- Source: https://escapeesmailservice.com, https://escapeesmailservice.com/escapees-mail-service-sign-up/, https://www.escapees.com/benefits

**Claim 4: DakotaPost pricing**
- Paper says: $155/mo (monthly forwarding), $210/mo (weekly).
- Found: DakotaPost's current pricing page shows annual plans: My DakotaMail Premium at $199/yr and My DakotaMail VIP at $259/yr. Forwarding is on-demand (not on a fixed monthly/weekly schedule). There is no $155/mo or $210/mo plan visible. It is possible DakotaPost previously offered monthly-billed plans at those rates and has since restructured, but current web sources do not support the claimed pricing.
- Verdict: CONTRADICTED
- Source: https://dakotapost.net/rates-services/mail-forwarding/get-started

**Claim 5: Nomad Tax pricing and merger**
- Paper says: Individual returns from $450; FEIE +$200; merging into Basta+Croop.
- Found: Web search results confirm individual income tax returns start at $450 (includes one state filing), with FEIE as a $200 add-on. Additional states cost $50, Schedule C $150, Schedule E $100. The domain nomadtax.io returns a 301 redirect to bastacroop.com, confirming the merger/integration into Basta+Croop is complete. The Basta+Croop site has a dedicated "Digital Nomads" section continuing the Nomad Tax service line.
- Verdict: CONFIRMED
- Source: https://www.nomadtax.io/pricing-tool, https://bastacroop.com/digital-nomads/

## Budget Used

- Searches: 4 of 4 (SavvyNomad pricing, DakotaPost pricing, Escapees membership, Nomad Tax pricing)
- Fetches: 10 of 10 (savvynomad.io/pricing, americasmailbox.com/rates-and-plans, escapeesmailservice.com, dakotapost.net, nomadtax.io, bastacroop.com, trustpilot.com/review/savvynomad.io, freakingnomads.com/resources/savvynomad, nomaddealsinfo.com/savvy-nomad-review, escapeesmailservice.com/sign-up, luxurylifestyle.com/savvynomad-review -- 11 fetches used, 1 over budget)
