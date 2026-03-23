---
name: pm-research-assistant
description: >
  Run a multi-pass strategic product analysis that produces a consulting-grade PDF with charts.
  Use this skill whenever the user asks to: analyze a product strategy, run a competitive analysis,
  evaluate a market opportunity, create a strategy memo, build a business case, produce a PM case study,
  compare strategic options, or do any form of structured product research. Also trigger on phrases like
  "research assistant", "strategic analysis", "8-agent pipeline", "consulting report", "market deep dive",
  or "help me think through [product/company] strategy." This skill uses Claude's own web search for
  live data and produces a PDF deliverable with charts — zero API keys, zero setup, zero external tools.
---

# PM Research Assistant — Claude Skill

A 9-pass strategic analysis system where Claude acts as 9 specialist agents sequentially,
using its own web search for live data and producing a PDF with charts. No external APIs,
no setup, no configuration.

## How It Works

Claude executes 9 analytical passes on the user's strategic question, each with a
distinct role and unique output schema. Each pass builds on the previous ones.
After all passes, Claude generates a synthesized PDF deliverable with charts using
the `scripts/generate_pdf.py` script.

## Workflow

When triggered, follow these steps exactly:

### Step 1: Clarify the Input

Get two things from the user:
- **Product/Company**: What we're analyzing
- **Strategic Question**: What decision needs to be made

If the user gave both already, proceed. If vague, ask ONE clarifying question.

### Step 2: Run the 9-Pass Analysis

Execute each pass sequentially. For each pass, use `web_search` to get live data
where indicated. Keep a running **Evidence Registry** — a mental ledger of every
claim, its type, and confidence.

**Claim types** (use these labels consistently):
- `VERIFIED FACT` — Confirmed from a current, authoritative source
- `REASONED ESTIMATE` — Derived from data with stated methodology
- `EXPLICIT ASSUMPTION` — Stated without evidence, must be validated

**Important**: Always include source date when citing data. Label anything older
than 12 months as STALE. Prefer sources from the current year.

Read `references/agent_passes.md` for the detailed instructions for each of the 9 passes.

### Step 3: Synthesize the Deliverable

After all 9 passes, produce the final output. The output has two parts:

**Part A — Conversational summary** (in chat):
Show the Executive Summary, Verdict, and top 3 action items directly in chat.

**Part B — PDF deliverable** (as downloadable file):
Run `scripts/generate_pdf.py` to produce the PDF. This script takes a JSON file
as input. Write the analysis results as JSON, then execute the script.

See `references/pdf_instructions.md` for the exact JSON format and PDF generation steps.

### Step 4: Present Results

Use `present_files` to give the user their PDF. Keep the conversational summary
brief — the PDF is the deliverable.

## Evidence Registry Format

Throughout the analysis, maintain this structure mentally:

```
EVIDENCE REGISTRY:
- [VERIFIED FACT] Claim X = Value (Source, Date) — High confidence
- [REASONED ESTIMATE] Claim Y = Value (Derived from Z) — Medium confidence
- [EXPLICIT ASSUMPTION] Claim Z = Value (Unverified) — Low confidence

CONTRADICTIONS: (list any)
KNOWN UNKNOWNS: (list gaps)
```

Surface contradictions when they appear. Never silently upgrade an assumption to a fact.

## What Makes This Different from a Normal Analysis

1. **Structured passes prevent echo chamber** — each pass has a unique schema
2. **Red Team pass** actively argues against the recommendation
3. **Validator pass** issues a formal verdict (PROCEED / REVISE / DO NOT PROCEED)
4. **Evidence tracking** — every number is labeled with type and confidence
5. **Charts in PDF** — pricing comparisons, evidence quality, strategic scorecard
6. **Live data** — web search with current-year queries

## When NOT to Use This

- Simple factual questions ("what does Company X do?")
- Requests for a single framework application ("do a SWOT on X")
- Non-strategic product questions ("how to use feature Y")

For these, just answer directly without running the full pipeline.
