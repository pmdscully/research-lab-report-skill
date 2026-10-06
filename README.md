# research-lab-report

An agent skill for writing, restructuring and exporting research lab
reports with a fixed, skimmable structure and enforceable style rules.

## What the skill provides

- **One fixed section order:** Introduction (problem first) → Materials
  and Method → Findings → Reflection and Recommendations → Source
  Materials / References, with an optional configuration appendix.
  Results never appear before the problem statement and the method.
- **Fourteen style rules**, each with a rationale and, where possible, a
  mechanical check (grep commands that must return zero): no pronouns, no
  leading phrases, self-describing names, units and origin on every
  number, claims matched to evidence, banned filler words, numbered
  captions and prose introductions for every table and figure,
  Title Case headings, findings headings written as self-explanatory
  condition-outcome statements, model citations and selection reasons in
  Materials and Method, and full model/experiment configuration in an
  appendix.
- **A report template** (`assets/report-template.md`) to start new
  reports from.
- **A PDF export recipe** (pandoc + XeLaTeX with full glyph coverage)
  and a verification step (page count, extracted-text spot checks,
  re-run of the style greps).
- **Versioning conventions** for report series (`v1-0`, `v1-1`, …).

## Installation

Copy this folder into the agent's skills directory, for example:

```
~/.claude/skills/research-lab-report/
```

The skill activates when a report is requested — experiment reports,
trial reports, findings write-ups, "report V1-x", "conclude this into a
report", "export the report as PDF" — and applies the structure and
style rules above.

## Files

| Path | Purpose |
|---|---|
| `SKILL.md` | the skill: structure, style rules, figure/table rules, math, PDF export, versioning |
| `assets/report-template.md` | skeleton for a new report |
