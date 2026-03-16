# Track 1: Apify's Official Evaluation Infrastructure for Consumers

## Summary

- **Actor Quality Score** (0-100): An automated scoring system launched Nov 2025 that evaluates actors across 8 categories -- Reliability, Popularity, Feedback & Community, Ease of Use, Pricing Transparency, Trustworthiness, History of Success, and Congruency -- and directly influences store ranking and discoverability. [Source](https://docs.apify.com/platform/actors/publishing/quality-score)
- **Store Page Metrics**: Each actor card/detail page displays star rating (e.g. 4.7), review count (e.g. 989), total users (e.g. 310K), monthly active users, total bookmarks/stars, response time to issues (e.g. 1.6 days), last modification date, and pricing model. [Source](https://apify.com/compass/crawler-google-places)
- **Rising Star Badge**: A curated collection highlighting "new Actors with strong early traction, positive reviews, or chosen by the Apify team" that "must meet functionality and discoverability standards." [Source](https://apify.com/store/collections/rising-star)
- **Automated Daily Testing**: Apify tests all store actors daily by running them with default input; actors that fail for 3 consecutive days are labeled "under maintenance," and after another 28 days are deprecated. [Source](https://docs.apify.com/platform/actors/publishing/test)
- **Issues Tab**: A public ticketing system on each actor's page (both web and Console) where consumers can see open/closed issues, developer response time, and the quality of support interactions before trying an actor. [Source](https://docs.apify.com/academy/actor-marketing-playbook/interact-with-users/issues-tab)
- **"Maintained by Apify" vs "Maintained by Community" Labels**: Clear ownership labels distinguish Apify-maintained actors (guaranteed maintenance, reliability testing) from community-maintained actors (developer-managed). [Source](https://help.apify.com/en/articles/6999799-what-are-apify-maintained-and-community-maintained-actors)
- **Permission Badges**: Actors display "Limited permissions" or "Full permissions" badges, letting consumers assess trustworthiness; limited-permission actors are more secure and score higher. [Source](https://docs.apify.com/platform/actors/development/permissions)
- **Free Trial / "Try for Free" Button**: All store actors have a "Try for free" button; rental actors have explicit trial periods; pay-per-event actors support max charge limits; pay-per-result actors allow max items limits. [Source](https://docs.apify.com/platform/actors/running/actors-in-store)
- **Store Sorting & Filtering**: The store API and UI support sorting by relevance (default, quality-score-weighted), popularity, newest, and lastUpdate; filtering by category, pricing model (FREE, PAY_PER_EVENT, etc.), developer type (Apify vs Community), and "allows agentic users." [Source](https://docs.apify.com/api/v2/store-get)
- **Actor Stars System**: Launched Nov 2024, users can star/bookmark actors to create personal lists; total stars are visible as a popularity signal. [Source](https://apify.com/change-log/actor-stars-and-standby-mode-are-here)
- **Store Collections**: Curated groupings like "Rising Stars," "$1M Challenge Picks," "Hidden Gems," "Popular from Community," and category-specific collections help consumers discover vetted actors. [Source](https://apify.com/store)
- **Actor Status Badge**: Embeddable SVG badge showing OK/Under Maintenance/Deprecated status, usable in GitHub READMEs or external docs. [Source](https://docs.apify.com/platform/actors/publishing/status-badge)
- **README as Landing Page**: Serves as the primary evaluation surface with structured sections (features, tutorial, pricing, input/output examples, FAQ); consumers rely on first 25% for evaluation decisions per heatmap data. [Source](https://docs.apify.com/academy/actor-marketing-playbook/actor-basics/how-to-create-an-actor-readme)
- **Dataset/Output Schema**: Actors can define structured output schemas with field descriptions, enabling consumers to preview exactly what data they will receive before running. [Source](https://docs.apify.com/platform/actors/development/actor-definition/dataset-schema)
- **Discount Tiers**: Bronze/Silver/Gold subscription tiers provide discounts on selected actors, shown on the actor pricing section. [Source](https://docs.apify.com/platform/actors/running/actors-in-store#apify-store-discounts)

## Full Findings

### 1. Actor Quality Score System

**Source**: https://docs.apify.com/platform/actors/publishing/quality-score

The Actor Quality Score is a 0-100 metric that aggregates multiple performance and quality dimensions. It recalculates several times per day and directly influences actor visibility and placement in Apify Store search results.

**Eight scoring categories:**

1. **Reliability** -- Measures operational stability: run success rates and automated QA test results. Implementing an input schema helps prevent runtime failures.
2. **Popularity** -- Reflects user engagement: number of users running the actor, save counts, return usage patterns.
3. **Feedback and Community** -- User reviews and ratings from users who have run the actor multiple times. Negative reviews hurt; prompt issue resolution helps.
4. **Ease of Use** -- How quickly users can understand and run the actor: clear titles, descriptions, self-explanatory input fields, well-structured README.
5. **Pricing Transparency** -- How clearly users can predict costs. Pay-per-event (PPE) model scores well. Offering Bronze/Silver/Gold discounts helps.
6. **Trustworthiness** -- Whether the actor uses limited permissions (principle of least privilege). Full permissions negatively impact score.
7. **History of Success** -- Developer track record of publishing successful actors.
8. **Congruency** -- Consistency across title, description, input schema, dataset schema, key-value store schema, and README. Reduces user confusion.

**Score fluctuations**: Scores are relative -- they shift as other actors improve/decline and as the algorithm evolves with new properties.

**How to view**: Console > Insights > Actor quality (developer-facing), but the resulting ranking is consumer-visible in store placement.

**Launch**: November 4, 2025 per changelog (https://apify.com/change-log/actor-quality-is-here). Introduced quality badges and the Rising Star badge alongside the scoring system.

### 2. Store Page Metrics Visible to Consumers

**Source**: https://apify.com/compass/crawler-google-places (scraped as JSON)

On each actor detail page, consumers can see:

| Metric | Example Value | Notes |
|--------|--------------|-------|
| Star Rating | 4.7 | Aggregate from user reviews |
| Review Count | 1,001 | Number of user reviews |
| Total Users | 310K | Cumulative unique users |
| Monthly Active Users | 19K | Recent engagement |
| Total Bookmarked/Stars | 3.5K | Saves by other users |
| Response Time | 1.6 days | Average issue response time |
| Last Modified | 2 days ago | Recency of updates |
| Pricing Model | Pay-as-you-go | Pricing type indicator |
| Pricing Details | from $2.10 / 1,000 places | Specific per-unit cost |
| Categories | Lead generation, Travel | Functional categorization |
| Maintained By | Apify or Community | Ownership label |
| Permission Level | Limited or Full | Trust signal |
| "Try for free" | Always present | Free trial CTA |

**In the store API** (https://docs.apify.com/api/v2/store-get), each actor returns:
- `stats.totalBuilds`, `stats.totalRuns`, `stats.totalUsers`, `stats.totalUsers7Days`, `stats.totalUsers30Days`, `stats.totalUsers90Days`, `stats.totalMetamorphs`, `stats.lastRunStartedAt`
- `categories` array (e.g. `["MARKETING", "LEAD_GENERATION"]`)
- `currentPricingInfo.pricingModel` (FREE, FLAT_PRICE_PER_MONTH, PRICE_PER_DATASET_ITEM, PAY_PER_EVENT)
- `isWhiteListedForAgenticPayment` (boolean -- indicates agentic AI compatibility)
- `readmeSummary` (LLM-generated readme summary)

### 3. Review and Rating System

**Source**: https://docs.apify.com/platform/actors/publishing/quality-score#feedback-and-community

- Users who have run an actor multiple times are invited to provide reviews and ratings.
- Star ratings are displayed on both the actor card in store listings and on the detail page.
- Ratings appear to use a 5-star scale (e.g. 4.7, 5.0, 3.5).
- Review count is prominently displayed alongside the star rating.
- Negative reviews impact the quality score; developers are encouraged to address issues promptly.

From the store homepage (https://apify.com/store), every actor card shows: user count, star rating, and review count in parentheses (e.g. "307K / 4.7 / (989)").

### 4. Free Trial Mechanics

**Source**: https://docs.apify.com/platform/actors/running/actors-in-store

Every actor has a **"Try for free"** button. The specifics depend on the pricing model:

- **Free actors**: No charge, only platform usage (compute units) applies.
- **Pay-per-event**: Users can set a maximum charge limit per run. The actor terminates gracefully at the limit, and overages are never charged.
- **Pay-per-result**: Users can limit the maximum number of results returned via "max items" setting. Some actors offer first N results free.
- **Rental actors** (sunsetting by Oct 2026): Most have explicit free trial periods (length shown on page). No paid plan needed to start the trial. After trial ends, monthly rental fee auto-deducts from prepaid usage.

New Apify accounts get $5 in free platform credits, which can be used to test actors.

### 5. Issues Tab

**Sources**:
- https://docs.apify.com/platform/actors/running/actors-in-store#report-issues-with-actors
- https://docs.apify.com/academy/actor-marketing-playbook/interact-with-users/issues-tab

The Issues tab is a public ticketing system present on every published actor's page, both on the web (apify.com) and in Apify Console.

**Consumer-facing features:**
- Three views: Open, Closed, All issues.
- Each issue has its own URL (SEO-indexed).
- Average **Response Time** metric is calculated and shown in actor metrics -- indicates how active and responsive the developer is.
- All visitors can see interactions (only signed-in users can post).
- Issues cannot be deleted, only closed -- provides transparent support history.
- When reporting, users are encouraged to share their run (shared privately).

**Evaluation value**: Consumers can browse issues before trying an actor to gauge reliability, common problems, developer responsiveness, and feature development trajectory.

### 6. "Maintained by" Labels

**Source**: https://help.apify.com/en/articles/6999799-what-are-apify-maintained-and-community-maintained-actors

Two labels appear in the upper-right corner of actor pages:

| Aspect | Maintained by Apify | Maintained by Community |
|--------|-------------------|------------------------|
| Ownership | Created by Apify team | Created by independent developers |
| Maintenance | Apify guarantees all updates, bug fixes | Developer handles everything; Apify only hosts |
| Reliability | Meticulous reliability testing to Apify standards | Tests recommended but not enforced |
| Support | Issues answered by Apify's Actor development team | Issues answered by community developer |
| Documentation | README + Help Center articles | README only |

**Consumer implication**: Apify-maintained actors carry an implicit quality guarantee; community actors require more independent evaluation.

### 7. Permission Badges (Trustworthiness Signal)

**Source**: https://docs.apify.com/platform/actors/development/permissions

Actors display a visible permission badge on their detail page:

- **Limited permissions (default for new actors)**: Restricted access to own storages and generated data. Cannot access other user data. Higher trust, higher quality score.
- **Full permissions**: Access to all user's Apify account data. Lower trust, lower quality score. Developers must explain why in README.

This is a direct consumer trust signal: limited-permission actors are safer to run, especially for security-conscious users.

### 8. Store Categories, Collections, and Filtering

**Source**: https://apify.com/store, https://apify.com/store/categories

**Categories visible in store navigation**: Social media, AI, Agents, Lead generation, E-commerce, SEO tools, and many more. The categories API filter supports values like `AI`, `MARKETING`, `LEAD_GENERATION`, `TRAVEL`, etc.

**Curated Collections** (visible on store homepage):
- **Rising Stars**: "New Actors with strong early traction, positive reviews, or chosen by the Apify team. Must meet functionality and discoverability standards."
- **$1M Challenge Picks**: Actors selected by Apify for their developer challenge.
- **Hidden Gems - Social Media**: Low-profile, high-impact tools.
- **Popular Actors from the Community**: High-engagement community-built actors.
- **E-commerce Tools**: Category-specific collection.
- **AI Agents**: Spotlight collection.

**Filtering options** (UI and API):
- By category
- By pricing model (Free, Pay-per-event, Pay-per-result, Rental)
- By developer type (All, Maintained by Apify, Maintained by Community)
- By agentic payment support

**Sorting options**: Relevance (default, quality-score-weighted), Popularity, Newest, Last Update.

**Scale**: The store currently lists 19,624 actors (as of March 2026).

### 9. Actor Stars (Bookmarking)

**Source**: https://apify.com/change-log/actor-stars-and-standby-mode-are-here

Launched November 18, 2024. Users can star any actor in Apify Console. Features:
- Creates personalized favorites list.
- Total star count is publicly visible as a popularity signal (e.g. "3.5K" for Google Maps Scraper).
- Users can filter to view only starred actors.
- Provides community insight: "See which Actors the community loves."

### 10. Actor Status Badge

**Source**: https://docs.apify.com/platform/actors/publishing/status-badge

A dynamic SVG badge that shows the current health status of an actor. Four states:
- **OK**: Actor passes automated tests.
- **Under maintenance**: Actor has failed automated tests for 3+ consecutive days.
- **Deprecated**: Actor has been broken for 28+ days after maintenance label.
- **Not found**: Actor does not exist.

The badge can be embedded in GitHub READMEs and external documentation via URL: `https://apify.com/actor-badge?actor=<USERNAME>/<ACTOR>`

Consumer value: Quick visual health check before using an actor, especially useful when discovering actors through GitHub or external docs.

### 11. Automated Testing System

**Source**: https://docs.apify.com/platform/actors/publishing/test

Apify runs automated tests on all store actors daily:
- Tests run the actor with its default input (from prefill in input schema).
- Expects completion with "Succeeded" status and non-empty default dataset within 5 minutes.
- **3 consecutive days of failure** = "under maintenance" label + developer notification.
- **14 more days of failure** = second notification.
- **Another 14 days** (28 total after initial label) = "deprecated."
- If an actor passes majority of test runs in next 7 days, automatically marked healthy.
- Actors requiring authentication or >5 min runs can be exempted via support request.

Developers can also use the public [Actor Testing](https://apify.com/pocesar/actor-testing) tool for custom tests.

### 12. README as Evaluation Surface

**Source**: https://docs.apify.com/academy/actor-marketing-playbook/actor-basics/how-to-create-an-actor-readme

The README serves four consumer-facing functions:
1. **SEO landing page** -- Google indexes README content.
2. **First impression** -- Determines whether a user tries the actor.
3. **Extended instructions** -- Complex input settings, formatting, special features.
4. **Support reference** -- Troubleshooting, known bugs, contact info.

Key signals consumers can extract from a README:
- What data the actor extracts (data table).
- Input complexity (screenshots of input schema).
- Output format (JSON examples, screenshots).
- Pricing estimation (cost per result explanations).
- Tutorials and videos (step-by-step guides).
- Legal disclaimers (data privacy, GDPR).
- Related actors from the same developer.
- FAQ and troubleshooting sections.

Per Apify's heatmap data, most first-time visitors don't scroll past the first 25% of the README.

The right-side table of contents is auto-generated from H2 headings, providing quick navigation.

### 13. Input Schema (Auto-Generated UI)

**Source**: https://docs.apify.com/platform/actors/development/actor-definition/input-schema

The input schema auto-generates a user interface for actor configuration. Consumers can:
- See all configurable parameters before running.
- Get inline descriptions and tooltips for each field.
- See prefilled default values that demonstrate expected usage.
- Have input validated before execution starts.

This reduces friction and lets consumers assess actor complexity before committing.

### 14. Dataset/Output Schema

**Source**: https://docs.apify.com/platform/actors/development/actor-definition/dataset-schema

Actors can define structured output schemas that:
- Show consumers exactly what data fields will be produced.
- Define field types, labels, and display formats.
- Render preview tables in the Output tab.
- Include field descriptions for AI agent interoperability.

Consumer value: Allows evaluation of whether the actor produces the specific data points needed before paying.

### 15. Actor Description and SEO Description

**Source**: https://docs.apify.com/academy/actor-marketing-playbook/actor-basics/actor-description

Each actor has two descriptions:
- **Regular description** (up to 300 chars): Visible on the store page, targets "warm" visitors.
- **SEO description** (145-155 chars): Visible in Google search results, targets "cold" discovery.

Plus corresponding names (Actor name vs SEO name, each 40-50 chars).

### 16. Pricing Transparency Signals

**Sources**: https://docs.apify.com/platform/actors/running/actors-in-store

Three pricing models (with rental being sunset):
- **Pay-per-event**: Specific events priced, shown on actor page. Max charge limit available.
- **Pay-per-result**: Price per result, max items limit available. Platform usage often included.
- **Rental** (sunsetting): Fixed monthly fee + platform usage. Trial periods available.
- **Free**: Only platform usage charges.

Discount tiers (Bronze, Silver, Gold) are shown in the pricing section for participating actors. Enterprise discounts also available.

Historical usage tracking in Console lets consumers see actual costs per actor.

### 17. Agentic Payment Whitelisting

**Source**: https://docs.apify.com/api/v2/store-get, https://blog.apify.com/agentic-payments-skyfire/

A newer signal: `isWhiteListedForAgenticPayment` flag in the API indicates whether an actor supports autonomous AI agent payments. The store API supports filtering by `allowsAgenticUsers`. This is relevant for consumers building AI agent workflows who need actors that can be called autonomously.

### 18. LLM-Generated README Summary

**Source**: https://docs.apify.com/api/v2/store-get

The store API returns a `readmeSummary` field described as "A brief, LLM-generated readme summary." This provides a quick, standardized summary for programmatic consumers (including AI agents) to evaluate actors without reading the full README.

## Execution Log

| # | Action | Tool | URL | Result | Reasoning |
|---|--------|------|-----|--------|-----------|
| 1 | Fetch quality score docs | firecrawl_scrape | https://docs.apify.com/platform/actors/publishing/quality-score | Full page: 8 scoring categories, 0-100 scale, relative scoring | Core topic |
| 2 | Fetch actors in store docs | firecrawl_scrape | https://docs.apify.com/platform/actors/running/actors-in-store | Pricing models, issues tab, discounts | Core pricing/evaluation info |
| 3 | Fetch how store works | firecrawl_scrape | https://docs.apify.com/academy/actor-marketing-playbook/store-basics/how-store-works | Actor types, ownership, metrics, testing | Academy overview |
| 4 | Fetch automated testing docs | firecrawl_scrape | https://docs.apify.com/platform/actors/publishing/test | Testing logic: 5min, 3-day failure, deprecation flow | Core testing system |
| 5 | Fetch issues tab docs | firecrawl_scrape | https://docs.apify.com/academy/actor-marketing-playbook/interact-with-users/issues-tab | Issues tab details: public, SEO, response time metric | Key evaluation feature |
| 6 | Fetch README guide | firecrawl_scrape | https://docs.apify.com/academy/actor-marketing-playbook/actor-basics/how-to-create-an-actor-readme | README as landing page, heatmap data, SEO role | Evaluation surface |
| 7 | Fetch publishing docs | firecrawl_scrape | https://docs.apify.com/platform/actors/publishing | Publish process, maintenance expectations | Context |
| 8 | Fetch input schema docs | firecrawl_scrape | https://docs.apify.com/platform/actors/development/actor-definition/input-schema | Auto-generated UI, validation | UX evaluation signal |
| 9 | Search for categories/badges | firecrawl_search | Apify Store actor categories badges labels filtering | Found status badge docs, categories page, store analyzer actors | Discovery |
| 10 | Search for reviews/ratings | firecrawl_search | Apify actor reviews ratings star system | Found Actor Quality changelog, Actor Stars changelog | Key features |
| 11 | Search for free trial info | firecrawl_search | Apify actor "free trial" store evaluation | Confirmed "Try for free" is standard across store | Trial mechanics |
| 12 | Fetch Actor Quality changelog | firecrawl_scrape | https://apify.com/change-log/actor-quality-is-here | Nov 4 2025 launch, Rising Star badge, improvement suggestions | Timeline and badges |
| 13 | Fetch Actor Stars changelog | firecrawl_scrape | https://apify.com/change-log/actor-stars-and-standby-mode-are-here | Nov 18 2024, starring feature, community insight | Bookmarking feature |
| 14 | Fetch status badge docs | firecrawl_scrape | https://docs.apify.com/platform/actors/publishing/status-badge | SVG badge, 4 states: OK/maintenance/deprecated/not found | External evaluation signal |
| 15 | Fetch store API docs | firecrawl_scrape | https://docs.apify.com/api/v2/store-get | Full API schema: stats, categories, pricing, agentic flag, readmeSummary | API-level evaluation data |
| 16 | Fetch Rising Star collection | firecrawl_scrape | https://apify.com/store/collections/rising-star | 20 actors listed, criteria: traction + reviews + Apify pick | Curated collection |
| 17 | Fetch store homepage | firecrawl_scrape | https://apify.com/store | 19K+ actors, collections, categories, metric display format | Store UI overview |
| 18 | Search for maintained-by labels | firecrawl_search | Apify actor maintained by badge | Found help center article, Smart Actor Scraper | Label system |
| 19 | Fetch permissions docs | firecrawl_scrape | https://docs.apify.com/platform/actors/development/permissions | Limited vs Full permissions, badge display, quality score impact | Trust signal |
| 20 | Fetch categories page | firecrawl_scrape | https://apify.com/store/categories | 19,624 actors, filtering UI (category, pricing, developer) | Filtering options |
| 21 | Fetch Apify vs Community help article | firecrawl_scrape | https://help.apify.com/en/articles/6999799-... | Detailed comparison table | Label details |
| 22 | Fetch Google Maps Scraper (JSON) | firecrawl_scrape | https://apify.com/compass/crawler-google-places | All visible metrics: 310K users, 4.7 stars, 1001 reviews, etc. | Real actor page data |
| 23 | Search for dataset schema | firecrawl_search | Apify actor dataset schema output schema | Found dataset schema docs, changelog | Output evaluation |
| 24 | Fetch dataset schema docs | firecrawl_scrape | https://docs.apify.com/platform/actors/development/actor-definition/dataset-schema | Output schema with field descriptions, views, AI agent support | Data quality signal |
| 25 | Fetch actor description docs | firecrawl_scrape | https://docs.apify.com/academy/actor-marketing-playbook/actor-basics/actor-description | Description vs SEO description, 300 vs 155 chars | Discovery signal |
| 26 | Search for agentic payments | firecrawl_search | Apify agentic actor whitelisted AI agents | Found blog post about Skyfire integration, whitelisting | New evaluation dimension |

## Budget Used

| Metric | Actual | Soft Limit |
|--------|--------|------------|
| Searches | 7 | 15-25 |
| Fetches/Scrapes | 21 | 30-60 |
| Total operations | 28 | 45-85 |

Budget well within limits. Coverage is comprehensive across all required topics.
