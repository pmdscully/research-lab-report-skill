# <Report Title, in Title Case> — v<major>-<minor>

**Date:** <YYYY-MM-DD> · **Dataset/Context:** <dataset or system under
study, one line> · **Series:** <what series this report belongs to and what
the series supports>

---

## 1. Introduction

<The problem being addressed, in the first sentence. Then the rationale:
why the problem matters now, what stays broken or unknown while the
problem stands. Concrete motivating scenario if one exists.>

<If the report answers several questions, enumerate:>

- **Q1 — <name>.** <The first question, one sentence.>
- **Q2 — <name>.** <The second question.>

## 2. Materials and Method

### 2.1 Materials

- **Dataset:** <name, size, sampling rate, spacing, cleaning>
- **Source documents:** <document, exact sections/pages read>
- **Pipeline under test:** <configuration complete enough to reproduce>
- **Hardware:** <machine, runtime>

<Introduce each materials table/figure in a sentence; a data-dictionary
table (column name, datatype, column type, unit, description) belongs here
when the report introduces a dataset.>

### 2.2 <Model / Theory, in Title Case>

<Equations with $$…$$, each followed by a worked numeric example from the
real data. Setup/model figures here. If a model is used: state the model
type, the reference/citation, and the reason the model was selected;
mark pre-trained upstream models as used-as-released. Full configuration
goes to Appendix A.>

### 2.3 <Analysis or Experiment Design, One Subsection Each, in Execution Order>

## 3. Findings

### 3.1 Q1 — <Self-Explanatory Statement of the Finding: X Condition, Leads to Y Outcome>

<First sentence restates the answer. Then a sentence introducing the
result table or figure, the table/figure itself, and a numbered italic
caption ("*Table 1 — …*"). Paired statistics for comparisons: delta,
n better / n pairs, p (t / Wilcoxon).>

### 3.2 Q2 — <Statement of the Second Finding>

## 4. Reflection and Recommendations

### 4.1 Reflection

<What the results contain and do not contain; which prior conclusions
survive; honest limits — what the data cannot separate, what was assumed.>

### 4.2 Recommendations and Next Direction

1. <Actionable recommendation.>
2. <…>
3. <Close with the next direction: the follow-on experiment, collection,
   or decision the findings point to.>

## 5. Source Materials / References

- <Scripts: repo paths, or `analysis/` paths inside the
  `Source-<ReportBaseName>/` folder.>
- <Results: directories or tags; logs; runtime; hardware.>
- <Source documents: with page numbers.>
- <Cited literature: numbered references or BibTeX keys.>

## Appendix A. Model and Experiment Configuration

<Required when a model was used. A captioned table of every
hyperparameter and constant, plus prose for the experiment configuration:
folds/splits, preprocessing, software versions, seeds or a statement of
determinism, runtime.>
