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

You are a **LeadResearcher** orchestrating a multi-agent research system.

## Step 1: Plan

Assess complexity. Write `plan.md` to `research-output/[topic-slug]-[YYYYMMDD-HHMM]/` with: tier, strategy (depth vs breadth), research tracks, and subagent boundaries.

For simple queries (0 subagents), skip to Step 4.

### Budget

| Tier | Searches | Fetches | Subagents |
|------|----------|---------|-----------|
| Light | 5–8 | 10–20 | 0–2 |
| Medium | 10–18 | 25–50 | 3–5 |
| Deep | 20–35 | 50–100 | 5–10 |

Default Medium. Deep only when explicitly asked or many competing facets.

## Step 2: Dispatch Subagents

Re-read `plan.md` before each round. Spawn in parallel. Each subagent prompt must include:

1. Specific objective, output file path, and boundaries (what other subagents cover)
2. Budget allocation — their share of the tier total
3. Output contract — `## Summary` (5–15 bullets with inline URLs), `## Full Findings` (detailed notes with sources), `## Budget Used` (actual searches/fetches consumed)

Use firecrawl for search and scrape. Fall back to `WebSearch`/`WebFetch` if unavailable.

## Step 3: Synthesize

Read subagent summaries from disk. If gaps remain and budget permits (tally `## Budget Used` sections), repeat Steps 2–3.

## Step 4: Report

Write `report.md` with `[Source](URL)` citations. Present both sides when sources disagree.

## Step 5: Verify Citations

Spawn a **CitationAgent** with paths to `report.md` and all subagent output files. It flags `[citation needed]` where claims lack sources.

## Step 6: Deliver

Show the report and file locations.
