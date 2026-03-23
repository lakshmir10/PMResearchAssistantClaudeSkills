# PM Research Assistant — Claude Skill

A 9-pass strategic analysis system that runs entirely inside Claude.
Give it a product and a strategic question, get back a consulting-grade PDF with charts.

No API keys. No setup. No external tools.

## Install (30 seconds)

1. Go to **Claude.ai → Settings → Claude Skills** (or wherever custom skills are managed)
2. Upload `pm-research-assistant-skill.tar.gz`
3. That's it

If installing manually:
```
Extract to: /mnt/skills/user/pm-research-assistant/
```

## Use It

Just ask Claude something like:

> "Analyze Notion's strategy for competing with Microsoft Loop and Google Docs in enterprise"

> "Run a strategic analysis on Stripe's opportunity in B2B lending"

> "Help me build a business case for Razorpay entering the payroll market"

Claude will automatically:
- Run 9 analytical passes (market sizing, competitive intel, strategic fit, business model, customer experience, red team, validation, synthesis)
- Search the web for live data at each pass
- Track every claim as VERIFIED FACT / REASONED ESTIMATE / EXPLICIT ASSUMPTION
- Generate a PDF with pricing charts, evidence quality donut, strategic scorecard, and a structured appendix
- Hand you the downloadable PDF

## What You Get

A 5-7 page PDF containing:

- **Page 1**: Cover + verdict badge + pricing comparison chart + evidence quality chart
- **Page 2**: Strategic options scorecard chart
- **Pages 3-4**: Synthesized deliverable (executive summary, recommendation, market context, business model with unit economics ranges, customer experience, failure modes, 90-day action plan, decision gates)
- **Pages 5-6**: Appendix (agent contribution grid, full evidence audit table, pipeline metadata)

## What Makes This Different

**It's not a chatbot wrapper.** It's a structured analytical pipeline where each pass has a unique output schema — the Market Scanner outputs sizing tables, the Competitive Intel outputs positioning maps, the Business Designer outputs unit economics with downside/base/upside ranges. A Red Team pass actively argues against the recommendation. A Validator pass issues a formal verdict. The Assembler deduplicates and synthesizes everything into one coherent narrative.

**Every number is tracked.** The evidence registry labels every claim with its type, source, date, and confidence. Contradictions between passes are surfaced automatically. Old data is flagged as stale.

## Example Output

See `sample_skill_output.pdf` in this package for what the Zoho Mail enterprise strategy analysis looks like.

## Limitations

- Quality depends on Claude's model tier (Opus > Sonnet > Haiku)
- Web search results are as good as what's publicly available
- Unit economics are always directional estimates, never forecasts
- The 9-pass analysis takes 2-5 minutes depending on model speed
- Works best for strategic product questions, not operational or technical ones
