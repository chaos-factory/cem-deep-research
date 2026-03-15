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

## Step 1: Plan

Assess complexity. Write `plan.md` to `research-output/[topic-slug]-[YYYYMMDD-HHMM]/` with: tier, strategy (depth vs breadth), research tracks, and subagent boundaries.

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
3. Output contract — `## Summary` (5–15 bullets with inline URLs), `## Full Findings` (detailed notes with sources), `## Execution Log` (numbered steps: action, target, result, reasoning), `## Budget Used` (actual searches/fetches consumed compared to soft limit)
4. **No training data** — every claim must come from web sources; training knowledge is only for guiding searches

For web search and scrape, try in order: (1) firecrawl CLI, (2) firecrawl MCP tools, (3) `WebSearch`/`WebFetch`.
This fallback order applies **per request** — a firecrawl failure on one domain (e.g. Reddit) does not mean you should stop using firecrawl for other domains. Always try firecrawl first for each new URL.
Search first, evaluate results, then selectively scrape promising URLs. Repeat to follow leads.

Search snippets can be weeks stale. Always scrape the actual page to verify claims — don't rely on snippets alone.

**Reddit**: Firecrawl and WebFetch are domain-blocked. Use `curl -s -H 'User-Agent: research-bot/1.0'` with `.json` appended to any Reddit URL. Parse with python3.

## Step 3: Synthesize

Read subagent summaries from disk. If gaps or contradictions, repeat Steps 2–3 with new objectives to resolve.

## Step 4: Report

Write `report.md` with `[Source](URL)` citations. Present both sides when sources disagree.

## Step 5: Verify Citations

Spawn a **CitationAgent** with paths to `report.md` and all subagent output files. It flags `[citation needed]` where claims lack sources.

## Step 6: Deliver

Show the report and file locations.
