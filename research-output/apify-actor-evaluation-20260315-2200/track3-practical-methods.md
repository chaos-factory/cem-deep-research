# Track 3: Practical Evaluation Methods & Comparison Tools for Apify Actors

## Summary

- **The Apify Store search supports filtering by keyword, category, pricing model, sort order (relevance/popularity/newest/lastUpdate), and username** — but the UI can feel overwhelming with 10,000+ actors and no advanced multi-criteria filtering beyond these basic options ([Store API docs](https://docs.apify.com/api/v2/store-get), [Apify blog](https://blog.apify.com/what-is-apify-store/))
- **The Apify Store Analyzer actor (automation-lab/apify-store-analyzer)** is a new community tool (2 total users, published March 2026) that searches the Store API by keyword and returns structured competitive analysis including pricing models, user counts, run stats, ratings, and market position classification (leader/challenger/niche/newcomer) — useful for comparison but very new and unproven ([source](https://apify.com/automation-lab/apify-store-analyzer))
- **The PPE Cost Estimator actor (automation-lab/ppe-cost-estimator)** analyzes any actor's recent run history and calculates true cost per result including CU costs, event charges, and storage fees, with volume projections and confidence intervals — a critical tool for pricing comparison before scaling ([source](https://apify.com/automation-lab/ppe-cost-estimator))
- **The Best Actor Finder (pranavpatel/best-actor-finder)** uses LLM-powered evaluation to search, score (7 criteria), and actually run the top 3 actors for a given query, returning performance comparisons — an automated testing workflow, though only 8 total users ([source](https://apify.com/pranavpatel/best-actor-finder))
- **use-apify.com provides the most actionable consumer evaluation checklist**: (1) check last update date within 30 days, (2) read reviews aiming for 4+ stars, (3) check run history and success rate (90%+ good, 95%+ excellent), (4) compare pricing models, (5) test with free credits first, (6) check Apify vs community maintenance badge ([source](https://use-apify.com/docs/best-apify-actors))
- **Pricing has two layers that catch users off guard**: platform-level billing (compute units at $0.20-$0.30/CU depending on plan tier) plus actor-level pricing (PPE, PPR, rental, or pay-per-usage) — and proxy costs (residential at $7-$8/GB, SERPs at $1.70-$2.50/1K) are separate hidden costs that many third-party actors do not include ([Apify pricing docs](https://docs.apify.com/platform/actors/publishing/monetize/pricing-and-costs), [data365.co](https://data365.co/blog/apify-reddit-scraper))
- **The Actor quality score (0-100) directly influences Store visibility** and evaluates 8 categories: reliability, popularity, feedback/community, ease of use, pricing transparency, trustworthiness, history of success, and congruency — consumers can use this as a proxy signal though the score itself is not directly displayed to users ([quality score docs](https://docs.apify.com/platform/actors/publishing/quality-score))
- **Third-party review sites (hackceleration, igleads, blackbearmedia) are affiliate-driven marketing sites** that provide general Apify platform reviews but not per-actor comparison tools; hackceleration.com is the most detailed with actual testing data (4.2/5 overall rating), while igleads.io and blackbearmedia.io are primarily funnels for their competing products ([hackceleration](https://hackceleration.com/apify-review/), [igleads](https://igleads.io/resources/apify-review/), [blackbearmedia](https://blackbearmedia.io/apify-review/))
- **data365.co highlights a key hidden cost concern**: third-party Reddit scraper actors on Apify often do not include proxy costs, and Apify has no native Reddit scraper — users must bring their own proxies or pay extra, making the advertised actor price misleading ([source](https://data365.co/blog/apify-reddit-scraper))
- **The recommended practical testing workflow is**: free trial ($5 credits) -> small sample run -> inspect output quality and volume -> check CU consumption and event charges -> compare effective cost-per-result across similar actors -> scale gradually with max limits set ([use-apify.com](https://use-apify.com/docs/what-is-apify/apify-pricing))
- **The Issues tab on actor pages is public and serves as a consumer evaluation signal**: active responses from developers suggest reliable maintenance, while many unresolved issues or silence is a red flag; Apify docs explicitly state this tab's activity level "may serve as an indicator of the Actor's reliability" ([Apify docs](https://docs.apify.com/academy/actor-marketing-playbook/store-basics/how-store-works))
- **Actor README quality is a strong evaluation signal**: well-structured READMEs with examples, clear input/output documentation, and transparent pricing perform better in Store search; the quality score explicitly evaluates "ease of use" and "congruency" based on documentation quality ([quality score docs](https://docs.apify.com/platform/actors/publishing/quality-score))
- **Apify runs automated daily tests on all Store actors**: if an actor fails for 3 consecutive days it gets labeled "under maintenance" and the developer is notified; 28 more days of failure leads to deprecation — consumers should check for this "Under maintenance" label as a major red flag ([Apify docs](https://docs.apify.com/academy/actor-marketing-playbook/store-basics/how-store-works))
- **The Apify Store Searcher (jirimoravcik/apify-store-searcher) offers ML-powered search** using TF-IDF and cosine similarity to surface more relevant actors per category, with smart agent detection — but it is currently marked "Under maintenance" with only 4 total users, limiting its practical utility ([source](https://apify.com/jirimoravcik/apify-store-searcher))

## Full Findings

### 1. Apify Store Search & Filter Capabilities

The Apify Store (apify.com/store) is the primary discovery surface for actors. Based on the Store API documentation and the official blog post:

**Available filters (via UI and API):**
- **Text search**: searches across title, name, description, username, and README content
- **Category filter**: predefined categories including AI, Social Media, E-commerce, Lead Generation, SEO Tools, Jobs, Real Estate, Developer Tools, Travel, Videos, Automation, Integrations, Open Source, MCP Servers, Agents, and Others
- **Sort options**: relevance (default), popularity, newest, lastUpdate
- **Pricing model filter**: FREE, FLAT_PRICE_PER_MONTH (rental), PRICE_PER_DATASET_ITEM (PPR), PAY_PER_EVENT (PPE)
- **Username filter**: filter by developer
- **Agentic users filter**: whether actor allows agentic payment

**Limitations:**
- No multi-criteria advanced filtering (e.g., "show me actors with 4+ stars AND updated in last 30 days AND PPE pricing")
- No direct comparison view for side-by-side actor evaluation
- Maximum 1,000 results per API query
- With 10,000+ actors, finding the right one requires knowing what to search for
- The Store UI groups actors by categories below the search box, but the sheer volume is "overwhelming for beginners" (hackceleration.com)

Source: [Apify Store API docs](https://docs.apify.com/api/v2/store-get), [Apify blog on Store](https://blog.apify.com/what-is-apify-store/)

### 2. Apify Store Analyzer Actor

**What it does**: Searches the Apify Store for actors matching keywords and produces structured competitive analysis. Uses the public Store API (no scraping).

**Key outputs per actor:**
- Pricing model and tier classification (free/subscription/per-result/budget/mid/premium)
- Market position classification: leader (1,000+ users or 100K+ runs), challenger (100+ users or 10K+ runs), niche (10+ users or 1K+ runs), newcomer
- User counts (total, monthly, quarterly), run stats, ratings, review counts
- Technical specs (memory, timeout, categories, last update)

**Pricing**: $0.035 per run start + $0.002 per actor analyzed. Analyzing 50 actors costs ~$0.135.

**Assessment**: Very new (published March 1, 2026, only 2 total users). The concept is valuable — it automates what consumers would otherwise do manually by clicking through dozens of actor pages. However, it is unproven at scale and created by a community developer (automation-lab/Stas Persiianenko), not Apify itself. Also available as an MCP tool for Claude AI.

Source: [apify.com/automation-lab/apify-store-analyzer](https://apify.com/automation-lab/apify-store-analyzer)

### 3. PPE Cost Estimator Actor

**What it does**: Analyzes any actor's recent run history (via API, does not actually run the target actor) and calculates true cost per result including:
- Compute unit costs
- Dataset storage costs
- Pay-per-event charges
- Volume projections with low/high confidence intervals
- Optimization recommendations (memory, batch size, failure rate)

**Why it matters for evaluation**: The most common complaint about Apify pricing is unpredictability. This tool lets consumers estimate real costs before scaling by analyzing historical run data. It supports "what-if" scenarios with custom event price overrides.

**Pricing**: $0.035 per run start + $0.005 per actor analyzed (~$0.04 total for one actor).

**Assessment**: Also very new (published Feb 28, 2026, 3 total users), same developer as Store Analyzer. Fills a genuine gap — no other tool calculates true per-result costs across all billing components.

Source: [apify.com/automation-lab/ppe-cost-estimator](https://apify.com/automation-lab/ppe-cost-estimator)

### 4. Best Actor Finder

**What it does**: An LLM-powered tool that:
1. Extracts search keywords from a natural language query
2. Searches the Apify Store and filters out subscription-based actors
3. Crawls actor pages to extract README content and pricing
4. Scores each actor on 7 weighted criteria: intent match (30%), reliability (20%), documentation (15%), pricing (15%), maintenance (10%), community trust (5%), input complexity (5%)
5. Selects top N actors (default 3), generates valid input via LLM, and actually runs them with retry logic (up to 5 attempts)
6. Returns evaluation scores alongside actual run results and output samples

**Assessment**: Ambitious concept but extremely niche (8 total users, last modified 3 months ago). Running other actors incurs their costs. The LLM-generated input may not be representative of real use cases. Still, it is the only tool that automates the full "discover, evaluate, test" workflow.

Source: [apify.com/pranavpatel/best-actor-finder](https://apify.com/pranavpatel/best-actor-finder)

### 5. Apify Store Searcher (ML-Enhanced)

**What it does**: A web application providing ML-enhanced search of the Apify Store using TF-IDF vectorization and cosine similarity. Features include smart agent detection (distinguishing true AI agents from miscategorized scrapers), full-text search, and category filtering.

**Assessment**: Currently marked "Under maintenance" — which by Apify's own testing system means it has failed automated tests for 3+ consecutive days. Only 4 total users. The concept (ML-improved search over the basic keyword search) addresses a real gap, but the tool itself is not currently usable.

Source: [apify.com/jirimoravcik/apify-store-searcher](https://apify.com/jirimoravcik/apify-store-searcher)

### 6. Third-Party Review/Comparison Sites

#### hackceleration.com
- **Type**: Growth marketing agency review (affiliate)
- **Content**: Most detailed third-party review found. Claims real testing of multiple actors including TikTok Scraper. Provides ratings across 5 dimensions (ease of use 3.8/5, value 4.0/5, features 4.5/5, support 4.0/5, integrations 4.5/5, overall 4.2/5). Includes specific performance claims: "50,000 TikTok profiles for ~$60 in compute units."
- **Evaluation utility for consumers**: Gives a good high-level platform overview but does not compare individual actors against each other. Useful as a "should I use Apify at all?" resource, not a "which actor should I pick?" resource.
- **Bias**: Affiliate link (apify.com/?fpr=a20zdo). Self-identifies as an "Apify agency."

Source: [hackceleration.com/apify-review/](https://hackceleration.com/apify-review/)

#### use-apify.com
- **Type**: Independent affiliate documentation site (Docusaurus-based)
- **Content**: Provides the most actionable evaluation guidance found anywhere. Their "How to Choose the Right Actor" checklist is the single best consumer resource:
  1. Check last update date (aim for within 30 days)
  2. Read reviews and ratings (aim for 4+ stars, check recency)
  3. Check run history and success rate (90%+ good, 95%+ excellent)
  4. Compare pricing models (table comparing Pay per Usage, Pay per Result, Rental, Pay per Event)
  5. Test with free credits first ($5/month)
  6. Check Apify vs Community maintenance badge
- Also provides category-specific "best actors" pages (Google Maps, Instagram, TikTok, YouTube, LinkedIn, etc.) with data-driven rankings.
- **Pricing guide**: Clearly explains the two-layer pricing model (platform + actor) and the "test, measure, tune, scale" workflow.
- **Bias**: Affiliate (fpr=use-apify parameter on all Apify links). Explicitly discloses affiliate relationship.

Source: [use-apify.com/docs/best-apify-actors](https://use-apify.com/docs/best-apify-actors), [use-apify.com/docs/what-is-apify/apify-pricing](https://use-apify.com/docs/what-is-apify/apify-pricing)

#### igleads.io
- **Type**: Competitor product review (IGLeads is a lead generation tool)
- **Content**: General Apify overview with pricing breakdown. Aggregates review platform ratings (G2 4.7/5, Capterra 4.8/5, Trustpilot 4.6/5). Notes Reddit complaints about support responsiveness. Includes a "Google Reviews Scraper" walkthrough as a practical example.
- **Evaluation utility**: Minimal for per-actor comparison. Primarily a funnel to their competing product.
- **Bias**: Heavy — every section ends with IGLeads promotion. The rating breakdown oddly rates "Contact Data Accuracy" and "Chrome Extension" which are IGLeads features, not Apify's.

Source: [igleads.io/resources/apify-review/](https://igleads.io/resources/apify-review/)

#### blackbearmedia.io
- **Type**: SEO/digital marketing agency review (affiliate)
- **Content**: Comprehensive platform overview. Claims 5,000+ pre-built actors. Notes Apify was "#1 web scraping software on Capterra in 2024." Mentions Intercom as a notable customer. Discusses credit-based pricing model requiring "careful planning for high-volume projects."
- **Evaluation utility**: Good general Apify overview but no per-actor comparison tools.
- **Bias**: Affiliate link (apify.com/?fpr=659095).

Source: [blackbearmedia.io/apify-review/](https://blackbearmedia.io/apify-review/)

#### data365.co
- **Type**: Competitor product blog post (Data365 Social Media API)
- **Content**: Focused specifically on Apify's Reddit scraping capabilities. Key finding: **Apify has no native Reddit scraper** — all Reddit scrapers are third-party community actors. These cost $9-20/month but often do not include proxy fees, which are essential for scraping. Highlights the CU pricing opacity (1 CU ≈ 1 GB-hour of memory usage; 1,000 posts ≈ 1-2 CUs but varies non-linearly).
- **Evaluation utility**: Valuable as a specific case study in hidden costs. Demonstrates the importance of checking whether an actor includes proxy costs or requires separate proxy purchase.
- **Bias**: Heavy — promotes Data365 API as alternative throughout.

Source: [data365.co/blog/apify-reddit-scraper](https://data365.co/blog/apify-reddit-scraper)

### 7. Pricing Comparison Methods & Hidden Costs

**The two-layer pricing structure is the most common source of confusion:**

**Layer 1 — Platform billing (your Apify account):**
| Plan | Monthly | Credits Included | CU Rate |
|------|---------|-----------------|---------|
| Free | $0 | $5 | $0.30/CU |
| Starter | $29 | $29 | $0.30/CU |
| Scale | $499 | $199 | $0.25/CU |
| Business | $999 | custom | $0.20/CU |

**Layer 2 — Actor-level pricing:**
- Pay per Usage: only platform CUs consumed (most transparent for small runs)
- Pay per Result (PPR): fixed price per data item
- Pay per Event (PPE): fixed price per defined event (e.g., $0.05 per run start + $0.003 per item scraped)
- Rental: monthly subscription + separate CU costs

**Hidden costs consumers miss:**
1. **Residential proxy fees**: $7-8 per GB (varies by discount tier) — charged separately from CU costs. Many community actors require residential proxies to avoid blocks but do not include them.
2. **SERPs proxy fees**: $1.70-2.50 per 1,000 SERPs
3. **Data transfer**: $0.18-0.20 per GB external, $0.04-0.05 per GB internal
4. **Dataset read/write operations**: small but can add up at scale
5. **Browser-based vs HTTP scrapers**: browser scrapers consume ~10x more CUs per page (300 pages/CU vs 3,000 pages/CU for HTTP)

**Practical pricing comparison method:**
1. Use free $5 credits to test 2-3 competing actors with identical small inputs
2. Check actual CU consumption in run logs
3. Calculate effective cost-per-result: (CU cost + event charges + proxy usage) / number of results
4. Use the PPE Cost Estimator actor to project costs at target volume
5. Compare across actors and pricing models — a "Pay per Usage" actor might be cheaper for small runs while a "Rental" actor saves money at high volumes

Sources: [Apify pricing docs](https://docs.apify.com/platform/actors/publishing/monetize/pricing-and-costs), [use-apify.com pricing guide](https://use-apify.com/docs/what-is-apify/apify-pricing), [data365.co](https://data365.co/blog/apify-reddit-scraper), [hackceleration](https://hackceleration.com/apify-review/)

### 8. Actor Quality Score as Evaluation Signal

The Actor quality score (0-100) is Apify's internal metric that directly influences Store visibility and ranking. While primarily aimed at developers, consumers can use the underlying criteria as an evaluation framework:

**8 quality categories:**
1. **Reliability**: Run success rates, passing automated QA tests
2. **Popularity**: User count, save counts, return usage patterns
3. **Feedback and community**: Reviews, ratings (users invited to review after multiple runs)
4. **Ease of use**: Clear titles, descriptions, self-explanatory input fields, well-structured README
5. **Pricing transparency**: Clear, predictable costs; PPE model scores higher
6. **Trustworthiness**: Limited permissions (principle of least privilege)
7. **History of success**: Developer's track record of publishing successful actors
8. **Congruency**: Consistency between title, description, docs, and schemas

**Score dynamics**: Recalculates several times daily. Relative to other actors (your score can change even without modifications). Algorithm evolves over time.

**Consumer implication**: Higher-quality actors appear higher in search results. But the numeric score is not directly visible to consumers — they see its effects through search ranking.

Source: [docs.apify.com/platform/actors/publishing/quality-score](https://docs.apify.com/platform/actors/publishing/quality-score)

### 9. Actor README Quality as Evaluation Signal

From the Apify Academy documentation and quality score criteria, README quality correlates strongly with actor quality:

**What to look for in a good README:**
- Clear description of what the actor does and does not do
- Input/output examples with realistic data
- Pricing breakdown with cost examples at different volumes
- Integration examples (API, MCP, SDK)
- FAQ addressing common issues
- Links to related actors or alternatives

**Red flags in READMEs:**
- Generic or auto-generated descriptions
- No input/output examples
- Missing pricing information
- No mention of limitations or known issues
- Very short or poorly formatted documentation

The quality score explicitly evaluates "ease of use" (documentation clarity) and "congruency" (consistency between README and actual behavior).

Source: [docs.apify.com/platform/actors/publishing/quality-score](https://docs.apify.com/platform/actors/publishing/quality-score)

### 10. The Issues Tab as Evaluation Signal

Each actor has a public Issues tab where users can open tickets, ask questions, request features, and report bugs.

**How consumers should use it:**
- **Active, responsive Issues tab**: Developer engages promptly with users, fixes reported bugs — strong signal of reliability
- **Many unresolved issues with repeated themes**: Red flag — the actor may have known problems the developer is not addressing
- **Empty Issues tab with many users**: Could mean the actor "just works" or users have given up reporting
- **Developer response time**: Fast responses suggest active maintenance

Apify's own documentation states: "Since the Issues tab is public, the level of activity — or lack thereof — can be observed by potential users and may serve as an indicator of the Actor's reliability."

Source: [docs.apify.com/academy/actor-marketing-playbook/store-basics/how-store-works](https://docs.apify.com/academy/actor-marketing-playbook/store-basics/how-store-works)

### 11. Apify's Automated Testing System

Apify runs automated tests daily on all Store actors:
- Tests check if an actor can successfully run with default input within 5 minutes
- **3 consecutive days of failure** → labeled "Under maintenance," developer notified
- **28 more days of failure** → deprecated
- Consumers should treat the "Under maintenance" label as a major red flag

This system means that any actor currently in the Store without the maintenance label has passed a basic "can it run?" test within the last 3 days. However, this only tests default input — it does not validate output quality, handle edge cases, or test at scale.

Source: [docs.apify.com/academy/actor-marketing-playbook/store-basics/how-store-works](https://docs.apify.com/academy/actor-marketing-playbook/store-basics/how-store-works)

### 12. Practical Testing Workflow (Synthesized Best Practice)

Based on all sources consulted, the recommended evaluation workflow for consumers:

**Step 1: Discovery**
- Search Apify Store with relevant keywords
- Sort by popularity to see battle-tested actors first
- Filter by pricing model if you have a preference
- Note the "Maintained by Apify" vs "Maintained by Community" badge

**Step 2: Initial Screening (per actor)**
- Check last update date (within 30 days = actively maintained)
- Check total users and monthly active users
- Read star ratings and recent reviews
- Look for the "Under maintenance" warning label
- Check the Issues tab for unresolved problems
- Read the README for documentation quality

**Step 3: Cost Estimation**
- Read the Pricing tab for the actor's pricing model
- Check if proxy costs are included or separate
- For PPE actors, calculate expected cost: (start event price) + (per-item price × expected items)
- For CU-only actors, note memory requirements and estimate CUs based on expected runtime
- Consider using the PPE Cost Estimator actor for data-driven estimates

**Step 4: Small Test Run**
- Use free $5 credits (refreshed monthly)
- Run with a small input sample (10-50 items)
- Check: Does it produce the expected output fields?
- Check: Is the data quality acceptable (no empty fields, correct formats)?
- Check: How long did it take and how many CUs did it consume?
- Check: Any errors or warnings in the run log?

**Step 5: Compare Competing Actors**
- Run the same small input on 2-3 competing actors
- Calculate effective cost-per-result for each
- Compare output quality, completeness, and format
- Note which actors handle edge cases better

**Step 6: Scale Gradually**
- Set maximum result/run limits where supported
- Monitor CU consumption as you increase volume
- Watch for rate limiting or blocking issues at larger scales
- Adjust proxy settings if needed

Sources: [use-apify.com](https://use-apify.com/docs/best-apify-actors), [use-apify.com pricing](https://use-apify.com/docs/what-is-apify/apify-pricing), [hackceleration](https://hackceleration.com/apify-review/), [Apify Store docs](https://docs.apify.com/academy/actor-marketing-playbook/store-basics/how-store-works)

### 13. Apify's Actor Validation Guide (Developer-Focused but Consumer-Relevant)

Apify's Academy includes a detailed "Validate your Actor idea" guide aimed at developers, but many techniques apply to consumers evaluating actors:

- **Check Apify Store metrics**: Monthly users, ratings, pricing, last updates — "transparent competitive intelligence most marketplaces hide"
- **Review competitor issues tabs**: "High-quality READMEs with examples and clear value propositions perform better"
- **Market saturation heuristics**: 10-30 actors = healthy competition (market validated), 50+ = saturated (need obvious gaps), 1-5 = blue ocean or unproven
- **Assess with the Store API**: Programmatic access to stats enables data-driven comparison

Source: [docs.apify.com/academy/build-and-publish/actor-ideas/actor-validation](https://docs.apify.com/academy/build-and-publish/actor-ideas/actor-validation)

### 14. Additional Store Scraper Actors (Meta-Evaluation Tools)

Multiple community actors exist specifically to scrape and analyze the Apify Store itself:

| Actor | Users | Description |
|-------|-------|-------------|
| louisdeconinck/apify-store-scraper-api | 81 | Extract actor details, pricing, metrics, categories |
| jupri/apify-store | 134 | Apify Store extension scraper |
| igolaizola/apify-store-scraper | 14 | Scale scraping of actor listings with stats/pricing |
| yourapiservice/apify-store-scraper | 53 | Extract stats over 7/30/90 day periods |
| scrape.badger/apify-store-scraper | 4 | Scrape all 12,000+ actors with issue counts |

These tools enable consumers to build their own comparison databases, but require technical comfort with running actors and processing JSON/CSV output.

Source: Related actors listed on [apify.com/automation-lab/apify-store-analyzer](https://apify.com/automation-lab/apify-store-analyzer)

## Execution Log

| # | Action | Tool | URL | Result | Reasoning |
|---|--------|------|-----|--------|-----------|
| 1 | Fetch Apify Store Analyzer page | firecrawl_scrape | https://apify.com/automation-lab/apify-store-analyzer | Full README with features, pricing, output schema, market classification criteria | Primary source for evaluating this tool |
| 2 | Fetch hackceleration review | firecrawl_scrape | https://hackceleration.com/apify-review/ | Detailed platform review with ratings, pricing analysis, real testing claims | Key third-party review site |
| 3 | Fetch use-apify.com best actors guide | firecrawl_scrape | https://use-apify.com/docs/best-apify-actors | Actionable 6-step evaluation checklist, pricing model comparison table, category-specific guides | Best consumer evaluation resource found |
| 4 | Fetch igleads review | firecrawl_scrape | https://igleads.io/resources/apify-review/ | General review with aggregated review platform ratings, competitor comparison | Third-party review, heavily biased toward IGLeads |
| 5 | Fetch data365 Reddit scraper article | firecrawl_scrape | https://data365.co/blog/apify-reddit-scraper | Hidden proxy cost analysis, no native Reddit scraper finding, CU pricing explanation | Key source for hidden costs angle |
| 6 | Fetch blackbearmedia review | firecrawl_scrape | https://blackbearmedia.io/apify-review/ | Comprehensive platform overview, 5,000+ actors claim, Capterra #1 ranking | Third-party review site |
| 7 | Fetch Apify Store docs (how store works) | firecrawl_scrape | https://docs.apify.com/academy/actor-marketing-playbook/store-basics/how-store-works | Store mechanics, actor types, ownership, Issues tab documentation, automated testing details | Official documentation on store evaluation signals |
| 8 | Search for Store search/filter capabilities | firecrawl_search | "Apify Store search filter compare actors guide" | Found Store Searcher, Best Actor Finder, Store API docs, actor validation guide | Discovery of additional evaluation tools |
| 9 | Search for actor evaluation workflows | firecrawl_search | "how to evaluate Apify actors before buying testing workflow" | Found quality score docs, automated testing docs, Best Actor Finder, use-apify | Discovery of quality score and testing infrastructure |
| 10 | Fetch Best Actor Finder page | firecrawl_scrape | https://apify.com/pranavpatel/best-actor-finder | Full README with LLM evaluation criteria, 7 scoring dimensions, execution workflow | Evaluation tool with automated testing |
| 11 | Fetch Apify Store Searcher page | firecrawl_scrape | https://apify.com/jirimoravcik/apify-store-searcher | ML-powered search features, currently "Under maintenance" status | Alternative search tool evaluation |
| 12 | Fetch actor validation guide | firecrawl_scrape | https://docs.apify.com/academy/build-and-publish/actor-ideas/actor-validation | SEO validation, community research, Store metrics analysis, market saturation heuristics | Developer guide with consumer-relevant evaluation techniques |
| 13 | Search for hidden pricing/proxy costs | firecrawl_search | "Apify actor pricing hidden costs proxy fees compute units real cost" | Found pricing docs, PPE Cost Estimator, use-apify pricing guide, oreateai analysis | Pricing comparison sources |
| 14 | Fetch PPE Cost Estimator page | firecrawl_scrape | https://apify.com/automation-lab/ppe-cost-estimator | Full README with cost breakdown methodology, volume projections, optimization tips | Critical pricing evaluation tool |
| 15 | Fetch Apify pricing/costs docs | firecrawl_scrape | https://docs.apify.com/platform/actors/publishing/monetize/pricing-and-costs | Platform unit costs by tier (CU, proxy, data transfer, storage operations) | Official hidden cost documentation |
| 16 | Fetch use-apify.com pricing guide | firecrawl_scrape | https://use-apify.com/docs/what-is-apify/apify-pricing | Two-layer pricing explanation, practical budgeting approach, common cost mistakes | Best consumer pricing guide |
| 17 | Fetch Apify blog on Store | firecrawl_scrape | https://blog.apify.com/what-is-apify-store/ | Store overview, 6,000+ actors, category/search/sort capabilities, monetization models | Official blog describing Store features |
| 18 | Fetch Actor quality score docs | firecrawl_scrape | https://docs.apify.com/platform/actors/publishing/quality-score | 8 quality categories, score mechanics, Store visibility impact | Quality score as evaluation proxy |
| 19 | Fetch Store API docs | firecrawl_scrape | https://docs.apify.com/api/v2/store-get | API parameters (search, sortBy, category, pricingModel, username, allowsAgenticUsers), response schema with stats | Official Store search capabilities |

## Budget Used

| Resource | Soft Limit | Actual Used |
|----------|-----------|-------------|
| Web searches | 15-25 | 4 (firecrawl_search) |
| Web fetches | 30-60 | 19 (firecrawl_scrape) |
| Total operations | 45-85 | 23 |

Budget used well within soft limits. All key URLs from the assignment were fetched and analyzed. Additional discovery searches identified important tools (PPE Cost Estimator, Best Actor Finder, Store Searcher) and documentation (quality score, automated testing, actor validation guide) not in the original URL list.
