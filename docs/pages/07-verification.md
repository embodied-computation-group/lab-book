# 7. Verification

[← The loop](06-the-loop.md) · [Contents](../index.md) · [Next: Reproducibility →](08-reproducibility.md)

---

Verification asks whether the code performs the intended calculation. Scientific
validation also asks whether that calculation is appropriate for the question and data.
Readable code and passing tests help, but neither settles both questions.

Use the [verification checklist](../starters/verification-checklist.md) to record evidence.
Choose checks that match your analysis and explain items that do not apply.

## 1. Define expected behaviour before implementation

Write down inputs, outputs and failure cases. For a descriptive calculation, a small
example worked by hand may be enough to define a useful test. The
[first exercise](first-exercise.md) demonstrates this.

For a fitted model, simulate observations from known parameters and assess recovery.
The simulator and fitter must use the same documented parameter definitions, but should
not share code that could reproduce the same mistake in both.

A recovery study should cover plausible parameter values, sample sizes and multiple
random seeds. Set acceptable error based on scientific needs and simulation variability.
If you report intervals, examine their coverage as well as point estimates. A single
successful fit with one seed is a useful development check, not a validation study.

Test-first development makes the specification inspectable before the code is written.
It does not prevent the agent from changing a test or hardcoding an answer. Review both
the implementation and any changes to the tests.

## 2. Check whether your tests detect errors

Temporarily introduce a plausible error and check that a relevant test fails. Save the
working version first, then restore it and rerun the tests.

Examples include:

- reversing a contrast or changing a unit conversion;
- duplicating a participant/trial row;
- passing an empty input or an invalid missing-value code;
- replacing participant-level averaging with trial-level averaging.

For a classification or permutation analysis, shuffled labels can provide a null check.
Choose a shuffle that respects the study's dependence structure; a single shuffle need
not give exactly chance performance.

## 3. Validate inputs in the pipeline

Check counts, ranges, uniqueness, units and missingness at the relevant processing step.
Here is an illustrative example; the expected count and ranges must come from your study:

```python
if df.subject_id.nunique() != expected_n:
    raise ValueError("Unexpected participant count")
if not df.confidence.between(1, 100).all():
    raise ValueError("Confidence must be present and between 1 and 100")
if df.duplicated(["subject_id", "trial"]).any():
    raise ValueError("Duplicate participant/trial pair")
```

If missing values are permitted, implement and test that policy explicitly. Python
`assert` statements are useful during development, but can be disabled with optimisation;
use explicit errors for checks that must always run.

## 4. Inspect diagnostic plots

Look at distributions per participant, traces before and after processing, fitted curves
over observations, and residuals where appropriate. Decide what you expect before looking:
for example, a unit conversion should rescale values without changing the distribution's
shape.

Record unexpected patterns and investigate them. A plausible plot is not sufficient
evidence that every processing step is correct.

## 5. Cross-check a key result independently

Recalculate a tractable part by hand or compare with an established implementation.
Check that both routes use the same conventions. Two wrappers around the same faulty
function are not independent checks.

For a complex model, inspect a small case closely and seek review from someone familiar
with the method. A second agent session is useful additional review, but does not replace
that expertise.

## 6. Compare the code with the scientific claim

Before submission or revision, compare the implementation with the methods and, where
applicable, the preregistration:

```text
Compare manuscript/methods.md with the analysis code.
List discrepancies in exclusions, model terms, priors, transformations
and filter settings. Give file locations. Do not change either file.
```

Resolve discrepancies explicitly. Do not silently rewrite a preregistered method to
match an unplanned analysis. Label exploratory changes and explain their rationale.

## What to bring to supervision

Bring the result, the relevant checks and their outputs, and any remaining uncertainty.
Be ready to explain one known-answer test, one error it detects and one error it would
miss. This is more informative than reporting how many tests passed.

---

[← The loop](06-the-loop.md) · [Contents](../index.md) · [Next: Reproducibility →](08-reproducibility.md)
