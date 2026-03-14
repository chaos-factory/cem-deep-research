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

### Web fetching strategy

Fetch pages via `https://markdown.new/[URL]` — it handles sites that block direct requests and returns clean markdown. Fall back to `WebFetch` if markdown.new is unavailable.

### Subagent output contract

Subagents write findings to their output file with **inline source URLs on every claim**. They return only a brief summary to the lead — full results live on disk, not in context.

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
