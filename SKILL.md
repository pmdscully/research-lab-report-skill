---
name: research-lab-report
description: Write, restructure, or export research reports in the lab-report structure - Introduction/problem, Materials & Method, Findings, Reflection & Recommendations, Source Materials/References - with the project's report style rules (no pronouns, point-first prose, paired statistics, traceable sources) and Markdown-to-PDF export via pandoc/XeLaTeX. Use this skill whenever the user asks to write, create, update, restructure, conclude, or version a report - experiment reports, trial reports, findings reports, analysis write-ups, "report V1-x", "write up the results", "conclude this into a report", "export the report as PDF" - even when the user does not say "lab report". Also use when the user asks to check or fix a report's structure or style.
---

# Research Lab Report

Reports written under this skill follow one fixed order of information, so a
reader always meets the problem before the method, the method before the
numbers, and the numbers before the conclusions. Section titles may vary;
the order may not.

## The structure

Idea/Problem/Rationale → How → Result → Reflect/Conclude → next direction.

```
# <Report Title> — v<major>-<minor>
**Date:** … · **Dataset/Context:** … · **Series:** …
---
## 1. Introduction
## 2. Materials and method
## 3. Findings
## 4. Reflection and recommendations
## 5. Source materials / references
```

A skeleton with placeholder text sits in `assets/report-template.md` — start
new reports from that file. Never place a findings summary, abstract of
results, or headline number before the introduction: results appearing
before the problem statement defeat the structure's purpose, which is that
every number lands on a reader who already knows the question and the
method behind the number.

### 1. Introduction

State the problem being addressed in the first sentence — not background,
not history. Then the rationale: why the problem matters now, what breaks
or stays unknown while the problem stands. When the report answers several
questions, enumerate them explicitly (**Q1**, **Q2**, …) and mirror that
enumeration in the Findings subsections, so every question visibly receives
an answer.

### 2. Materials and method

Materials first: datasets (with sizes, rates, spacings), source documents
(with the exact sections read), the pipeline or system under test (with the
configuration that makes results reproducible), and hardware. Then method
subsections in execution order, one per analysis or experiment. Equations
belong here, each followed by a worked numeric example from the real data —
a reader who can reproduce one number by hand trusts the rest. Figures that
explain a setup or model also belong here; figures that show outcomes
belong in Findings.

### 3. Findings

One subsection per question or experiment, in the order the Introduction
posed them. Give the result table or figure first, then the reading of the
result in prose. Comparisons between configurations use paired statistics
over matched runs wherever the runs pair (report the delta, n better out of
n pairs, and both t-test and Wilcoxon p-values); a pooled-mean difference
without a paired test is a claim the report cannot support, so either pair
the runs or flag the comparison as unpaired. Null and negative results
appear with the same prominence as positive ones — a measured null is a
finding.

### 4. Reflection and recommendations

Interpret before recommending: what the results contain and do not contain,
which prior conclusions survive, which claims are now conditioned, and the
honest limits (what the data cannot separate, what was assumed). Then
numbered, actionable recommendations, closing with the next direction — the
follow-on experiment, collection, or decision the findings point to.

### 5. Source materials / references

Scripts (repo paths), result directories or tags, log files, runtimes,
hardware, source documents with page numbers, and cited literature. Traceable
sources turn a report into evidence; a number no one can trace is an
anecdote. Use the heading "Source Materials / References" (never
"Provenance").

## Project layout

The project folder's top level holds the deliverable PDF and nothing else
the report build produced; the user's own source data stays wherever the
user put the data. Everything used to build the report goes in one sibling
subdirectory named `Source-<ReportBaseName>/`:

```
<project>/
  <user data, e.g. courseid.xlsx>      # left where the user keeps it
  <ReportBaseName>.pdf                 # the deliverable, alone at top level
  Source-<ReportBaseName>/
    <ReportBaseName>.md
    analysis/                          # analysis and build scripts
    <ReportBaseName>_figs/             # figures, merged data, stats JSON
```

