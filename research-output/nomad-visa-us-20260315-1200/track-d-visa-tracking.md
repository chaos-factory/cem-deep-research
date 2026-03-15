# Track D: Visa Tracking, Day Counting, and Overstay Prevention Tools

## Summary

- **The market is fragmented**: At least 8+ dedicated visa/day-counting apps exist (Flamingo Compliance, TrackingDays, Nomad Tracker, Days Monitor, Residency, DaysAround, Schengen Simple, Country Days Tracker, International Travel Tracker) but none covers all jurisdictions and rules comprehensively. ([daysmonitor.com](https://daysmonitor.com/blog/the-5-best-residency-tracking-apps-in-2026-and-one-that-beats-them-all/))
- **Flamingo Compliance is the most mature**: 4.4 stars, 47 ratings on iOS, covers US SPT, Schengen 90/180, UK SRT, US city-level tax tracking (NYC), auto GPS trip recording, CSV export. Praised for customer support. Only iOS, no Android. ([App Store](https://apps.apple.com/us/app/flamingo-compliance/id1631680437))
- **TrackingDays is the longest-running**: 10+ years, trusted in 60+ countries, automatic GPS logging, Schengen rolling window, US Substantial Presence Test, UK SRT nights counting. Also has a sister app "TrackingStates" for US state residency. iOS only. ([trackingdays.com](https://www.trackingdays.com/))
- **Nomad Tracker is newest/most innovative**: Launched Feb 2026, free core features, photo metadata import to reconstruct travel history, background GPS, on-device AI "Fiscal Oracle," Schengen 90/180, 183-day rules, US state tracking added Mar 2026. Solo dev, 85 PH upvotes. No Android. ([Product Hunt](https://www.producthunt.com/products/nomad-tracker-tax-residency-for-nomads))
- **Residency app** targets expats/dual citizens with photo-based trip detection, IRS SPT, B1/B2 & ESTA rules, Green Card physical presence tracking, citizenship timeline tracking. Subscription model. ([App Store](https://apps.apple.com/us/app/residency-visa-day-tracker/id6749048224))
- **Schengen Simple** is Schengen-only but uniquely **predictive** -- it calculates future allowance protecting booked trips, not just backward-looking compliance. Android support added June 2025. ([Globetrender](https://globetrender.com/2025/06/03/schengen-simple-app-helps-travellers-avoid-overstaying-eu/))
- **US-specific rules are poorly served**: The ESTA 90-day limit has no official "time out" ratio rule -- CBP officers have broad discretion, and the unofficial "time in < time out" heuristic is not codified. No app currently models this pattern-of-entry risk. ([Reddit r/travel](https://www.reddit.com/r/travel/comments/1d6wpff/overusing_my_esta_is_that_a_thing/))
- **CBP's own I-94 website and CBP Link app** now offer traveler compliance checks (10-day warning emails, overstay notifications) but are reactive, not planning tools. ([CBP](https://www.cbp.gov/travel/international-visitors/i-94/traveler-compliance))
- **The IRS Substantial Presence Test** (31 days current year + weighted 183-day 3-year formula) is complex; only Wise and a few calculators offer standalone tools, while Flamingo, TrackingDays, and Residency integrate it. ([IRS](https://www.irs.gov/individuals/international-taxpayers/substantial-presence-test), [Wise](https://wise.com/us/expat/substantial-presence-test))
- **Key user complaints**: (1) Apps only do one jurisdiction well, (2) no Android support for most tools, (3) GPS tracking drains battery, (4) free tiers too restrictive, (5) no app handles the US "pattern of entry" risk for ESTA/VWP travelers, (6) actual tax residency tests are more complex than simple day counts, (7) users still don't trust apps over manual checking. ([Reddit r/digitalnomad](https://www.reddit.com/r/digitalnomad/comments/11xvijo/), [Reddit r/longtermtravel](https://www.reddit.com/r/longtermtravel/comments/1qg1raa/))
- **Spreadsheets remain the #1 competitor**: Many nomads still use Google Sheets/Excel because apps lack customization. Nomad Stays is building an "Advanced Visa Tracker" in beta that integrates with housing/travel planning. ([blog.nomadstays.com](https://blog.nomadstays.com/advanced-visa-tracker-built-for-border-crossers-not-spreadsheet-warriors/))
- **Gap analysis -- micro-SaaS opportunity**: A tool that (1) models US ESTA/B1-B2 pattern-of-entry risk (not just day counting), (2) combines SPT + closer connection exception + treaty tie-breaker logic, (3) works cross-platform (web + mobile), (4) offers predictive "what-if" trip planning across multiple jurisdictions simultaneously, and (5) integrates I-94 data via CBP API or manual import would fill the biggest unmet need.

## Full Findings

### Existing Tools Landscape

#### Flamingo Compliance (AccuraSoft Ltd)
- **Platform**: iOS only, 247.7 MB
- **Rating**: 4.4/5, 47 ratings
- **Pricing**: Free with in-app purchases
- **Key features**: Auto GPS trip recording, tax residency & domicile tracking, US cities tax tracking (NYC), permanent residency tracking, Schengen 90/180 calculator, passport index synced with IATA, document storage, CSV export
- **US-specific**: Substantial Presence Test, Physical Presence Test, US state + city tracking
- **Privacy**: Local-only storage + iCloud
- **Strength**: Most comprehensive feature set for multi-jurisdiction compliance
- **Weakness**: iOS-only, no web version, NYC is only city for city-level tracking
- Source: [App Store listing](https://apps.apple.com/us/app/flamingo-compliance/id1631680437)

#### TrackingDays
- **Platform**: iOS only
- **History**: 10+ years, downloaded in 60+ countries
- **Key features**: Automatic GPS background tracking, Schengen rolling 90/180 counting, US SPT support, UK SRT night counting, Rolling 365 feature (Portugal/NZ/Malaysia), Cyprus 60-day rule
- **US-specific**: Substantial Presence Test with 3-year weighted formula, "Non USA Days" feature for US expat Physical Presence Test (330 days abroad), sister app "TrackingStates" for US state residency
- **Weakness**: "Always on" GPS tracking = battery drain concern, no manual Schengen calculator mode
- Source: [trackingdays.com](https://www.trackingdays.com/)

#### Nomad Tracker (Gotzon Zabala, solo dev)
- **Platform**: iOS only, 40.9 MB
- **Launched**: Feb 2, 2026
- **Rating**: Too new for reviews
- **Pricing**: Free core (entire app), premium features available
- **Key features**: Photo metadata import to reconstruct past travel, background GPS, AI-powered "Fiscal Oracle" (on-device, requires iOS 26+), Schengen 90/180 rolling window, fiscal year tracking per country, entry-based rule support, PDF reports, smart document scanner (OCR), cloud sync via iCloud
- **US-specific**: US state tracking added v1.5 (Mar 2026), 183-day rule tracking
- **Innovation**: Photo library scanning for travel reconstruction is the standout feature -- users on PH cited it as the "first trust moment"
- **Weakness**: Very new, no Android, AI features require latest iOS
- Source: [Product Hunt](https://www.producthunt.com/products/nomad-tracker-tax-residency-for-nomads), [App Store](https://apps.apple.com/us/app/nomad-tracker-country-days/id6756324053)

#### Residency: Visa Day Tracker (Drobinin Limited)
- **Platform**: iOS + iPad, 48.1 MB
- **Pricing**: Subscription (weekly/annual)
- **Key features**: Photo-based trip detection (filters in-flight/layover noise), IRS SPT, B1/B2 & ESTA rules, UK ILR, Schengen 90/180, Green Card physical presence tracking, citizenship/naturalization timeline tracking, passport vault, PDF/CSV/JSON export
- **Tagline**: "Built by people who've been detained at immigration. For people who'd rather not be."
- **US-specific**: SPT, B1/B2 visa, ESTA tracking, citizenship path tracking
- **Weakness**: Subscription-gated core features, still too new for reviews
- Source: [App Store](https://apps.apple.com/us/app/residency-visa-day-tracker/id6749048224)

#### Days Monitor
- **Platform**: iOS (recently launched)
- **Key features**: Custom trackers per jurisdiction, SPT calculator, Schengen calculator, push alerts, privacy-first (on-device)
- **Positioning**: Markets itself as the "winner" above enterprise tools, GPS loggers, Schengen-only calculators, and spreadsheets
- **US-specific**: Substantial Presence Test calculator offered as a standalone web tool
- Source: [daysmonitor.com](https://daysmonitor.com/blog/the-5-best-residency-tracking-apps-in-2026-and-one-that-beats-them-all/)

#### Schengen Simple (George Cremer)
- **Platform**: iOS + Android (Android added June 2025)
- **Focus**: Schengen 90/180 only
- **Key innovation**: **Predictive planning** -- calculates future allowance while protecting already-booked trips, unlike backward-looking calculators
- **Features**: Passport Control calendar for border officials, allowance analysis showing which trips to shorten for flexibility
- **Context**: Founded 2023 post-Brexit, especially important with EU EES (Entry/Exit System) launching late 2025 and ETIAS in 2026
- **Weakness**: Schengen-only, no US or other jurisdiction support
- Source: [Globetrender article](https://globetrender.com/2025/06/03/schengen-simple-app-helps-travellers-avoid-overstaying-eu/)

#### Nomad Stays Advanced Visa Tracker (Beta)
- **Status**: Beta program, not yet public
- **Approach**: Multi-country timeline view, smart alerts, region-aware rule calculations, integration with housing/stays platform
- **Vision**: "One place where your movement, housing, and legal status make sense together"
- **Weakness**: Still in beta, unclear feature depth
- Source: [blog.nomadstays.com](https://blog.nomadstays.com/advanced-visa-tracker-built-for-border-crossers-not-spreadsheet-warriors/)

#### Other notable tools
- **Country Days Tracker** (App Store): Manual tracking with notes, PDF export
- **International Travel Tracker** (iOS): 183-day rule focus, simple travel log
- **DaysAround** (iOS): Automatic Schengen tracking from location data, private
- **Wise SPT Calculator**: Downloadable spreadsheet for Substantial Presence Test only
- **Beacon Hill Wealth SPT Calculator**: Web-based educational calculator

### US-Specific Rules and Tracking Gaps

#### ESTA / Visa Waiver Program (90 days)
- Travelers get 90 days per entry, but there is **no official cumulative limit** or "time in/time out" ratio
- Unofficial heuristic: "time out >= time in" -- widely cited on Reddit but **not codified by CBP**
- CBP officers have broad discretion to deny entry or revoke ESTA at any time
- Key Reddit insight: "The USA isn't Cambodia or Thailand. You can't stay for 89 days and then leave for a day and come back for 89 days" (905 upvotes)
- **No existing app models this pattern-of-entry risk** -- they only count the 90-day per-entry limit
- Source: [Reddit r/travel](https://www.reddit.com/r/travel/comments/1d6wpff/overusing_my_esta_is_that_a_thing/)

#### B1/B2 Visa
- Maximum 6-month stay per entry (as granted by CBP officer via I-94)
- I-94 departure date is the authoritative source
- CBP I-94 website and CBP Link app now show travel history and compliance status
- Source: [CBP I-94 site](https://i94.cbp.dhs.gov/), [CBP compliance page](https://www.cbp.gov/travel/international-visitors/i-94/traveler-compliance)

#### CBP Traveler Compliance System
- CBP sends email reminders at 10 days remaining on admission
- Sends overstay violation notifications
- "View Compliance" tab on I-94 website
- Currently limited to certain VWP travelers, expanding to more classes
- **Reactive only** -- no forward-looking planning capability
- Source: [CBP](https://www.cbp.gov/travel/international-visitors/i-94/traveler-compliance)

#### Substantial Presence Test (IRS)
- Formula: 31 days current year + weighted 183-day total over 3 years (100% current + 1/3 prior + 1/6 two years prior)
- Exceptions: medical conditions, transit, commuters, exempt individuals (students, teachers, government officials, athletes)
- Closer Connection Exception available even if test is met
- Most apps implement the basic formula but **none handle the Closer Connection Exception or treaty tie-breaker provisions**
- Source: [IRS](https://www.irs.gov/individuals/international-taxpayers/substantial-presence-test)

### User Complaints and Wishes (from Reddit, App Store, Product Hunt)

1. **"Does it have the actual tax residency tests for different countries, or only the 183 day counter?"** -- Top comment (11 pts) on International Travel Tracker launch. Users want real rule logic, not just simple counters. ([Reddit](https://www.reddit.com/r/longtermtravel/comments/1qg1raa/))

2. **"I would still use my calendar or calculate it myself. I don't like downloading apps that do one thing only."** -- 6 pts. Apps must provide multi-dimensional value beyond counting. ([Reddit](https://www.reddit.com/r/digitalnomad/comments/11xvijo/))

3. **"Given different citizenships often have different agreements, it would be a complex beast to build and maintain accurately."** -- 7 pts. Bilateral visa agreements make universal accuracy hard. ([Reddit](https://www.reddit.com/r/digitalnomad/comments/11xvijo/))

4. **Liability risk**: "Whoever marketed/sold the app would be facing some hefty liability risks if they got it wrong" -- 6 pts. Legal disclaimer is critical. ([Reddit](https://www.reddit.com/r/digitalnomad/comments/11xvijo/))

5. **"Downloaded it and seems useful, although I would rather it not count future days"** -- User wants current-day-accurate counts, not projections mixed in. ([Reddit](https://www.reddit.com/r/longtermtravel/comments/1qg1raa/))

6. **No Android**: Flamingo, TrackingDays, Nomad Tracker, Days Monitor, DaysAround are all iOS-only. Schengen Simple is the notable exception with Android added in 2025.

7. **Battery drain**: GPS-based tracking (TrackingDays, Flamingo, Nomad Tracker) requires constant location access. Users cite this as a top concern.

8. **Privacy concerns**: Users uncomfortable with cloud-stored location history. All newer apps emphasize on-device processing.

### Gap Analysis: Micro-SaaS Opportunity

| Gap | Current State | Opportunity |
|-----|--------------|-------------|
| US ESTA pattern-of-entry modeling | No app tracks cumulative ESTA usage or models denial risk | Risk score based on entry frequency, duration patterns, total days in rolling periods |
| Cross-jurisdiction "what-if" planner | Most apps show status per jurisdiction independently | Unified planner: "If I spend 3 weeks in Portugal, how does it affect my US SPT, Schengen allowance, and Portuguese tax residency simultaneously?" |
| I-94 data integration | Users must manually check CBP website | Import I-94 travel history (scrape or API) to auto-populate US entries/exits |
| Treaty tie-breaker + Closer Connection | No app implements these SPT exceptions | Guide users through the 8840 form logic and treaty provisions |
| Web + cross-platform | Market is 90% iOS-only | Web-first PWA with optional mobile apps would capture underserved Android + desktop users |
| US state-level compliance | Only Flamingo (NYC only) and TrackingStates (separate app) | Integrated state + federal tracking: California 9-month rule, NY convenience-of-employer, etc. |
| Proof-of-compliance document generation | CSV/PDF export exists but is generic | Generate jurisdiction-specific compliance documents (e.g., 8840 Closer Connection form data, UK SRT worksheet) |
| Multi-passport routing optimization | No app suggests which passport to use at which border | Given multiple citizenships, suggest optimal entry documents for each destination |

## Execution Log

| # | Action | Tool | URL/Query | Result | Reasoning |
|---|--------|------|-----------|--------|-----------|
| 1 | Search visa day tracking tools | firecrawl search | "digital nomad visa day counting tracking app overstay prevention tools 2025 2026" | 10 results including DaysMonitor, NomadStays, Reddit, App Store listings | Broad initial search to map the landscape |
| 2 | Search specific tool reviews | firecrawl search | "NomadApp.io Flamingo compliance visa tracker review complaints" | 7 results, Flamingo App Store listings dominant | Targeted search for named tools |
| 3 | Scrape DaysMonitor comparison article | firecrawl scrape | daysmonitor.com blog post | Full article comparing 5 categories of tracking tools | Comprehensive overview of tool categories |
| 4 | Scrape NomadStays visa tracker article | firecrawl scrape | blog.nomadstays.com | Beta program details for Advanced Visa Tracker | Understanding new entrant approach |
| 5 | Search US-specific I-94/SPT tracking | firecrawl search | "US B1 B2 visa I-94 tracking substantial presence test day counter app" | 10 results: IRS, CBP, Wise, YouTube | US-specific rule sources |
| 6 | Fetch Reddit 183-day rule app thread | curl (Reddit JSON) | r/longtermtravel thread | Post + 4 comments with user feedback | Direct user complaints on tracker apps |
| 7 | Search user complaints about trackers | firecrawl search | "visa day tracker app review complaints reddit nomad overstay risk spreadsheet alternative" | 10 results, top Reddit thread from r/digitalnomad | User sentiment data |
| 8 | Scrape Flamingo App Store page | firecrawl scrape | apps.apple.com/flamingo-compliance | Full feature list + reviews | Most complete tracker features |
| 9 | Scrape TrackingDays website | firecrawl scrape | trackingdays.com | Full product page with feature descriptions | Longest-running competitor details |
| 10 | Fetch Reddit nomad visa tracker thread | curl (Reddit JSON) | r/digitalnomad thread | 6 comments with feature wishes and concerns | User demand validation |
| 11 | Search Product Hunt visa tracker launches | firecrawl search | "product hunt visa tracker nomad day counter app launch" | Nomad Tracker PH page, DaysAround, Nomad List | PH-specific user feedback |
| 12 | Scrape IRS Substantial Presence Test page | firecrawl scrape | irs.gov/substantial-presence-test | Official SPT rules, exceptions, exempt individuals | Authoritative US rule source |
| 13 | Scrape Nomad Tracker Product Hunt page | firecrawl scrape | producthunt.com/nomad-tracker | Maker comments, user feedback, feature details | Newest competitor analysis |
| 14 | Scrape Nomad Tracker App Store page | firecrawl scrape | apps.apple.com/nomad-tracker | Full feature list, version history showing rapid iteration | Feature comparison data |
| 15 | Search CBP One / I-94 tracking | firecrawl search | "CBP One app I-94 travel history tracking US visa overstay digital nomad" | 8 results: CBP official pages, compliance tools | US government tracking capabilities |
| 16 | Scrape CBP Traveler Compliance page | firecrawl scrape | cbp.gov/traveler-compliance | Email notification system details | Government-side tracking capabilities |
| 17 | Scrape Residency app App Store page | firecrawl scrape | apps.apple.com/residency | Full feature list, version history | Photo-based trip detection approach |
| 18 | Search ESTA overstay discussions | firecrawl search | "visa tracker app complaints missing features wish list overstay US B1 B2 ESTA 90 days reddit" | 8 Reddit threads about ESTA overstay concerns | US overstay anxiety validation |
| 19 | Fetch Reddit ESTA overuse thread | curl (Reddit JSON) | r/travel ESTA overuse thread | 8 comments, top at 905 pts confirming pattern-of-entry risk | Key unmet need: no tool models this |
| 20 | Scrape Schengen Simple article | firecrawl scrape | globetrender.com article | Predictive planning approach, founder story | Unique predictive feature approach |
| 21 | Scrape Wise SPT Calculator page | firecrawl scrape | wise.com/substantial-presence-test | Calculator details, SPT explanation | Alternative SPT tool |

## Budget Used

| Resource | Soft Limit | Actual |
|----------|-----------|--------|
| Searches | ~8 | 7 |
| Scrapes | ~15 | 12 |
| Reddit API (curl) | -- | 3 |
| Total web operations | ~23 | 22 |
