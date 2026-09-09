# 6. Running the loop

[← Writing a CLAUDE.md](05-claude-md.md) · [Contents](../index.md) · [Next: Verification →](07-verification.md)

---

Use this workflow for a substantial analysis change. Practise it with the
[first exercise](first-exercise.md) before applying it to unfamiliar methods.

## Context: state the question and your proposed approach

Write down the calculation you expect before asking the agent to code. Include the
relevant files, constraints and a way to check the result. For example:

```text
Fit the psychometric function defined in src/models.py.
Use the column definitions in docs/data-schema.md and fictional
data from data/generated/. Return threshold and slope with 95% CIs.
Keep preprocessing unchanged. Propose a parameter-recovery test
before implementation, and identify any missing specifications.
```

This is a starting brief. The agent may need to ask about the interval method, fitting
bounds or missing values. Resolve those questions before approving the analysis.

If the task is still vague, ask: "Help me clarify the question. Ask about the inputs,
scientific assumptions and intended output before proposing code." The optional
`/interview` skill on [page 10](10-skills.md) supports this conversation.

## Plan: check the scientific decisions

In Claude Code, use Shift+Tab to select Plan Mode. Read the proposed approach and check:

- which observations it includes and how it handles missing values;
- units, transformations, model terms and parameter definitions;
- existing functions it will reuse;
- files it will change and tests it will run.

Give concrete corrections: "Exclusions happen before binning" or "Use the existing
confidence-binning function." Save decisions that affect the analysis in the project notes.

## Execute: inspect progress

Approve the agreed task and watch the first changes. Ask the agent to commit each
coherent step with a descriptive message and the relevant check results. Use Esc if the agent starts changing
preprocessing, relaxing tests or expanding the scope without a reason.

Repeated unsuccessful attempts are a reason to reassess. Ask what each attempt established
and whether the approach is feasible. A smaller task, a reference implementation or help
from someone who knows the method may be more useful than another retry.

## Review: examine evidence

1. Inspect `git diff` and `git status`, including new files that are not yet tracked.
2. Run the tests and read what they check. Investigate changes to expected values.
3. Compare the result with an independent calculation, simulation or reference.
4. Ask a fresh session to review the specification and implementation.

For example:

```text
Compare src/hrd_fit.py with docs/model-specification.md.
Look for errors in parameterisation, units, missing-data handling
and uncertainty estimates. Give file locations and a way to
reproduce each finding. Do not edit files.
```

A fresh reviewer can find additional problems, but it can also miss errors or report
ones that are not there. Check each finding. [Page 7](07-verification.md) explains how
to choose stronger evidence for a scientific result.

Two terminals are useful if you want to keep the writing session available while a
separate session reviews. Keep the reviewer read-only to avoid conflicting edits.

## Finish and record what you learned

Have the agent save small commits throughout the cycle: the specification, reviewed
tests, implementation and later improvements. A test-first commit may record expected
failures; the implementation commit should record the passing checks.
[Page 4](04-project-layout.md) explains how this helps with PR review and recovery.

Record the run command, checks and unresolved questions.
Update project instructions when a correction will matter again. Then begin the next
task with the relevant context.

In supervision, explain one change from question to code to evidence. If you cannot
explain a step, use that as the next learning task.

---

[← Writing a CLAUDE.md](05-claude-md.md) · [Contents](../index.md) · [Next: Verification →](07-verification.md)
