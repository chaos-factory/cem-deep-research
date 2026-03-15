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

**Discovery**: Run 3–5 broad searches to map the landscape. Identify subtopics, major sources, community hubs, data availability, and terminology. Think deeply — where is the richest data? What are the natural fault lines for splitting work?

**Plan**: Write `plan.md` to `research-output/[topic-slug]-[YYYYMMDD-HHMM]/` with: tier, discovery findings, strategy, research tracks, and subagent boundaries. Explain *why* you split tracks the way you did.

Skip to Step 4 for simple queries (0 subagents).

### Budget (soft limits)

| Tier | Searches | Fetches | Subagents |
|------|----------|---------|-----------|
| Light | 16–30 | 30–60 | 0–4 |
| Medium | 30–60 | 60–140 | 3–10 |
| Deep | 60–100 | 140–300 | 5–20 |


## Step 2: Dispatch Subagents

Re-read `plan.md` before each round. Spawn in parallel. Each subagent prompt must include:

1. Specific objective, output file path, and boundaries (what other subagents cover)
2. Budget allocation — their share of the tier total
3. Output contract — `## Summary` (5–15 bullets with inline URLs), `## Full Findings` (detailed notes with sources), `## Execution Log` (one row per action: action, tool used, URL (can truncate), result, reasoning), `## Budget Used` (actual vs soft limit)
4. **No training data** — every claim must cite a web source

For web operations, try in order: firecrawl CLI, firecrawl MCP, `WebSearch`/`WebFetch`. Use limit=10 for firecrawl search. A firecrawl failure on one request doesn't mean stop using it — retry firecrawl first on each new request.

**Process**:
Search first, then scrape every promising URL. Follow all related links. Search for all new terms or entities found in discussions. Repeat while new data arises.

Snippets can be stale — always scrape the actual page to verify claims.

**Stress-test findings**: Don't just gather — verify. Seek independent signals: user reviews, forum discussions, complaint patterns, recent news. Surface-level descriptions often hide problems only visible in real-world feedback.

**Completeness**: Before finishing, ask: do your findings represent deep, thorough coverage of your objective? Did you follow all leads? If not, keep going.

**Reddit**: Firecrawl search finds Reddit URLs but scraping Reddit pages fails. To read reddit pages, use `curl -s -H 'User-Agent: research-bot/1.0'` with `.json` appended to the URL. Wait and retry if rate-limited.

## Step 3: Synthesize

Read each subagent file in full. If gaps or contradictions remain, repeat Steps 2–3 with new objectives.

## Step 4: Report

Write `report.md` with `[Source](URL)` citations. Present both sides when sources disagree.

## Step 5: Verify Citations

Spawn a **CitationAgent** with paths to `report.md` and all subagent output files. It flags `[citation needed]` where claims lack sources.

## Step 6: Deliver

Show the report and file locations.
