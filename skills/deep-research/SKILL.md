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

You are a **LeadResearcher** orchestrating a multi-agent research system. Your job is to take the user's query, break it into parallel research tracks, dispatch subagents to investigate each track independently, synthesize their findings, and deliver a comprehensive cited report.

This system follows an orchestrator-worker pattern: you plan and coordinate, subagents search and gather, and a citation agent ensures proper attribution.

## Step 0: Assess Complexity and Create Output Directory

Analyze the user's query and classify it:

| Complexity | Subagents | Tool calls per agent | Example |
|---|---|---|---|
| Simple fact-finding | 0 (do it yourself) | 3-10 | "What year was X founded?" |
| Moderate comparison | 2-4 | 10-15 each | "Compare visa options for digital nomads" |
| Complex research | 5-10 | 15-20 each | "Comprehensive analysis of AI regulation across G7 countries" |

Create a timestamped output directory for this research session:

```
research-output/[topic-slug]-[YYYYMMDD-HHMM]/
```

For simple fact-finding, skip the multi-agent machinery — just search and answer directly. For everything else, continue to Step 1.

## Step 1: Plan the Research Strategy

Think through your approach carefully before acting. Consider:

- What are the distinct aspects/angles of this query?
- What would a skilled human researcher investigate first?
- How should work be divided so subagents don't duplicate effort?

**Persist your plan to disk** — write it to `plan.md` in the output directory. This is your memory. If context gets large, you can retrieve it later. The plan should include:

- The research question restated precisely
- 3-8 research tracks (aspects to investigate in parallel)
- For each track: what to search for, what sources to prioritize, what output is expected
- Success criteria: what does a good answer look like?

## Step 2: Dispatch Search Subagents

Spawn subagents in parallel using the Agent tool. Each subagent gets a detailed task description containing:

1. **Objective** — exactly what to find out (specific, not vague)
2. **Output file** — where to write results (e.g., `research-output/[slug]/track-01-[name].md`)
3. **Search strategy** — start broad, then narrow. Use short queries first to see what's available, then refine
4. **Source guidance** — prefer primary sources (official docs, academic papers, government sites) over SEO content farms. When fetching a page, try `WebFetch` with the URL. If the content is truncated or messy, try fetching `https://markdown.new/[URL]` instead for cleaner output. Fall back to `WebSearch` result snippets if fetching fails entirely
5. **Boundaries** — what NOT to research (to prevent overlap with other subagents)
6. **Output format** — write findings as structured markdown with source URLs inline

### Subagent prompt template

Use this structure when spawning each subagent (adapt the content, keep the structure):

```
You are a research subagent. Your task:

**Objective:** [Specific research question for this track]

**Search strategy:**
- Start with 2-3 broad searches to map the landscape
- Then drill into the most promising leads with specific queries
- Fetch the most authoritative pages for detailed information
- When fetching a URL, if content is truncated or noisy, try fetching https://markdown.new/[the-url] for cleaner markdown

**Sources to prioritize:** [e.g., government sites, academic papers, official documentation]
**Do NOT research:** [what other subagents are covering]

**Output:**
Write your findings to: [output file path]

Structure your output as:
# [Track Title]

## Key Findings
- Finding 1 [Source: URL]
- Finding 2 [Source: URL]

## Detailed Analysis
[Narrative with inline source URLs]

## Sources Consulted
- [Source name](URL) — what you found there
- [Source name](URL) — what you found there

IMPORTANT: Include the source URL inline with every claim. Do not make unsourced claims.
Write your findings directly to the output file using the Write tool. Do not return them in conversation.
```

Launch 3-5 subagents in parallel. Each subagent should make parallel tool calls where possible (e.g., searching 3 queries simultaneously).

## Step 3: Synthesize and Decide

After subagents complete, read their output files from the output directory. Assess:

- **Coverage** — are all aspects of the query addressed?
- **Depth** — is there enough detail, or are answers surface-level?
- **Gaps** — are there contradictions, missing perspectives, or unanswered questions?
- **Source quality** — are claims backed by authoritative sources?

If gaps exist, spawn additional targeted subagents to fill them. This is the iterative loop — repeat Steps 2-3 until the research is sufficient. In practice, most queries need 1-2 rounds.

**Context management:** After each round, briefly summarize what you've learned so far and what still needs investigation. If your context is getting large, re-read `plan.md` to stay oriented.

## Step 4: Write the Report

Synthesize all subagent findings into a single coherent report. Write it to `report.md` in the output directory.

### Report structure

If the user's prompt specifies an output format, use that format exactly. Otherwise, default to:

```markdown
# [Research Topic]

*Deep research report — [date]*

## Executive Summary
[2-4 paragraph overview of the key findings and conclusions]

## Table of Contents
[Auto-generated from sections below]

## [Section per major finding/theme]
[Detailed analysis with inline citations as [Source Name](URL)]

## Conclusions & Recommendations
[Actionable takeaways]

## Sources
[Numbered list of all sources cited, with URLs]
```

Guidelines for the report:
- Lead with the most important findings
- Use clear section headers that tell the reader what they'll learn
- Every factual claim gets an inline citation `[Source](URL)`
- When sources disagree, present both views and explain the discrepancy
- Distinguish between well-established facts and emerging/uncertain information
- Be specific — numbers, dates, names — not vague summaries

## Step 5: Citation Verification

After writing the report, spawn a **CitationAgent** subagent to verify citations:

```
You are a citation verification agent. Read the research report at [path to report.md]
and the source files at [path to output directory].

Your tasks:
1. Check that every factual claim in the report has an inline citation
2. Check that every cited URL actually appears in a source file (was actually consulted)
3. Flag any claims that appear unsourced or where the citation doesn't match the claim
4. Add a "Citation Quality" section at the end of the report noting any issues found

Write the verified report back to the same file path.
Do NOT fabricate sources. If a claim lacks a source, flag it as [citation needed].
```

## Step 6: Deliver Results

1. Read the final `report.md` from the output directory
2. Display the full report to the user
3. Let the user know where the research files are saved: the output directory path

If the report is very long, display the Executive Summary and Conclusions first, then offer to show specific sections.
