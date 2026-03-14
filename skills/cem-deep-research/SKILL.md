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

## Step 0: Assess Complexity

Determine query complexity, tools needed, number of subagents, and each subagent's role. Simple fact-finding needs no subagents; complex research may need 10+.

Create output directory: `research-output/[topic-slug]-[YYYYMMDD-HHMM]/`

### Research budget

Write the chosen tier into `plan.md` so subagents respect it.

| Tier | Searches | Fetches | Subagents |
|------|----------|---------|-----------|
| Light | 5–8 | 10–20 | 0–2 |
| Medium | 10–18 | 25–50 | 3–5 |
| Deep | 20–35 | 50–100 | 5–10 |

Default to Medium. Use Deep only when explicitly asked or when the topic has many competing facets. Cut subagents short if they're burning fetches on low-value pages.

## Step 1: Plan

Depth (one topic in detail) or breadth (many topics in parallel)?

**Persist plan to `plan.md`** — this is your external memory. Include research tracks with objectives, source priorities, and boundaries between subagents.

## Step 2: Dispatch Subagents

Re-read `plan.md` before each dispatch round. Spawn subagents in parallel. Each needs:

1. **Specific objective** — exactly what to find, not a topic area
2. **Output file path**
3. **Boundaries** — what NOT to research (what other subagents cover)

### Failure modes to counteract

- **Overly specific queries:** Start broad, evaluate, then narrow
- **SEO content farms:** Prefer primary sources — academic papers, .gov, official docs
- **No evaluation between searches:** Think after each result before the next search
- **Sequential tool use:** Parallel tool calls wherever possible
- **Citation chasing:** 6–8 reads can cascade from one search. **2 hops max** from original search result

### Web fetching strategy

**Search:** `firecrawl_search` → `WebSearch`
**Fetch:** `firecrawl_scrape` → `https://markdown.new/[URL]` via `WebFetch` → `WebFetch` directly

Use first available in each chain.

### Subagent output contract

Each subagent writes two sections to their output file:

1. **`## Summary`** — 5–15 bullets of key findings with inline URLs. This is what the lead reads.
2. **`## Full Findings`** — detailed notes, quotes, data with inline source URLs.

The lead reads only summaries. Dip into Full Findings only to resolve contradictions.

## Step 3: Synthesize

Read subagent summaries. If gaps or contradictions remain, spawn more targeted subagents (repeat Steps 2–3).

Subagent results live on disk — read from files, not context.

## Step 4: Write Report

Synthesize into `report.md`. Use the user's requested format if specified, otherwise a structured report with `[Source](URL)` citations. Present both views when sources disagree.

## Step 5: Citation Verification

Spawn a **CitationAgent** to cross-reference the report against source files. It verifies every claim has a citation and every URL was actually consulted. Flags `[citation needed]` where sources are missing.

## Step 6: Deliver

Show the report. Tell them where the files are saved.
