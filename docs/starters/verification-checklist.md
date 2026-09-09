# Verification checklist

Run through this before you believe a result, and definitely before it goes in a
manuscript. Full reasoning on [page 6](../pages/06-verification.md).

Copy into your project as `VERIFICATION.md` and tick as you go — a filled-in copy is also
a useful thing to show a supervisor or attach to a replication package.

---

## Ground truth

- [ ] There is a simulator that generates data from known parameters.
- [ ] A test recovers those parameters within a stated tolerance.
- [ ] The test was written **before** the implementation, or by a session that had not
      seen it.

## Adversarial checks

- [ ] I broke the model deliberately (flipped a sign) and a test failed.
- [ ] I shuffled the condition labels and the effect collapsed to chance.
- [ ] All-NaN input raises rather than returning a number.
- [ ] A duplicated subject is caught by something.
- [ ] At least one check has actually fired at some point. Checks that have never failed
      are not evidence.

## Pipeline assertions

At the top of every processing step:

- [ ] subject count equals the expected N
- [ ] every value is inside its plausible range (confidence scale, RTs, IBIs)
- [ ] no duplicate subject × trial rows
- [ ] missingness is explicit — no silent `dropna()`
- [ ] units are asserted or documented (ms vs s, BPM vs IBI)

## Eyes on data

- [ ] Distributions plotted per subject, not just in aggregate.
- [ ] Fitted curves drawn over the actual data points.
- [ ] Each variable plotted before and after every transformation.
- [ ] Residuals inspected.
- [ ] I have looked at the subject with the most extreme estimate and it is not an artefact.

## Independent confirmation

- [ ] One key number re-derived a second way (different library, language, or by hand).
- [ ] One subject computed entirely by hand from their raw file and it matches.
- [ ] A fresh session (`/clear`) reviewed the code and I addressed what it found.

## Code vs claims

- [ ] Pipeline compared line by line against the methods section; discrepancies resolved.
- [ ] Exclusions in the code match the exclusions in the text, with the same count.
- [ ] Model terms, priors, and transformations match the preregistration.
- [ ] No leftover debug flags, hardcoded paths, or `n_subjects = 5` test values.

## Reproducibility

- [ ] Every figure and table is produced by a rule in the Snakefile.
- [ ] `snakemake -n` on a clean checkout says everything is up to date for the right reasons.
- [ ] Environment is pinned and the lockfile is committed.
- [ ] Seeds set in one place and recorded.
- [ ] Provenance recorded: commit hash, date, package versions.

## Cluster runs (if applicable)

- [ ] I counted **output files containing real results**, not SLURM's COMPLETED count.
- [ ] No job was killed at the walltime — or if some were, I know which and why, and I have
      accounted for the bias that introduces.
- [ ] Nothing was computed on the frontend.

## Provenance of the code itself

- [ ] I can explain what every file in `src/` is for.
- [ ] No AI-generated data is anywhere outside `data/generated/`.
- [ ] The AI-assistance disclosure sentence in the manuscript is accurate.

---

**If more than two boxes are unticked, the honest description of what you have is "the
agent produced a number".**