Never write the Markdown source, scripts (`.py`, `.ps1`), figure folders,
intermediate HTML/CSV/JSON, or logs into the project root: a cluttered
root buries the deliverable and mixes build debris with the user's files.
Scripts read the user's data by paths relative to the Source folder
(`../courseid.xlsx`), so the layout survives a folder rename. Throwaway
exploration scripts and temporary renders go to the session scratchpad or
another temp folder, never into the project.

## Style rules

These rules exist because reports get skimmed: a reader should understand
any sentence, especially a paragraph's first sentence, without reading the
sentences around that sentence.

1. **No pronouns.** Never use "it", "its", "they", "them", "their", or any
   person pronoun ("I", "we", "our", "he", "she") in report prose — name
   the referent explicitly every time. A demonstrative must modify a noun
   ("this recipe", "that fold"), never stand alone as a subject ("This
   shows…" hides the referent exactly the way "it" does). Before
   delivering, verify:
   `grep -cinE '\b(it|its|they|them|their|theirs|we|us|our|ours|he|him|his|she|her|hers)\b' report.md`
   and `grep -cnE '\bI\b' report.md` must both return 0 (the second check is
   case-sensitive so the imaginary unit $i$ in math never false-positives).
2. **No leading phrases.** "The headline survives" begs "which headline?" —
   write the claim: "Cosine decoding with pretraining ranks highest…".
   State the point first; explain detail afterwards.
3. **Self-describing names.** Never label experiment branches, methods,
   groups, or conditions with bare letters or digits — no "A/B/C",
   "Method 1/2", "Group 3", "Condition B" — and never with the word
   "arm" at all ("evaluation arm", "Seen arm", "both arms"): "arm" is
   trial jargon that names nothing; write the thing instead ("the
   Unseen-Places methodology", "both methodologies", "the west-heading
   condition"). Name the activity or quantity the label stands for, so
   the name alone tells a reader what was measured or done: `invBhZ`
   (yaw-invariant feature set), `yawaug8` (learned yaw augmentation),
   "champion control". A label that needs a legend to decode loses the
   reader at every mention. Before delivering, verify:
   `grep -cinE '\barm(s)?\b' report.md` must return 0.
4. **Numbers carry units and origin.** Every measured value states units;
   every table says what produced the values. Distinguish measured from
   assumed from cited.
5. **Claims match evidence.** No "monotonically", "every", or
   "significant" unless the data shows exactly that; hedge cited values
   not re-verified ("reported", "at publication").
6. **Never the word "provenance".** Use a more common term for the same
   idea: "origin", "source", "where the values come from", "traceability".
7. **Never "exactly" or "precisely".** Both words signal that the
   surrounding text has been imprecise elsewhere — state the value, match,
   or condition plainly ("unchanged from v1-1", "the same constants",
   "byte-identical") and let the specificity carry the claim. Add to the
   pre-delivery checks:
   `grep -cinE '\b(provenance|exactly|precisely)\b' report.md` must return 0
   (rule 1's grepped example text is exempt; report prose is not).
8. **Every table and every figure carries a caption** — an italic line
   directly below, numbered in order of appearance ("*Table 2 — …*",
   "*Figure 1 — …*"), stating what the table or figure shows; table
   captions also say what produced the values (rule 4) and define any
   column whose meaning the header alone does not carry.
9. **Introduce every table and figure in prose first.** At least one
   sentence before the table or figure names the object ("Table 3 gives…",
   "Figure 2 extends…"), says what the object shows, and why the object is
   included at that point in the report. A table or figure must never
   follow a heading directly.
10. **Headings are professional, never conversational.** No rhetorical
   flourish, no narrative connectives doing argumentative work ("no
   baseline beats persistence at lag-matched horizons either" fails on
   the "either"), no suspense. Methods/materials headings name the object
   measured; findings headings follow rule 14. The same register applies
   to all text: technical and professional, reaching the point in the
   first words, with no conversational connectives ("either", "of
   course", "in fact").
11. **Headings use Title Case.** Every heading at every level ("Materials
   and Method", "Q2 — Baseline Comparison at 45-120 s Horizons"); minor
   words (articles, short prepositions, "vs") stay lowercase; unit and
   symbol spellings are kept as written ("s", "degC", "ppmCO").
12. **Model and experiment configuration go in an appendix.** When a
   report uses a model (fitted or pre-trained), the full modeling
   configuration (every hyperparameter and constant) and the experiment
   configuration (folds/splits, preprocessing, software versions, seeds
   or a statement of determinism, runtime) appear in a closing
   "Appendix A. Model and Experiment Configuration", as a captioned
   table plus prose, so the body stays readable and the run stays
   reproducible.
13. **Model choice is justified in Materials and Method.** When a report
   uses a model, the Materials and Method section states the model type,
   the reference/citation where applicable (paper or implementation), and
   the reason that model was selected over alternatives; pre-trained
   upstream models that produced input features are cited the same way,
   marked as used-as-released rather than fitted.
14. **Findings headings state the finding.** A findings subsection
   heading is a self-explanatory statement a reader can carry away
   without the body — condition(s) leading to outcome(s), "X Condition,
   Leads to Y Outcome" ("Sunny Days, Dry Clothes Better than Rainy
   Days"; "Adding Visual Features to Sensor History Yields No
   Significant Gain"). A topic-only findings heading ("Timestamp Audit
   of the Video-Sensor Join") hides the result; the statement form,
   in the professional register of rule 10 and the Title Case of
   rule 11, is required.

## Figures and tables

Reference every figure from the prose and caption every figure in italics
below the image, stating what the figure shows and the one thing to notice.
Number figures in order of appearance. Keep figure image files in
`Source-<ReportBaseName>/<ReportBaseName>_figs/`, beside the Markdown
source inside the Source folder (see Project layout), referenced by a path
relative to the `.md`, so the Markdown renders anywhere and the PDF export
finds the images. Wide tables: prefer one narrow table with many
rows over a doubled side-by-side layout — doubled layouts overflow the PDF
page. Long code identifiers in table cells (file names, run tags) do not
wrap in the PDF export and overflow into the neighbouring column: strip
any shared prefix out of the cells and state the prefix once in the
caption, keep each in-cell code span short, and give that column a wider
share of the pipe-table separator row (`|------|---|…`) — pandoc reads
relative column widths from the separator dashes.

## Math

Write display equations as `$$…$$` and inline math as `$…$` with LaTeX
commands (`\varphi`, `\sqrt`, `^\circ`) — pandoc renders both. Inside
fenced code blocks, use plain Unicode (√, °, µ) instead, because code
blocks bypass the math renderer.

## PDF export

Export with pandoc + XeLaTeX (fonts chosen for full µ/φ/Δ/‖ glyph
coverage), run from inside the Source folder so the relative figure paths
resolve, writing the PDF one level up to the project top level:

```bash
cd "Source-<ReportBaseName>"
pandoc <ReportBaseName>.md -o ../<ReportBaseName>.pdf --pdf-engine=xelatex \
  --resource-path=. \
  -V geometry:margin=2.2cm -V mainfont="Cambria" \
  -V monofont="Consolas" -V fontsize=10pt -V colorlinks=true
```

Intermediate render files (for example a `.print.html`) stay in the
Source folder or the scratchpad; only the PDF lands at the top level.

Then verify rather than assume: check the page count and spot-check that
key strings and symbols extracted from the PDF match the source (pypdf
`extract_text`), re-run the pronoun, arm and banned-word greps on the
final Markdown, and **render every page that carries a table or figure
(PyMuPDF `get_pixmap`) and look at the rendered pages** — cell text
overflowing into a neighbouring column, clipped captions and overlapping
legends survive every text-level check and only show in the pixels. On
machines without Cambria/Consolas, substitute any installed Unicode font
with equivalent coverage (for example DejaVu Serif / DejaVu Sans Mono).

## Versioning and updates

Reports carry a series version (`v1-0`, `V1-3`) in the filename and title.
Add findings into the current version until the user states a version
increment; a new version starts a new file, with a new
`Source-<ReportBaseName>/` folder named after the new version's base
name. When restructuring an existing report, move content into the
lab-report order without dropping any finding or number — restructuring
changes order, not substance.
