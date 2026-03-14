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

Determine query complexity. Create output directory: `research-output/[topic-slug]-[YYYYMMDD-HHMM]/`

**Persist plan to `plan.md`** in the output directory. The plan must include:

- **Tier** — Light, Medium, or Deep (see budget table below)
- **Strategy** — depth (one topic in detail) or breadth (many facets in parallel), and how this affects subagent count and report structure
- Research tracks with objectives, source priorities, and boundaries between subagents

For simple fact-finding (0 subagents), skip to Step 4 — do the research yourself and write the report directly.

### Research budget

| Tier | Searches | Fetches | Subagents |
|------|----------|---------|-----------|
| Light | 5–8 | 10–20 | 0–2 |
| Medium | 10–18 | 25–50 | 3–5 |
| Deep | 20–35 | 50–100 | 5–10 |

Default to Medium. Use Deep only when explicitly asked or when the topic has many competing facets.

## Step 2: Dispatch Subagents

Re-read `plan.md` before each dispatch round. Spawn subagents in parallel. Each subagent prompt must include:

1. **Specific objective** — exactly what to find, not a topic area
2. **Output file path** — a file in the output directory
3. **Boundaries** — what NOT to research (what other subagents cover)
4. **Budget allocation** — their share of the tier's total searches/fetches
5. **Output contract** — write two sections: `## Summary` (5–15 bullets of key findings with inline URLs — this is what the lead reads) and `## Full Findings` (detailed notes, quotes, data with inline source URLs). End the file with `## Budget Used` — report actual searches and fetches consumed
6. **Rules** — start broad then narrow; evaluate after each search before the next; use parallel tool calls; **2 hops max** from original search results

### Web fetching strategy

Use firecrawl for search and scrape. Search first, evaluate results, then selectively scrape promising URLs. Fall back to `WebSearch`/`WebFetch` if firecrawl is unavailable.

## Step 3: Synthesize

Read subagent summaries from their output files (not from context). Dip into Full Findings only to resolve contradictions.

If gaps or contradictions remain and budget permits, spawn targeted follow-up subagents (repeat Steps 2–3). Tally spent budget from subagent `## Budget Used` sections before deciding.

## Step 4: Write Report

Synthesize into `report.md` in the output directory. Use the user's requested format if specified, otherwise a structured report with `[Source](URL)` citations. Present both views when sources disagree.

## Step 5: Citation Verification

Spawn a **CitationAgent** with: the path to `report.md` and all subagent output file paths. It verifies every claim has a citation and every cited URL appears in a source file. Flags `[citation needed]` where sources are missing.

## Step 6: Deliver

Show the report. Tell them where the files are saved.
