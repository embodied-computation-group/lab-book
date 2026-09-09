# 6. Verification

[← The loop](05-the-loop.md) · [Contents](../index.md) · [Next: Reproducibility →](07-reproducibility.md)

---

This is the page that matters. Reading agent-written code is not verification. The code
will look fine, because looking fine is what these models are best at.

Checklist version: [`starters/verification-checklist.md`](../starters/verification-checklist.md).

## 1. Test against a known answer

The strongest technique in scientific code, agent or not: **simulate data where you know
the truth, then check that the code recovers it.**

```python
def test_recovers_known_slope():
    # 500 trials from a psychometric function with known parameters
    true_threshold, true_slope = 2.5, 0.8
    data = simulate_psychometric(true_threshold, true_slope, n=500, seed=0)

    fit = fit_psychometric(data)

    assert abs(fit.threshold - true_threshold) < 0.3
    assert abs(fit.slope - true_slope) < 0.15
```

If an agent wrote `fit_psychometric`, this test is the only thing standing between you and
a wrong paper.

Ask for it in that order, explicitly: *write the simulator and the test first, with known
true parameters, then implement the fit.* It is a much better brief than "fit a
psychometric function", and the agent cannot tune the code to a test that already exists.

## 2. Make it fail on purpose

A test that has never failed is not evidence. Break things and check the test notices:

- flip a sign in the model
- shuffle the condition labels — accuracy should collapse to chance
- pass all-NaN input — it should raise, not return a number
- feed it one subject twice — does anything catch the duplicate?

If none of your checks fire, you do not have checks.

## 3. Assertions in the pipeline, not only in tests

Cheap, permanent, and they catch the failures that actually happen, which are data
failures rather than code failures:

```python
assert df.subject_id.nunique() == N_SUBJECTS
assert df.confidence.between(1, 100).all()
assert not df.duplicated(["subject_id", "trial"]).any()
assert df.rt.gt(0).all()
```

Every one of those corresponds to something that has gone wrong in somebody's real
analysis. Put them at the top of each processing step. An agent will write them if you ask
and will not if you do not.

## 4. Plot everything, early and cheaply

Look at the data at every stage: distributions per subject, raw traces, the fitted curve
over the actual points, residuals. This is how you catch the agent having misread your data
structure. A plot makes it obvious in a second, where the code and the numbers both looked
fine.

Generate a lot of these and throw them away. They are cheap now, so use them.

## 5. Cross-check independently

For anything going into a paper:

- **Re-implement the key number a second way.** Different library, different language, or
  by hand. Two independent routes to the same value is real evidence.
- **Do one subject entirely by hand.** Take subject 3, their raw trial file, and a
  calculator; compare to the pipeline output. Tedious, and it catches indexing bugs that
  survive everything else.
- **Ask a fresh session to find the bug** (page 5). Different framing, different blind
  spots.

## 6. Check the code against the methods section

Agents drift. The pipeline at submission is frequently not the pipeline you described.

```
Read manuscript/methods.md and scripts/run_analysis.py.
List every discrepancy: excluded subjects, model terms, priors,
transformations, filter settings. Do not summarise. List.
```

Before every submission, and again before every revision.

## What "done" means

A result is believable when:

- [ ] a test recovers known parameters from simulated data
- [ ] you have broken it deliberately and the checks fired
- [ ] assertions cover subject counts, ranges, duplicates, missingness
- [ ] you have looked at plots at every stage
- [ ] one key number is confirmed by a second, independent route
- [ ] the code matches the methods section line by line
- [ ] a fresh session reviewed it and you addressed what it found

Anything less, and the honest description of what you have is "the agent produced a
number".

---

[← The loop](05-the-loop.md) · [Contents](../index.md) · [Next: Reproducibility →](07-reproducibility.md)
