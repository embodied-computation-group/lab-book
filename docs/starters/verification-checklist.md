# Verification checklist

Use this for results you will rely on. For the first exercise, start with the expected
answer and a rerun. Add checks as the analysis grows.

Copy this into your project as `VERIFICATION.md`. Link to evidence beside each relevant
item: test output, a diagnostic figure or a run record. Mark an item "not applicable"
with a reason when needed. See [page 7](../pages/07-verification.md).

## Scientific specification

- [ ] The question, unit of analysis, units and missing-data policy are documented.
- [ ] Model equations and conventions are specified where applicable.
- [ ] The implementation matches the intended method.
- [ ] Exploratory changes are distinguished from preregistered analyses.

## Calculation checks

- [ ] A small example agrees with a calculation made independently.
- [ ] A deliberately introduced plausible error is detected.
- [ ] Tests cover relevant invalid inputs, duplicates and missing values.
- [ ] Expected test values were reviewed and not changed merely to pass.
- [ ] Diagnostic plots have been inspected and unexpected patterns investigated.

## Model fitting, if applicable

- [ ] Recovery is assessed over relevant parameters, sample sizes and several seeds.
- [ ] Tolerances are justified and weakly identifiable parameters are discussed.
- [ ] Convergence and boundary estimates are checked.
- [ ] Reported uncertainty is evaluated, including interval coverage where appropriate.

## Review and history

- [ ] I can explain the key calculation and the limits of its checks.
- [ ] Code and new files have been reviewed.
- [ ] Any fresh-session review findings have been checked and addressed.
- [ ] Small, descriptive commits record the changes and relevant check outcomes.

## Reproduction

- [ ] A documented command reproduces the result from saved inputs and settings.
- [ ] The environment is recorded and the lockfile committed where used.
- [ ] Random seeds are recorded where applicable.
- [ ] The run record identifies code version, uncommitted changes, inputs and settings.
- [ ] A clean rerun produces the expected result.
- [ ] Fictional observations are labelled and cannot be mistaken for collected data.
- [ ] The AI-assistance disclosure accurately describes what was done.

## Cluster runs, if applicable

- [ ] Expected outputs are present and contain the required results.
- [ ] Missing, failed and timed-out jobs are accounted for.
- [ ] Computation ran on allocated compute nodes.

## Outstanding questions

Record remaining uncertainties and who will help resolve them. Completion is a judgement
about relevant evidence, not a score based on the number of ticked boxes.
