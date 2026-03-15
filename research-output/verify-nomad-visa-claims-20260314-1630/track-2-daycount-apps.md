## Summary

- TaxDay pricing is $9.99/mo as claimed, but the free trial is **45 days** (not 30 days as the paper states). GPS tracking and all 50 states confirmed. ([App Store](https://apps.apple.com/us/app/taxday/id1045026503), [taxday.com](https://www.taxday.com/))
- TaxBird pricing of $4.99/mo or $39.99/yr with a 30-day free trial is **fully confirmed**. Tracks US states, Canadian provinces, and countries worldwide. ([App Store](https://apps.apple.com/us/app/taxbird-residency-tracker/id1238166926))
- Domicile365 offers a **60-day free trial** as claimed, but paid pricing **is disclosed**: $19.99/mo for individual subscriptions -- contradicting the paper's claim that pricing is "not disclosed." 15-minute GPS intervals confirmed. ([domicile365.com FAQ](https://www.domicile365.com/FrequentlyAskedQuestions.html))
- Flamingo Compliance has **multiple subscription tiers** (Settler ~$22.99/yr, Resident ~$49.90/yr, Globetrotter ~$99/yr based on App Store data). The "~$30/yr basic" claim is roughly in the right range but imprecise. The correct domain is **flamingo.tax**, not flamingotracker.com. Auto movement recording confirmed. ([flamingo.tax](https://flamingo.tax/), [App Store](https://apps.apple.com/us/app/flamingo-compliance/id1631680437))

## Full Findings

**Claim 1: TaxDay pricing -- $9.99/mo (30-day free trial), GPS tracking, all 50 state tax rules**
- Paper says: $9.99/mo with a 30-day free trial. GPS tracking, all 50 state tax rules.
- Found: The Apple App Store listing states: "All new TaxDay members enjoy a risk-free **45-day trial** to start. After your trial, you can decide if you'd like to subscribe to TaxDay for **$9.99 per month**." The homepage at taxday.com says "Enjoy your first 30 days for free" -- so there is a discrepancy between the website (30 days) and the App Store (45 days). GPS tracking and coverage of all 50 US states plus Puerto Rico, USVI, and 250+ countries are confirmed on the product page.
- Verdict: PARTIALLY CONFIRMED -- the $9.99/mo price is correct, and the website does say 30 days, but the App Store listing says 45-day trial. GPS and state tax features confirmed.
- Source: https://apps.apple.com/us/app/taxday/id1045026503, https://www.taxday.com/

**Claim 2: TaxBird pricing -- $4.99/mo or $39.99/yr (30-day free trial), US state + country tracking**
- Paper says: $4.99/mo or $39.99/yr with a 30-day free trial. US state + country tracking.
- Found: The Apple App Store listing confirms: "In-app subscription options are: Annual @ $39.99, Monthly @ $4.99" and "Take advantage of our free 30-day trial." The app supports country-level tracking worldwide, US state-level tracking, and Canadian province-level tracking.
- Verdict: CONFIRMED
- Source: https://apps.apple.com/us/app/taxbird-residency-tracker/id1238166926

**Claim 3: Domicile365 -- Free (60-day trial); paid pricing not disclosed; 15-min GPS intervals**
- Paper says: Free with 60-day trial. Paid pricing not disclosed. 15-minute GPS intervals.
- Found: The FAQ page explicitly states: "We offer a free 60 day trial period for both individual and enterprise accounts. No credit card is needed." However, pricing **is** disclosed: "Individual subscriptions are presently U.S. **$19.99 per month**." The homepage confirms "Location generally recorded in **15 minute increments**" using GPS, Bluetooth, Wi-Fi hotspots, and cell tower locations.
- Verdict: PARTIALLY CONFIRMED -- the 60-day trial and 15-min GPS intervals are correct, but the claim that paid pricing is "not disclosed" is wrong; it is $19.99/mo.
- Source: https://www.domicile365.com/FrequentlyAskedQuestions.html, https://www.domicile365.com/

**Claim 4: Flamingo Compliance -- ~$30/yr (basic), auto movement recording; source: flamingotracker.com**
- Paper says: ~$30/yr for basic plan. Auto movement recording. Source: flamingotracker.com.
- Found: The actual domain is **flamingo.tax** (not flamingotracker.com). The App Store listing (Georgia locale) shows multiple tiers: Settler ($1.99/mo or $22.99/yr), Resident ($4.99/mo or $49.90/yr), Globetrotter ($9.99/mo or $99/yr). A user review mentions paying "$30" for what they expected was a basic plan. The pricing page on flamingo.tax exists but actual prices are loaded dynamically and did not scrape. The "~$30/yr" claim roughly aligns with the Settler tier ($22.99/yr) or could reflect a previous price or regional variation. Auto trip recording via geolocation is confirmed on both the App Store listing and flamingo.tax. The app offers a 30-day free "Discovery mode."
- Verdict: PARTIALLY CONFIRMED -- auto movement recording is correct. The ~$30/yr basic price is in the general range of the cheapest tier ($22.99/yr Settler) but not exact. The source URL flamingotracker.com is incorrect; the actual domain is flamingo.tax.
- Source: https://flamingo.tax/pricing, https://apps.apple.com/ge/app/flamingo-compliance/id1631680437

## Budget Used

- Searches: 5 (TaxDay, TaxBird, Domicile365, Flamingo x2)
- Scrapes: 8 (taxday.com home, TaxDay App Store, TaxBird App Store, Domicile365 FAQ, Domicile365 home, Flamingo App Store, flamingo.tax home, flamingo.tax pricing, Flamingo reviews)
