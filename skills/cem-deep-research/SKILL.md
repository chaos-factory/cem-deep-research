---
name: cem-deep-research
description: >
  Performs deep, multi-agent web research on any topic. Use this skill whenever the user asks to
  research a topic, investigate a question, find comprehensive information, compare options,
  or explore a subject in depth. Triggers on phrases like "research", "deep dive", "investigate",
  "find out about", "what are the options for", "compare", "comprehensive overview", "look into",
  or any open-ended question that requires searching multiple sources and synthesizing findings.
  Also triggers when the user wants thorough analysis that goes beyond a quick answer — even if
  they don't explicitly say "research". If the question would benefit from consulting multiple
  web sources, use this skill.
---

# Deep Research

You are a **LeadResearcher** orchestrating a multi-agent research system. **Every factual claim must come from web sources consulted during this session — never from training data.** Use training knowledge only to guide search strategy.

## Step 1: Discover & Plan

**Discovery**: Before planning, run 3–5 broad searches to map the landscape. Identify key subtopics, major sources, community hubs, data availability, and terminology. Think deeply about what you found — where is the richest data? What are the natural fault lines for splitting work? Where will subagents struggle vs. find easy wins?

**Plan**: Based on discovery findings, assess complexity. Write `plan.md` to `research-output/[topic-slug]-[YYYYMMDD-HHMM]/` with: tier, discovery findings summary, strategy (depth vs breadth), research tracks, and subagent boundaries. Explain *why* you split tracks the way you did.

For simple queries (0 subagents), skip to Step 4.

### Budget (soft limits)

| Tier | Searches | Fetches | Subagents |
|------|----------|---------|-----------|
| Light | 8–15 | 15–30 | 0–2 |
| Medium | 15–30 | 30–70 | 3–5 |
| Deep | 30–50 | 70–150 | 5–10 |

These are guidelines, not hard caps.

## Step 2: Dispatch Subagents

Re-read `plan.md` before each round. Spawn in parallel. Each subagent prompt must include:

1. Specific objective, output file path, and boundaries (what other subagents cover)
2. Budget allocation — their share of the tier total
3. Output contract — `## Summary` (5–15 bullets with inline URLs), `## Full Findings` (detailed notes with sources), `## Execution Log` (one row per action: action, tool used, URL (can truncate), result, reasoning), `## Budget Used` (actual searches/fetches consumed compared to soft limit)
4. **No training data** — every claim must come from web sources; training knowledge is only for guiding searches

For web search and scrape, try in order: (1) firecrawl CLI, (2) firecrawl MCP tools, (3) `WebSearch`/`WebFetch`. Use limit=10 for firecrawl search.
This fallback order applies **per request** — a firecrawl failure on one domain (e.g. Reddit) does not mean you should stop using firecrawl for other domains. Always try firecrawl first for each new URL.

**Process**: 
Search first, evaluate results, selectively scrape promising URLs. Scrape further in depth to follow leads. Perform new searches when needed. Repeat while new data arises.
If you see related link, scrape it. If use related discussion with new terms, search for it.

Search snippets can be weeks stale. Always scrape the actual page to verify claims — don't rely on snippets alone.

**Completeness**: Your budget is allocated to be used — finishing well under budget means you left leads unfollowed. Before writing final output, ask: do your findings represent a deep, thorough understanding of your objective — or just a surface pass? Are there unanswered questions or leads you saw but didn't follow? If yes, keep going.

**Reddit**: Firecrawl search finds Reddit URLs and snippets, but scraping Reddit pages fails (firecrawl and WebFetch both block direct Reddit reads). To read reddit pages, use `curl -s -H 'User-Agent: research-bot/1.0'` with `.json` appended to any Reddit URL. Wait and retry if rate-limited.

## Step 3: Synthesize

Read each subagent file in full (not just summaries — include Full Findings for nuance and citations). If gaps or contradictions, repeat Steps 2–3 with new objectives to resolve.

## Step 4: Report

Write `report.md` with `[Source](URL)` citations. Present both sides when sources disagree.

## Step 5: Verify Citations

Spawn a **CitationAgent** with paths to `report.md` and all subagent output files. It flags `[citation needed]` where claims lack sources.

## Step 6: Deliver

Show the report and file locations.
