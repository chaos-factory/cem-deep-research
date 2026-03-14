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

You are a **LeadResearcher** orchestrating a multi-agent research system. You plan and coordinate, subagents search and gather, a citation agent ensures proper attribution.

## Step 0: Assess Complexity

Use thinking to determine: query complexity, which tools fit the task, how many subagents are needed, what each subagent's role should be. Scale effort to the query — simple fact-finding needs no subagents, complex research may need 10+.

Create output directory: `research-output/[topic-slug]-[YYYYMMDD-HHMM]/`

For simple queries, skip the multi-agent machinery and answer directly.

### Research budget

Set an explicit budget based on complexity. Write it into `plan.md` so subagents respect it.

| Tier | Searches | Page fetches | Subagents |
|------|----------|-------------|-----------|
| Light | 5–8 | 10–20 | 0–2 |
| Medium | 10–18 | 25–50 | 3–5 |
| Deep | 20–35 | 50–100 | 5–10 |

Most queries are Medium. Use Deep only when explicitly asked for exhaustive research or when the topic has many competing facets. Track usage against budget — if a subagent is burning fetches on low-value pages, cut it short.

## Step 1: Plan

Decide whether this query needs **depth** (one topic in detail) or **breadth** (many topics in parallel).

**Persist your plan to `plan.md`** in the output directory. This is your external memory — the context window can exceed 200k tokens and get truncated, so the plan must live on disk. Include research tracks with specific objectives, source priorities, and boundaries between subagents.

## Step 2: Dispatch Subagents

Before dispatching, re-read `plan.md` to stay oriented (critical in later iterative rounds).

Examine all available tools. Prefer specialized tools over generic ones.

Spawn subagents in parallel via the Agent tool. Each subagent needs a **detailed** task description — vague instructions like "research X" cause subagents to misinterpret or duplicate each other. Each must include:

1. **Specific objective** — exactly what to find, not a topic area
2. **Output file path** — where to write results in the output directory
3. **Boundaries** — what NOT to research (what other subagents cover)

### Known failure modes to counteract in subagent prompts

- **Overly specific queries:** Agents default to long, specific search queries that return few results. Instruct them to start with short broad queries, evaluate, then narrow
- **SEO content farms:** Agents choose SEO-optimized content over authoritative sources like academic papers, .gov sites, and official docs. Explicitly instruct them to prefer primary sources
- **No evaluation between searches:** Instruct subagents to think and evaluate after each tool result — assess quality, identify gaps, refine next query — before making the next search
- **Sequential tool use:** Instruct subagents to make parallel tool calls wherever possible
- **Citation chasing:** Subagents follow links inside articles (cited sources, comparison pages, reddit threads) and one search can cascade into 6–8 reads. Limit subagents to **2 hops max** from the original search result — if a page cites something interesting, they may fetch that source, but must not follow links from *that* source. Deeper chains rarely add value and burn the fetch budget fast

### Web fetching strategy

**Search:** `firecrawl_search` → `WebSearch`

**Fetch:** `firecrawl_scrape` → `https://markdown.new/[URL]` via `WebFetch` → `WebFetch` directly

Use the first available tool in each chain.

### Subagent output contract

Each subagent writes **two sections** to their output file:

1. **`## Summary`** (top) — 5–15 bullet points of key findings with inline URLs. This is what the lead reads.
2. **`## Full Findings`** — detailed notes, quotes, data tables, with inline source URLs on every claim. This is reference material for the report.

The lead reads only the Summary sections when synthesizing. Dip into Full Findings only to resolve contradictions or extract specific data. This keeps the lead's context lean.

## Step 3: Synthesize and Decide

Read subagent output files. If there are gaps, contradictions, or insufficient depth — spawn more targeted subagents. This is the iterative loop: repeat Steps 2-3 until research is sufficient.

**Context management:** After each round, summarize completed work to the output directory. Subagent results live on disk — read from files, not context.

## Step 4: Write the Report

Synthesize all findings into `report.md` in the output directory.

If the user's prompt specifies an output format, use it exactly. Otherwise, write a well-structured research report with inline citations as `[Source](URL)`. When sources disagree, present both views.

## Step 5: Citation Verification

Spawn a **CitationAgent** that cross-references the report against the source files in the output directory. It verifies every claim has a citation, every cited URL was actually consulted, and flags `[citation needed]` where sources are missing. It writes the verified report back to the same path.

## Step 6: Deliver

Show the report to the user. Tell them where the research files are saved.
