# Track 1: Apify User Reviews & Community Pain Points

## Summary

- **Pricing unpredictability is the #1 complaint**: Credit/compute-unit billing makes budgeting nearly impossible; users report unexpected charges from actors ignoring configured limits, bills spiking with headless browser usage, and no cost estimation before runs ([Trustpilot](https://www.trustpilot.com/review/apify.com?stars=1&stars=2&stars=3), [Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Prospeo](https://prospeo.io/s/apify-alternatives))
- **Marketplace actor quality is inconsistent**: Community-built actors break when target sites update, have varying documentation quality, and some are abandoned with commits months old ([Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Trustpilot](https://www.trustpilot.com/review/apify.com), [Browse.ai](https://www.browse.ai/vs/apify))
- **Actor breakage when target sites change**: Scrapers for platforms like LinkedIn, Facebook, Instagram, and Twitter frequently break after UI changes, requiring manual fixes or waiting on maintainers ([Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Reddit r/AI_Agents](https://www.reddit.com/r/AI_Agents/comments/1qjkotq/))
- **Apollo scraper removal broke entire user workflows**: Apify removed Apollo scrapers, breaking lead generation pipelines overnight with no warning, forcing users to scramble for alternatives ([Reddit r/coldemail](https://www.reddit.com/r/coldemail/comments/1o4lrpa/), [Reddit r/EntrepreneurRideAlong](https://www.reddit.com/r/EntrepreneurRideAlong/comments/1o0ckc9/))
- **Developer marketplace economics are unsustainable**: Actor developers earn very little revenue; highest-value categories are dominated by Apify's own first-party actors; free-tier freeloaders abuse the platform and developers don't get paid for those runs ([Reddit r/apify](https://www.reddit.com/r/apify/comments/1rpswcb/), [Trustpilot 1-star](https://www.trustpilot.com/review/apify.com?stars=1&stars=2&stars=3))
- **Steep learning curve for non-developers**: Proxy configuration, memory usage, actor parameters, and debugging require technical knowledge despite no-code marketing ([Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Software Advice](https://www.softwareadvice.com/data-extraction/apify-profile/reviews/))
- **Billing disputes handled poorly**: Users report unresponsive support, refusal to refund for platform-triggered runs, gaslighting during billing disputes, and threats to escalate to Czech Trade Inspection Authority ([Trustpilot](https://www.trustpilot.com/review/apify.com?stars=1&stars=2&stars=3))
- **Twitter/X scraper is unreliable**: Parameters don't work as expected, fetches thousands of tweets despite strict limits, returns outdated data, inconsistent results between identical runs ([Trustpilot](https://www.trustpilot.com/review/apify.com?stars=1&stars=2&stars=3))
- **Credits don't roll over**: Unused monthly credits are lost, which feels punitive during lighter usage months ([Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Trustpilot](https://www.trustpilot.com/review/apify.com))
- **UI/dashboard is overwhelming and cluttered**: Multiple users describe the interface as crowded, hard to navigate for beginners, with too many buttons and settings ([Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Software Advice](https://www.softwareadvice.com/data-extraction/apify-profile/reviews/))
- **Customer support is slow or non-responsive**: Chat support described as having "zero response"; no ticket system; support quality restricted by pricing plan ([Trustpilot](https://www.trustpilot.com/review/apify.com?stars=1&stars=2&stars=3), [Capterra](https://www.capterra.com/p/150854/Apify/reviews/))
- **Proxy pricing escalates on large volumes**: Users paying $25+ for actor plus proxy fees on Facebook data collection; bulk scraping cost is high ([Trustpilot](https://www.trustpilot.com/review/apify.com))
- **Data quality issues with scraped results**: Irrelevant metadata fields, partially broken data, email accuracy problems (~45-65% deliverability on lead scrapers), and inconsistent Instagram scraping results ([Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Reddit r/coldemail](https://www.reddit.com/r/coldemail/comments/1pd4tfq/), [Apify Issues](https://apify.com/apify/instagram-post-scraper/issues/not-reliable-scrapin-KJdVhdEExefs04KfS))

---

## Full Findings

### 1. Pricing Unpredictability & Hidden Costs

**The single most recurring complaint across all sources.** Apify's compute-unit billing model makes it extremely difficult for users to predict costs.

**Capterra reviews:**
- Dominik L. (Freelancer, 5/5): "The primary drawback is the steep learning curve for non-developers and the credit-based pricing model, which can be confusing and lead to unexpected costs when scaling."
- Clinton W. (Owner, 5/5): "Pricing Can Spiral. While the free tier is generous, larger scrapes (especially with headless browsers like Playwright) eat up compute units fast. If you don't monitor usage, your bill can spike quickly."
- Jonathan C. (Director, 5/5): "Pricing can ramp up quickly if you're running high-volume or frequent scrapers."
- Chris G. (Solopreneur, 5/5): "The pricing on Apify is kind of confusing. They have a subscription fee, then on top of that there are different kinds of pricing per each actor."
- Saif R. (Founder, 5/5): "Wish there was a way to estimate how much a run will cost before you actually run it."
- Paul A. (Software Engineer, 4/5): "Credits don't roll over. Unused monthly credits are lost, which feels punitive during lighter usage months."
- Arnau M. (Data Helper, 5/5): "It can be a bit expensive sometimes, especially if you have to rent an actor + pay for their usage."
- Sabahudin M. (Founder, 5/5): "Actor pricing because when you compare this with other tools you will probably pay a way more regarding to the same problem."
- Veysel Resit C. (CS Engineer, 5/5): Listed "Pricing and Billing Transparency" as a con.

**Trustpilot reviews:**
- 1-star review (Feb 14, 2026): "I experienced unexpected charges (around $4.01) for very short Actor runs (around 9-25 seconds) with minimal results... The platform should clearly show a breakdown of costs (compute, proxy, storage/egress, any 'pay-per-event' minimum fees/rounding)."
- 1-star review (Feb 3, 2026): Actor triggered after being disabled, ran for 3.5 hours consuming 912,109 results. Charge: $456.05. "Our system logs definitively proved we didn't initiate the run."
- 4-star review: "Main issue is proxy pricing gets expensive on large volumes. Pay around $25 for actor plus proxy fees."
- 5-star review: "Price, perhaps could be a bit lower when scraping in Bulk."
- 5-star review: "Sure, it's maybe a bit pricey compared to other options."
- Review on credits: "Unused credits should roll over between months."

**Software Advice reviews:**
- Naftal O. (3/5): "Payment not clear, too much unclear approaches to payment of different actors."
- Mahmoud A. (5/5): "The pricing docs / structure" listed as a con.

**Browse.ai comparison:** "Complex compute unit calculations make budgeting unpredictable. Variable costs per extraction depending on Actor efficiency. Same extraction can cost differently each time."

**Prospeo alternatives article:** "Compute-unit billing surprises are the number-one complaint. A Google Maps scrape for 1,000 listings can cost $7+ when factoring in compute unit consumption and proxy bandwidth. Predictable budgeting is nearly impossible."

Source: [Prospeo](https://prospeo.io/s/apify-alternatives), [Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Trustpilot](https://www.trustpilot.com/review/apify.com?stars=1&stars=2&stars=3)

---

### 2. Marketplace Actor Quality & Reliability

**Community-built actors vary wildly in quality, break frequently, and can be abandoned.**

**Capterra reviews:**
- Atharva P. (Founder, 5/5): "Some actors on this site have poor quality and guide documentation, and it takes more trials before I get my desired results."
- Valentin Q. (Co-founder, 4/5): "The biggest drawback is that not all actors maintain the same quality standards, leading to unpredictable results and forcing me to test multiple options before finding reliable ones."
- Jehu Zachary S. (Web Scraping Specialist, 5/5): "Some actors break when platforms like Facebook or LinkedIn update their UI."
- Clinton W. (Owner, 5/5): "Some marketplace actors break when target websites change structure (which happens often)."
- Benoit P. (Cofounder/CMO, 4/5): "Sometimes actors are not really efficient so you have to modify code to get results."
- Verified Reviewer (Founder, 5/5): "When websites update their layout, crawlers can break and need adjustments."

**Software Advice reviews:**
- ever a. (5/5): "Some actors are not well-maintained or reviewed, which means they don't always work as expected."

**Trustpilot:**
- 3-star review: "Good but difficult to find the best actor for a use case."

**Browse.ai comparison:** "Relies on third-party Actor developers who may abandon projects. Variable quality across different Actors in the marketplace. No control over when or how Actors are updated."

**Prospeo:** "Community-built Actors have wildly varying upkeep levels; when target sites change structure, users wait on maintainers for fixes. Community Actors sometimes have 'last commit was four months ago,' indicating abandonment."

Source: [Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Browse.ai](https://www.browse.ai/vs/apify), [Prospeo](https://prospeo.io/s/apify-alternatives)

---

### 3. Apollo Scraper Removal & Dependency Risk

**Apify's removal of Apollo scrapers broke many lead generation workflows overnight, exposing the fragility of depending on the platform.**

**Reddit r/coldemail (u/Adventurous-Lie-9209):** "I am sure everyone now knows that Apify removed their apollo scrapers and now their scrapers are either too expensive or useless. I just want to see if people found any good replacement sites for Apollo/LinkedIn sales nav scraping."

**Reddit r/EntrepreneurRideAlong (u/original poster):** "Two months ago I built an AI agent called LeadForge. It scraped Apollo and LinkedIn to find leads, enrich them, and write cold emails automatically. It was working beautifully..until one morning, both the Apollo scrapers I used (Apify + Ample Leads) went down. No warnings. Just gone. That completely broke my workflow. Weeks of work... buried."

**Reddit r/coldemail (u/erickrealz):** "Apify scrapers that break constantly. Our clients scraping Sales Nav use Phantombuster mostly because it's stable."

**Reddit r/coldemail (Apollo blocking thread):** Users reported scrapers going down with no warning, scrambling for workarounds. "Seems like Apollo is now blocking all scrapers. Anyone have a workaround?"

**Reddit r/coldemail (B2B lead scraper testing):** After Apollo ban, user spent months and significant money testing alternatives. Found email accuracy ranged only 45-65% across scrapers. One scraper (lead-finder #4) "already got deprecated."

Source: [Reddit r/coldemail replacement thread](https://www.reddit.com/r/coldemail/comments/1o4lrpa/), [Reddit r/EntrepreneurRideAlong](https://www.reddit.com/r/EntrepreneurRideAlong/comments/1o0ckc9/), [Reddit Apollo blocking](https://www.reddit.com/r/coldemail/comments/1nzjnhl/), [Reddit B2B testing](https://www.reddit.com/r/coldemail/comments/1pd4tfq/)

---

### 4. Developer Marketplace Economics

**Developers building public actors find the economics unsustainable. Apify dominates high-value categories with first-party actors.**

**Reddit r/apify (u/gcampb41, Actor developer):** "I've built a number of actors over time and some of them get used fairly regularly...But when I actually look at the numbers, the revenue coming back to the developer is extremely small relative to the usage. The actors that generate the most demand (and presumably the most revenue) are things like social media scrapers, major platform integrations, etc. - and a lot of those are built and operated by Apify themselves."

**Same user in reply:** "The pricing has turned it all into a bit of a waste of time. The ones that get the high usage are owned by Apify..who you can't really compete with.. it's a race to the bottom. I've just put a 29.99 monthly rental on all my actors today. It's a shame because it could have been quite an equitable platform for developers, but I won't be building anything else."

**Reddit r/apify (u/Careless-inbar):** "I use apify in the backend and for front end I modify it according to customer needs. I make more money in selling this than creating actors on apify. It's a shit show in apify actor store."

**Trustpilot 1-star (Oct 7, 2025):** "Terrible platform for developers. Platform is plagued with freeloaders that create multiple accounts for the $5 in free credit. Apify doesn't pay developers when they use this credit, even though it costs us to process those requests. There's tons of abuse on this platform, and worse, the support doesn't appear to care or respond when brought to their attention."

**Reddit r/apify (u/Otherwise-Resolve252):** "They appear to be prioritizing MCP because agents can utilize actors under a pay-per-event pricing model." (Suggesting strategic shift away from developer-friendly economics)

Source: [Reddit r/apify pricing thread](https://www.reddit.com/r/apify/comments/1rpswcb/), [Trustpilot](https://www.trustpilot.com/review/apify.com?stars=1&stars=2&stars=3)

---

### 5. Billing Disputes & Customer Support Failures

**Multiple users report hostile or absent responses when disputing charges, including platform-triggered runs being billed to users.**

**Trustpilot 1-star (Feb 3, 2026, titled "AVOID APIFY AT ALL COSTS"):**
- Actor was "explicitly disabled, yet triggered hours later and ran uncontrolled during the night for 3.5 hours, consuming 912,109 results"
- Charge: $456.05
- "Our system logs definitively proved we didn't initiate the run"
- "Apify's own technical team acknowledged this was 'an automated workflow' continuing after disablement - essentially confirming their platform error. Yet support refused accountability."
- Apify claimed run was "triggered via API" with no evidence, admitted they don't retain API logs longer than 7 days
- User threatened to escalate to Czech Trade Inspection Authority

**Trustpilot 1-star (Feb 14, 2026):** "I tried contacting support through the in-app chat and got no response, so it's hard to clarify what exactly I'm being charged for."

**Trustpilot 1-star (Sep 20, 2025):** "Zero customer support, their chat support has zero respond, looks like they have no employees to address customers issues. Even they don't have a ticket system where we can raise our concerns."

**Trustpilot meta-note:** Trustpilot flags that Apify "Hasn't replied to negative reviews" on the platform.

**Capterra reviews:**
- James R. (Director AIML, 4/5): "The user interface is cumbersome and support is quite slow."

Source: [Trustpilot negative reviews](https://www.trustpilot.com/review/apify.com?stars=1&stars=2&stars=3)

---

### 6. Twitter/X Scraper Unreliability

**Detailed 2-star Trustpilot review documenting systematic problems with the Twitter scraper.**

**Trustpilot 2-star (Mar 3, 2026):**
1. "Parameters not working as expected - Even when we configured limits such as maximum items to fetch, the scraper did not always respect them."
2. "Unnecessary fetching that wasted our budget - On several occasions the scraper fetched thousands of tweets even though strict limits were configured. These runs consumed a large amount of resources and unexpectedly increased our costs."
3. "Fetching outdated tweets instead of recent ones - The scraper frequently returned old tweets instead of the latest ones... tweets from the previous day appeared while tweets posted within the last hour were missing entirely."
4. "Uncertain and inconsistent scraper behavior - Identical configurations would sometimes produce completely different results between runs."

Source: [Trustpilot](https://www.trustpilot.com/review/apify.com?stars=1&stars=2&stars=3)

---

### 7. Steep Learning Curve & UI/UX Issues

**Recurring theme across all review platforms - especially problematic for non-technical users.**

**Capterra reviews:**
- Leroy S. (Management Support, 5/5): "At the start it was also a little confusing because there were many buttons and settings, and I did not know what to click."
- Peter L. (Lawyer, 5/5): "Some options could have been better explained, like proxy or memory usage because I am non professional."
- Aliff R. (CEO, 5/5): "The user interface was overwhelming and cluttered, making it confusing and hard to navigate easily."
- Jonathan Enrique N. (Owner, 5/5): "One thing that I don't like about Apify is the UI interface because it seems a little crowded."
- Ashutosh Kumar T. (Student, 4/5): "Documentation is a bit tricky for me, sometimes I find it difficult to understand a particular part."
- Maryam A. (Research Assistant, 5/5): "Apify's scheduling feature lacks the ability to dynamically adjust date ranges for actors, forcing users to manually define fixed intervals."
- Dev N. (Backend Engineer, 5/5): "Steep learning curve, limited data cleaning, debugging can be tricky, and mobile management is clunky."

**Software Advice:**
- Arnold Benedict M. (Full Stack Automation Architect, 5/5): "When you manage many actors, the UI can feel a bit crowded, and I would like stronger built-in dashboards and alerting."

Source: [Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Software Advice](https://www.softwareadvice.com/data-extraction/apify-profile/reviews/)

---

### 8. Data Quality & Email Accuracy Issues

**Scraped data quality is problematic, especially for lead generation use cases.**

**Capterra:**
- Esther A. (Co-Founder, 5/5): "Sometimes the returned data includes too many irrelevant metadata fields, so you have to spend time cleaning up results."
- Vansh A. (CTO, 5/5): "It does not have an inbuilt database table for storing data even though it lets you export the scraped data but a clean database would be so much better."

**Reddit r/coldemail (B2B scraper testing):** User tested multiple Apify B2B lead scrapers after Apollo ban. Email accuracy findings:
- olympus/b2b-leads-finder: "Email accuracy: Major issue - emails aren't enriched, just not real placeholders"
- code_crafter/leads-finder: "~45% deliverability" and "you only get 20-50% of what Apollo's count shows"
- microworlds/leads-generator: "~60% deliverable" but "Expensive, nearly 2x other options"
- amr-mando/lead-finder: "~65% deliverable, best I've tested" but "Painfully slow"

**Apify Issues page (Instagram Post Scraper):** "I am trying to scrape Instagram data to run an observational study. However, the scraped data is not reliably the same every time, even if scraping the same target."

**Prospeo:** "Even successful runs can return partially broken data (example: 200 of 1,000 results problematic)."

Source: [Reddit r/coldemail](https://www.reddit.com/r/coldemail/comments/1pd4tfq/), [Capterra](https://www.capterra.com/p/150854/Apify/reviews/), [Apify Issues](https://apify.com/apify/instagram-post-scraper/issues/not-reliable-scrapin-KJdVhdEExefs04KfS)

---

### 9. Account Management Issues

**Trustpilot 1-star (Jul 24, 2025):** "I lost my login details for an old email address I used for Apify and had to create another account. They blocked the second account, too, saying that I created multiple accounts and had abused the platform's free resources. I have never even used a single api from their platform."

**Trustpilot 1-star (Apr 11, 2025):** "Can't even signup, it forces you to use Google signup but it doesn't even work."

**Trustpilot 1-star (Oct 27, 2025):** "Horrible setup to pop up the upgrade pop up."

Source: [Trustpilot](https://www.trustpilot.com/review/apify.com?stars=1&stars=2&stars=3)

---

### 10. Scraper Fragility as Industry-Wide Problem (Apify-Amplified)

**Reddit r/AI_Agents (u/nanohuman_ai, 8 upvotes):** "I spent 3 years building the 'perfect' custom scraper. Then I realized my job was 'Data Scientist,' not 'Cat-and-Mouse Game Professional against Cloudflare.'"

**Reddit r/AI_Agents (u/hasdata_com, 8 upvotes):** "You can't build a set and forget scraper without massive infra. We run synthetic tests 24/7 just to keep uptime high."

**Reddit r/webscraping (u/amralaaalex, 4 upvotes):** "Apify is slow and expensive. I just finished moving my company apify scrapers to scrapy framework saving more than 90% of the cost."

**Reddit r/AI_Agents (general pattern):** Multiple users describe Apify as one option among many but note its cost relative to alternatives. Users switching to Playwright/Puppeteer directly, or to services like Bright Data, Zyte, ScrapingBee.

Source: [Reddit r/AI_Agents](https://www.reddit.com/r/AI_Agents/comments/1qjkotq/), [Reddit r/webscraping](https://www.reddit.com/r/webscraping/comments/rbq4pl/)

---

### 11. Workarounds Users Employ

1. **Switch to monthly rental pricing** to make actor development economically viable (r/apify developer thread)
2. **Use Apify as backend only**, build custom front-end for clients (r/apify u/Careless-inbar)
3. **Layer email verification tools** on top of Apify lead scrapers due to poor email accuracy (r/coldemail multiple users)
4. **Abandon scraping entirely**, switch to legitimate API access for platforms like Apollo (r/coldemail u/erickrealz)
5. **Rebuild workflows without scraping dependencies** after breakages (r/EntrepreneurRideAlong LeadForge story)
6. **Use alternative tools** like Phantombuster for LinkedIn (more stable), Bright Data for proxies, self-hosted Scrapy/Crawlee for cost savings
7. **Monitor usage obsessively** to avoid bill spikes - multiple reviewers mention needing to actively watch credit consumption
8. **Test multiple actors** before committing, since quality varies widely across the marketplace

---

## Execution Log

| # | Action | Tool | URL/Query | Result | Reasoning |
|---|--------|------|-----------|--------|-----------|
| 1 | Scrape G2 reviews | firecrawl_scrape | https://www.g2.com/products/apify/reviews | 403 Forbidden - G2 blocks scraping | Primary review source |
| 2 | Scrape Capterra reviews | firecrawl_scrape | https://www.capterra.com/p/150854/Apify/reviews/ | Success - 25 reviews with pros/cons | Primary review source |
| 3 | Scrape Trustpilot | firecrawl_scrape | https://www.trustpilot.com/review/apify.com | Success - 404 reviews, mostly positive with key negatives | Primary review source |
| 4 | Fetch Reddit pricing thread | curl (Reddit JSON) | r/apify/comments/1rpswcb | Success - developer marketplace complaint | Key pain point source |
| 5 | Fetch Reddit replacement thread | curl (Reddit JSON) | r/coldemail/comments/1o4lrpa | Success - Apollo removal fallout | Dependency risk evidence |
| 6 | Fetch Reddit Scrapy thread | curl (Reddit JSON) | r/webscraping/comments/rbq4pl | Success - cost comparison | Alternative perspective |
| 7 | Fetch Reddit open-source thread | curl (Reddit JSON) | r/opensource/comments/1fxf960 | Success - alternatives discussion | Context |
| 8 | Fetch Reddit AI_Agents thread | curl (Reddit JSON) | r/AI_Agents/comments/1qjkotq | Success - scraper reliability discussion | Industry context |
| 9 | Fetch Reddit LeadForge thread | curl (Reddit JSON) | r/EntrepreneurRideAlong/comments/1o0ckc9 | Success - product collapse story | Dependency risk |
| 10 | Fetch Reddit Apollo blocking | curl (Reddit JSON) | r/coldemail/comments/1nzjnhl | Success - blocking workarounds | Breakage evidence |
| 11 | Scrape Trustpilot negative | firecrawl_scrape | trustpilot.com (stars=1,2,3 filter) | Success - 8 negative reviews found | Critical complaints |
| 12 | Search Reddit complaints | firecrawl_search | "Apify complaints problems issues site:reddit.com" | 10 results, 3 relevant | Discovery |
| 13 | Search negative reviews | firecrawl_search | "Apify review negative expensive broken scraper" | 10 results, 5 relevant | Discovery |
| 14 | Fetch Reddit B2B testing | curl (Reddit JSON) | r/coldemail/comments/1pd4tfq | Success - email accuracy data | Data quality evidence |
| 15 | Fetch G2 pros/cons | WebFetch | g2.com/products/apify/reviews?qs=pros-and-cons | 403 Forbidden | Blocked |
| 16 | Search Apify broken actors | firecrawl_search | "Apify actor broken stopped working" | 10 results, identified r/apify patterns | Discovery |
| 17 | Scrape Capterra page 2 | firecrawl_scrape (JSON) | capterra.com page 2 | Success - 25 complaints extracted | More review data |
| 18 | Search pricing complaints | firecrawl_search | "apify pricing expensive credits cost" | 10 results, Prospeo/IGLeads relevant | Pricing evidence |
| 19 | Fetch Prospeo alternatives | WebFetch | prospeo.io/s/apify-alternatives | Success - detailed criticisms | Third-party analysis |
| 20 | Fetch Browse.ai comparison | WebFetch | browse.ai/vs/apify | Success - marketplace/maintenance critique | Competitor perspective |
| 21 | Scrape Software Advice | firecrawl_scrape (JSON) | softwareadvice.com reviews | Success - 13 complaints extracted | Additional review source |
| 22 | Fetch Reddit Apollo leads | curl (Reddit JSON) | r/coldemail/comments/1npm5nz | Success - data quality discussion | Enrichment context |
| 23 | Search developer payouts | firecrawl_search | "Apify developer payout unfair marketplace" | 5 results, confirmed r/apify thread | Marketplace economics |
| 24 | Get r/apify top posts | curl (Reddit JSON) | r/apify/top.json | Success - 25 top posts scanned | Subreddit overview |
| 25 | Search data quality | firecrawl_search | "Apify scraper unreliable inconsistent data quality" | 8 results, Instagram issues found | Data quality |

## Budget Used

- **Searches**: 6 / ~25 soft limit
- **Fetches**: 25 / ~60 soft limit (including curl calls, scrapes, and WebFetch)
- **Total operations**: 31 (well within budget)
- Note: G2 was inaccessible (403) via both firecrawl and WebFetch, so coverage relies on Capterra, Trustpilot, Software Advice, and Reddit instead. The Trustpilot negative filter and Capterra JSON extraction compensated effectively.
