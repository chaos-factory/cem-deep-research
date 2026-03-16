# Research Plan: Evaluating & Picking Apify Actors as a Consumer

## Tier: Medium (60–120 searches, 120–280 fetches, 3–5 subagents)

## Discovery Findings

1. **Apify has an official "Actor quality score"** system with reliability, ease of use, popularity, and other indicators — documented at docs.apify.com. This is a relatively new feature (discussed in Creator Cantina Q&A Nov 2024).

2. **Store metrics are visible** — monthly runs, star ratings, reviews, user counts, reliability scores shown on each Actor's store page.

3. **Free trial system exists** — paid/rental actors offer free trials. Some users abuse trials (creating multiple accounts). You don't need a paid plan to start a trial.

4. **Reliability is a genuine pain point** — Multiple Reddit posts about actors breaking, returning empty data, schemas changing. Someone literally built an "actor reliability and drift monitor" because this is so common. Another post: "Apify actor keeps breaking my n8n lead gen workflow."

5. **People do ask "which actor?"** — Reddit threads like "which Apify actor is most useful?", "which actor do you use?", "shop around for the best actor" in r/automation. The problem of choosing is real but there's no comprehensive consumer guide.

6. **Store Analyzer actor exists** — `apify.com/automation-lab/apify-store-analyzer` compares pricing, user counts, run stats, ratings across actors.

7. **Community review efforts** — Someone built a place to review actors they use. Reddit community votes for favorites. But no centralized, independent review ecosystem.

8. **External review signals** — Trustpilot reviews of apify.com exist but are platform-level, not per-actor. Hackceleration did a "1500+ actors" analysis.

9. **Most documentation is developer-focused** — Docs about quality scores, testing, validation are aimed at actor *builders*, not consumers. Consumer evaluation is an underserved topic.

## Strategy

The research question has two dimensions:
- **"Do people have this problem?"** — Is choosing the right actor a recognized pain point?
- **"How do you solve it?"** — What tools, signals, and workflows exist for evaluation?

## Research Tracks

### Track 1: Official Evaluation Infrastructure (Subagent A)
**What Apify provides consumers.** Quality score system (how it works, what factors, how visible), store metrics, free trial mechanics, the Issues tab, README quality signals, Actor categories/labels. Scrape the actual docs pages.

**Why this track:** Understanding the platform's built-in evaluation tools is foundational — consumers need to know what signals are available before they can use them.

**Budget:** 15–25 searches, 30–60 fetches

### Track 2: Community Pain Points & Real-World Experience (Subagent B)
**Do people actually struggle with picking actors?** Scrape Reddit threads (r/apify, r/n8n, r/automation, r/nocode, r/SaaS), Apify community/Discord via answeroverflow.com, Trustpilot. Look for: complaints about broken actors, "which actor" questions, reliability frustrations, stories of picking the wrong one, wasted credits.

**Why this track:** This directly answers "do people have such problem at all?" — it needs deep community signal gathering, which is distinct from the official docs research.

**Budget:** 15–25 searches, 30–60 fetches

### Track 3: Practical Evaluation Methods & Comparison Tools (Subagent C)
**How to actually test and compare.** The Store Analyzer actor, third-party review sites (hackceleration, use-apify.com, igleads, blackbearmedia), practical testing workflows (free trial → small run → check output quality), pricing comparison methods, what experienced users actually do. Also: data365.co's article about proxy fees hidden in actor costs.

**Why this track:** This is the actionable "how-to" part — it needs to synthesize both official tools and community wisdom into practical evaluation methods. Separate from Track 1 (official docs) and Track 2 (pain points) because it focuses on solutions rather than infrastructure or problems.

**Budget:** 15–25 searches, 30–60 fetches
