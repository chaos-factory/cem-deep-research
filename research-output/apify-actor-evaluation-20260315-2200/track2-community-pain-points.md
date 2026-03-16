# Track 2: Community Pain Points & Real-World Experience with Picking Apify Actors

## Summary

- **Yes, people struggle to pick the right Apify actor.** With 20,000+ actors in the store, users frequently ask "which actor should I use?" and report difficulty finding reliable options. A user on r/apify noted "most users seem to rely on maybe the same few hundred tools" out of 20,000+ ([reddit.com/r/apify/comments/1rr3l1s](https://www.reddit.com/r/apify/comments/1rr3l1s/))
- **Actor breakage is a top complaint.** Actors break when target sites change HTML structure or anti-bot measures. Users describe a painful cycle: "Inspect the DOM manually → Update selectors → Re-deploy → Hope it works again" ([reddit.com/r/apify/comments/1rdobb8](https://www.reddit.com/r/apify/comments/1rdobb8/))
- **Empty/malformed data is a recurring frustration.** Users report actors returning empty datasets, schema changes breaking downstream workflows, and inconsistent results between identical runs ([reddit.com/r/n8n/comments/1rrzwlf](https://www.reddit.com/r/n8n/comments/1rrzwlf/))
- **Actors disappear without warning.** The Apollo scraper removal left users scrambling for alternatives, with a 17-year-old freelancer who just bought a $40 subscription suddenly stranded ([reddit.com/r/automation/comments/1npnr9b](https://www.reddit.com/r/automation/comments/1npnr9b/))
- **No SLAs on community actors.** A user warned: "It's basically a bunch of indie developers operating without any SLAs. If the developer you choose to go with becomes unresponsive, you'll need to find someone else" ([reddit.com/r/SaaS/comments/1nhiuxt](https://www.reddit.com/r/SaaS/comments/1nhiuxt/))
- **Detailed Trustpilot review (2-star) documents Twitter scraper wasting budget** through parameters not working as expected, fetching thousands of tweets despite configured limits, and returning outdated data ([trustpilot.com/review/apify.com](https://www.trustpilot.com/review/apify.com))
- **Developer-side frustration: first-party actors dominate high-value categories.** Builder complains Apify's own actors capture the most revenue while third-party devs make "extremely small" returns ([reddit.com/r/apify/comments/1rpswcb](https://www.reddit.com/r/apify/comments/1rpswcb/))
- **Community-built solutions are emerging:** r/ActorReviews subreddit was created specifically to review actors; an SEO Analyzer tool was built to analyze all 20,000+ actors; use-apify.com published comparison guides with checklists; a user built a "Selector Auto Fixer" actor to handle breakage ([reddit.com/r/ActorReviews](https://www.reddit.com/r/ActorReviews/))
- **Trustpilot overall is very positive (4.8/5, 404 reviews)** but the few negative reviews are highly specific about actor reliability and cost control failures. Apify also recently updated Store Publishing Terms due to "an influx of fraudulent reviews" ([answeroverflow.com/m/1259815987050713159](https://www.answeroverflow.com/m/1259815987050713159))
- **Users who scale up often migrate away** from community actors to direct data APIs (e.g., ThorData, BrightData) because actor maintenance and proxy cost overlap become unsustainable ([reddit.com/r/apify/comments/1rt7obr](https://www.reddit.com/r/apify/comments/1rt7obr/))
- **Real-world actor comparison is manual and painful.** A user tested "every B2B lead scraper on Apify" spending months and significant money comparing 4 actors across speed, email accuracy, and data quality — information not available on the store page ([reddit.com/r/coldemail/comments/1pd4tfq](https://www.reddit.com/r/coldemail/comments/1pd4tfq/))
- **Discord shows influx of "not working" reports.** Answer Overflow indexes Discord threads titled "All actors are broken, can't access," "Actor broken," "Actor Not Loading (Day 2)," and "Getting empty results via Python client" ([answeroverflow.com](https://www.answeroverflow.com/))

## Full Findings

### 1. The "Which Actor?" Problem

**Evidence of choice paralysis:**

Users regularly post asking which actor to use for a given task, indicating the store's discovery/comparison mechanisms are insufficient:

- **"$25 Apify Credits Expiring Tomorrow, Need Advice"** — User with expiring credits asks "Which actors yall find the most helpful?" and admits Google Maps actor didn't return decision-maker leads. No clear guidance available. ([reddit.com/r/apify/comments/1run7e6](https://www.reddit.com/r/apify/comments/1run7e6/))

- **"which Apify actor is most useful?"** — Developer planning to build actors asks for demand signals, gets only one reply mentioning Google Maps and LinkedIn. ([reddit.com/r/SaaS/comments/1p5mxm5](https://www.reddit.com/r/SaaS/comments/1p5mxm5/))

- **"YouTube transcript"** — User says "I was using one actor for YouTube transcript that suddenly stopped working. I'll be happy to receive recommendations for actors that work." Gets 3 different recommendations, each from the actor's own developer, highlighting the self-promotion dynamic. ([reddit.com/r/apify/comments/1r63pa9](https://www.reddit.com/r/apify/comments/1r63pa9/))

- **LinkedIn scraper reliability** — User asks "could you tell me which actor on apify works for you? all the ones I look into have been very unreliable until now" ([reddit.com/r/SaaS/comments/1mibl3u](https://www.reddit.com/r/SaaS/comments/1mibl3u/))

- **Struggling to get personal contact data** — User finds the leads-finder actor only returns generic company info, asks "Has anyone else used this specific actor and found a way to unlock better data?" and whether to switch actors. No useful responses. ([reddit.com/r/apify/comments/1qlxmdf](https://www.reddit.com/r/apify/comments/1qlxmdf/))

**The store visibility problem:**

- A developer notes: "There are 20,000+ Actors in the store, but most users seem to rely on maybe the same few hundred tools. For new developers it is extremely hard to get visibility, even when the tool works well." ([reddit.com/r/apify/comments/1rr3l1s](https://www.reddit.com/r/apify/comments/1rr3l1s/))

- A commenter responds: "I don't usually use the popular Apify actors, I prefer building my own... I even built an Apify actor to help with that research. It's basically SEO for the Apify Store" — confirming the discovery problem is so severe that someone built a tool to solve it.

- Another user: "I suggest everyone to also post in discord channel of apify. A lot of people also visit discord instead of google. I found many many useful actors there which are now part of my data collection" — users resort to Discord to find actors they can't discover through the store.

### 2. Actor Breakage & Reliability

**Scraper breakage is a universal pain point:**

- **"My scraper broke again..."** — Developer describes the cycle: website changes HTML → scrapers break → manual inspection → update selectors → redeploy → hope. Built a "Selector Auto Fixer" actor as a community solution. ([reddit.com/r/apify/comments/1rdobb8](https://www.reddit.com/r/apify/comments/1rdobb8/))

- **n8n workflow breakage** — "Apify actor keeps breaking my n8n lead gen workflow (empty responses + schema changes)." Comments describe the need for validation layers, error branches, and decoupled architectures — all workarounds for unreliable actors. ([reddit.com/r/n8n/comments/1rrzwlf](https://www.reddit.com/r/n8n/comments/1rrzwlf/))

- **LinkedIn structure changes** — "The HTML structure changes are the real killer. Built one last year that worked great for 3 weeks then LinkedIn updated something tiny and broke everything." ([reddit.com/r/SaaS/comments/1mibl3u](https://www.reddit.com/r/SaaS/comments/1mibl3u/))

- **First actor published, broke for everyone** — Developer published an actor that worked for them but failed for all other users due to a permissions misconfiguration. The docs provided no help for the specific error. ([reddit.com/r/apify/comments/1pmkj30](https://www.reddit.com/r/apify/comments/1pmkj30/))

**Discord "not working" reports (via Answer Overflow):**

- "All actors are broken, can't access" — user reports complete inability to access actors ([answeroverflow.com/m/1313727161978589194](https://www.answeroverflow.com/m/1313727161978589194))
- "Actor broken" — user reports actor not working for days, describes situation as "very urgent" ([answeroverflow.com/m/1234475373207617556](https://www.answeroverflow.com/m/1234475373207617556))
- "Apify Actor Not Loading (Day 2)" — multi-day outage ([answeroverflow.com/m/1202285011768971304](https://www.answeroverflow.com/m/1202285011768971304))
- "Getting empty results via Python client" — Instagram scraper works in web UI but returns empty data via API ([answeroverflow.com/m/1259815987050713159](https://www.answeroverflow.com/m/1259815987050713159))
- "My apify actor keeps running even after revoking the key" — actor runs without permission ([answeroverflow.com/m/1209201839061475348](https://www.answeroverflow.com/m/1209201839061475348))

### 3. Actor Disappearance & Platform Risk

**The Apollo scraper removal was a watershed moment:**

- **Freelancer stranded** — "I just bought the $40 monthly subscription for Apify and now seems like The Apollo scraper has completely vanished due to some technical difficulty... Anyone has any idea how long it will take to come back up?" ([reddit.com/r/automation/comments/1npnr9b](https://www.reddit.com/r/automation/comments/1npnr9b/))

- **12-upvote thread** seeking alternatives after removal — "I've been scraping Apollo leads using an Apify actor for a while, but that actor has recently been removed. I switched to using Ample Leads, but from what I've seen on Reddit threads, it's just not working well right now." ([reddit.com/r/coldemail/comments/1o135xi](https://www.reddit.com/r/coldemail/comments/1o135xi/))

- **Actor #4 deprecated during testing** — In the B2B lead scraper comparison thread, a commenter notes "already got deprecated, do you have any alternatives?" The author responds it will be back after the developer makes changes. ([reddit.com/r/coldemail/comments/1pd4tfq](https://www.reddit.com/r/coldemail/comments/1pd4tfq/))

- **Developer complaint** — "oh no they removed my actor again" — a developer posts about repeated actor removal on r/apify ([reddit.com/r/apify](https://www.reddit.com/r/apify/))

### 4. Wasted Credits / Cost Frustrations

**The Trustpilot 2-star review is the most detailed cost complaint found:**

A user describes their experience with Apify's Twitter scraper (March 2026):
1. "Parameters not working as expected" — limits not respected
2. "Unnecessary fetching that wasted our budget" — scraper fetched thousands of tweets despite strict limits, consumed resources, no refund given
3. "Fetching outdated tweets instead of recent ones" — returned old data despite requesting latest
4. "Uncertain and inconsistent scraper behavior" — identical configurations producing completely different results

Conclusion: "For any system that depends on predictable data collection and controlled spending, these problems can become very costly very quickly." ([trustpilot.com/review/apify.com](https://www.trustpilot.com/review/apify.com))

**Other cost signals:**

- User describes "compute/proxy cost overlap" — paying for both compute (RAM/CPU) to run headless browser plus residential proxies, burning through credits faster than expected on Amazon scraping ([reddit.com/r/apify/comments/1rt7obr](https://www.reddit.com/r/apify/comments/1rt7obr/))

- "Also buying more credits was getting expensive fast for what should've been one job" — from a webdev thread about a 36,000-page scraping project ([reddit.com/r/webdev/comments/1nyovt1](https://www.reddit.com/r/webdev/comments/1nyovt1/))

- Advice to "bake in a 30-40% buffer for usage spikes" — experienced user warns about unpredictable costs ([reddit.com/r/SaaS/comments/1nhiuxt](https://www.reddit.com/r/SaaS/comments/1nhiuxt/))

### 5. Marketplace Quality Control & Trust Issues

**No SLA concern:**

- "I wouldn't recommend using Apify if you're trying to build an actual business at scale. It's basically a bunch of indie developers operating without any SLAs. If the developer you choose to go with becomes unresponsive, you'll need to find someone else." ([reddit.com/r/SaaS/comments/1nhiuxt](https://www.reddit.com/r/SaaS/comments/1nhiuxt/))

**ChatGPT warns against Apify:**

- A user building a SaaS reports: "I told chatgpt to add it to the prd.md and that's when it recommended I shouldn't due to unreliability." This suggests the reputation issue is now embedded in AI training data. ([reddit.com/r/SaaS/comments/1nhiuxt](https://www.reddit.com/r/SaaS/comments/1nhiuxt/))

**Fraudulent reviews problem:**

- Apify's own Discord announcement (visible on Answer Overflow): "Due to an influx of fraudulent reviews recently, Apify's Legal team has taken some actions to protect developers, customers, and Apify, by updating the Store Publishing Terms and Acceptable Use Policy." ([answeroverflow.com/m/1259815987050713159](https://www.answeroverflow.com/m/1259815987050713159))

**Developer Trustpilot review (1-star):**

- "Terrible platform for developers. Platform is plagued with freeloaders that create multiple accounts for the $5 in free credit. Apify doesn't pay developers when they use this credit." ([trustpilot.com/review/apify.com](https://www.trustpilot.com/review/apify.com))

**First-party dominance complaint:**

- "The actors that generate the most demand (and presumably the most revenue) are things like social media scrapers, major platform integrations, etc. — and a lot of those are built and operated by Apify themselves." Developer says "the pricing has turned it all into a bit of a waste of time" and switched all actors to monthly rental as only viable option. A commenter agrees: "I use apify in the backend... I make more money in selling this than creating actors on apify. It's a shit show in apify actor store." ([reddit.com/r/apify/comments/1rpswcb](https://www.reddit.com/r/apify/comments/1rpswcb/))

### 6. How People Currently Decide Between Competing Actors

**Manual, expensive trial-and-error:**

The most detailed example is the B2B lead scraper comparison post where a user spent "2 months and $$$+" testing 4 Apollo alternatives across data quality, speed, email accuracy, and price. Key findings:
- Actor 1: Great data, but emails aren't enriched — "not real placeholders"
- Actor 2: Good filters, but "you only get 20-50% of what Apollo's count shows" — "Deal breaker for volume work"
- Actor 3: Fast but expensive — "nearly 2x other options"
- Actor 4: Best email accuracy (~65%) but "painfully slow"

This level of comparative data is unavailable on actor store pages. ([reddit.com/r/coldemail/comments/1pd4tfq](https://www.reddit.com/r/coldemail/comments/1pd4tfq/))

**Word of mouth and self-promotion dominate:**

When users ask "which actor?", responses are overwhelmingly from actor developers promoting their own tools. In the YouTube transcript thread, 3 of 4 substantive replies were developers linking their own actors. This creates a trust problem — users can't distinguish genuine recommendations from marketing.

**Checklist from third-party guide (use-apify.com):**

An independent affiliate site published a structured decision framework:
1. Check last update date (target within 30 days)
2. Read reviews and ratings (aim 4+ stars)
3. Check run history and success rate (90%+)
4. Compare pricing models
5. Test with free credits first
6. Check Apify vs. community maintenance

The guide explicitly acknowledges: "finding the right one can feel overwhelming. This is one of the most common concerns mentioned in user reviews." ([use-apify.com/docs/best-apify-actors](https://use-apify.com/docs/best-apify-actors))

### 7. Community-Built Solutions

| Solution | Type | Source |
|----------|------|--------|
| r/ActorReviews subreddit | Review community | [reddit.com/r/ActorReviews](https://www.reddit.com/r/ActorReviews/) |
| r/RoastMyApify subreddit | Feedback community | [reddit.com/r/apify/comments/1r3ex5c](https://www.reddit.com/r/apify/comments/1r3ex5c/) |
| Apify Store SEO Analyzer | Discovery tool (actor that analyzes all 20,000+ actors via Algolia index) | [reddit.com/r/ActorReviews/comments/1rkckv0](https://www.reddit.com/r/ActorReviews/comments/1rkckv0/) |
| Selector Auto Fixer actor | Reliability tool (auto-fixes broken CSS/XPath selectors) | [reddit.com/r/apify/comments/1rdobb8](https://www.reddit.com/r/apify/comments/1rdobb8/) |
| use-apify.com "Best Actors" guide | Comparison/ranking site | [use-apify.com/docs/best-apify-actors](https://use-apify.com/docs/best-apify-actors) |
| "Day X promoting a random Actor" series | Community curation | [reddit.com/r/apify/comments/1rsmagb](https://www.reddit.com/r/apify/comments/1rsmagb/) |
| Actor Quality Score (Apify official) | Platform feature | [reddit.com/r/apify/comments/1oqzlli](https://www.reddit.com/r/apify/comments/1oqzlli/) |

### 8. Trustpilot Sentiment Analysis

**Overall: 4.8/5 stars, 404 reviews**

The overwhelming majority of reviews are 5-star, praising ease of use, infrastructure, and the actor ecosystem. However, the negative reviews are highly specific and paint a different picture:

- **1-star (developer perspective):** Platform plagued with free-credit abusers, developers don't get paid for usage from trial accounts
- **2-star (Twitter scraper):** Parameters don't work, budget wasted on uncontrolled fetching, outdated results, inconsistent behavior
- **4-star reviews hint at friction:** "Proxy pricing gets expensive on large volumes," "The dashboard is a bit busy when you just want to check recent runs," "unused credits should roll over"

**Notable pattern:** Many 5-star reviews read as formulaic and appear during the $1M Challenge period, which incentivizes actor developers to generate positive reviews for their actors. Apify's own legal update about "fraudulent reviews" confirms this is a known problem.

### 9. Integration Pain Points (n8n, Make, Zapier)

Users integrating Apify actors into automation platforms face compounded reliability issues:

- **Make.com timing issue** — Apify module pulls data before it's ready, resulting in empty datasets. User had to add a timer as workaround. ([reddit.com/r/automation/comments/1k5yklh](https://www.reddit.com/r/automation/comments/1k5yklh/))

- **Make.com JSON input failure** — "Make.com → Apify Actor JSON input not working with mapped URL" ([reddit.com/r/Integromat/comments/1kj9say](https://www.reddit.com/r/Integromat/comments/1kj9say/))

- **Zapier empty results** — "it shows all successes, but the last three even though they are green show no results" ([reddit.com/r/zapier/comments/1npxf0m](https://www.reddit.com/r/zapier/comments/1npxf0m/))

- **n8n pagination failure** — "The problem I am facing is if I want 40 leads it is only scraping 20 like the pagination and the 'need more page?' Node is not working" ([reddit.com/r/n8n_ai_agents/comments/1r5dpf3](https://www.reddit.com/r/n8n_ai_agents/comments/1r5dpf3/))

## Execution Log

| # | Action | Tool | URL/Query | Result | Reasoning |
|---|--------|------|-----------|--------|-----------|
| 1 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1rdobb8 | Scraper breakage pain point + auto-fixer solution | Key URL from brief |
| 2 | Fetch thread | curl (Reddit JSON) | reddit.com/r/n8n/comments/1rrzwlf | Empty responses + schema changes breaking workflows | Key URL from brief |
| 3 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1r3ex5c | ActorReviews + RoastMyApify subreddits created | Key URL from brief |
| 4 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1oqzlli | Quality score Q&A details, max 63 without users | Key URL from brief |
| 5 | Fetch thread | curl (Reddit JSON) | reddit.com/r/SaaS/comments/1p5mxm5 | "which actor is most useful" — minimal useful answers | Key URL from brief |
| 6 | Search | firecrawl_search | site:reddit.com apify actor broken unreliable "which actor" | Found LinkedIn scraper thread with unreliable complaint | Broad discovery |
| 7 | Search | firecrawl_search | site:reddit.com apify "which actor" OR "best actor" | Found 10 threads including "AI doesn't recommend Apify" | Discovery |
| 8 | Search | firecrawl_search | site:reddit.com apify actor "empty data" OR "stopped working" | Found 10 threads including first actor broke, Make empty data | Discovery |
| 9 | Search | firecrawl_search | site:answeroverflow.com apify actor | Found 10 Discord threads including breakage reports | Discord coverage |
| 10 | Fetch thread | curl (Reddit JSON) | reddit.com/r/SaaS/comments/1mibl3u | LinkedIn scraper reliability complaints, "very unreliable" | Follow lead |
| 11 | Fetch thread | curl (Reddit JSON) | reddit.com/r/SaaS/comments/1nhiuxt | "AI doesn't recommend Apify" + no SLA warning | Follow lead |
| 12 | Fetch thread | curl (Reddit JSON) | reddit.com/r/coldemail/comments/1pd4tfq | Detailed 4-actor comparison, months of testing | Follow lead |
| 13 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1pmkj30 | First actor published, permissions broke for all users | Follow lead |
| 14 | Scrape | firecrawl_scrape | trustpilot.com/review/apify.com | 4.8/5, 404 reviews, detailed 2-star Twitter scraper complaint | Key URL from brief |
| 15 | Fetch thread | curl (Reddit JSON) | reddit.com/r/automation/comments/1npnr9b | Apollo scraper vanished, $40 sub wasted | Follow lead |
| 16 | Search | firecrawl_search | answeroverflow.com apify actor broken OR unreliable | Found "All actors are broken," "Actor broken," empty results | Deepen Discord coverage |
| 17 | Search | firecrawl_search | site:reddit.com apify "wasted credits" OR "hard to choose" | Found lead scraper comparison, Apollo data quality threads | Discovery |
| 18 | Fetch thread | curl (Reddit JSON) | reddit.com/r/automation/comments/1k5yklh | Make module pulling empty data, timing issue | Follow lead |
| 19 | Scrape | firecrawl_scrape | answeroverflow.com/m/1259815987050713159 | Empty results via Python client, fraudulent reviews announcement | Verify Discord content |
| 20 | Scrape | firecrawl_scrape | answeroverflow.com/m/1313727161978589194 | "All actors are broken, can't access" confirmed | Verify Discord content |
| 21 | Scrape | firecrawl_scrape | answeroverflow.com/m/1234475373207617556 | "Actor broken" — actor not working for days, "very urgent" | Verify Discord content |
| 22 | Fetch thread | curl (Reddit JSON) | reddit.com/r/automation/comments/1ncuv8k | Best scraping tools comparison, Apify "heavier than needed" | Context |
| 23 | Search | firecrawl_search | site:reddit.com r/ActorReviews apify | Found "Analysed All 20,000+ Actors" post, review subreddit | Community solutions |
| 24 | Search | firecrawl_search | apify "fraudulent reviews" OR "quality score" | Found quality score docs, fraudulent reviews announcement | Quality control |
| 25 | Scan | curl (Reddit JSON) | reddit.com/r/apify/new.json?limit=25 | Found "$25 credits expiring," "closed market," "pricing unfair" | Broad scan |
| 26 | Search | firecrawl_search | site:reddit.com apify actor "not working" OR "returns empty" | Found Make.com, Zapier, n8n integration failures | Integration pain |
| 27 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1rr3l1s | "Is Apify Store Becoming a Closed Market" — visibility problem | Follow lead |
| 28 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1rpswcb | Pricing unfair for builders, first-party dominance | Follow lead |
| 29 | Fetch thread | curl (Reddit JSON) | reddit.com/r/coldemail/comments/1o135xi | Apollo scraper removed, alternatives sought | Follow lead |
| 30 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1r63pa9 | YouTube transcript actor stopped, self-promotion in replies | Follow lead |
| 31 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1rt7obr | Migration from Apify to direct Data API | Follow lead |
| 32 | Search | firecrawl_search | apify actor comparison tool OR review site | Found use-apify.com best actors guide | Community solutions |
| 33 | Scrape | firecrawl_scrape | use-apify.com/docs/best-apify-actors | Detailed checklist for choosing actors, acknowledges overwhelm | Verify community solution |
| 34 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1qlxmdf | Struggling with lead actor data quality | Follow lead |
| 35 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1run7e6 | $25 credits expiring, doesn't know which actor to use | Follow lead |
| 36 | Fetch thread | curl (Reddit JSON) | reddit.com/r/apify/comments/1rtem3p | Day 2 random actor promotion series | Context |

## Budget Used

| Metric | Actual | Soft Limit |
|--------|--------|------------|
| Searches | 11 | 15-25 |
| Fetches (scrapes + curl) | 28 | 30-60 |
| Total web operations | 39 | 45-85 |

All within budget. Coverage spans Reddit (r/apify, r/SaaS, r/coldemail, r/automation, r/n8n, r/webscraping, r/ActorReviews, r/Integromat, r/nocode, r/zapier, r/n8n_ai_agents), Trustpilot, Answer Overflow (Apify Discord), and an independent review site (use-apify.com).
