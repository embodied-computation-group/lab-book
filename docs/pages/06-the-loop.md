# 6. Running the loop

[← Writing a CLAUDE.md](05-claude-md.md) · [Contents](../index.md) · [Next: Verification →](07-verification.md)

---

[Page 1](01-start-here.md) gave you the four steps. This page is the keystrokes.

```
CONTEXT    /clear · CLAUDE.md loads · @point at files · two lines on the task
    ↓
PLAN       Shift+Tab into Plan Mode · argue with the plan · approve
    ↓
EXECUTE    watch the first edits · Esc the moment it drifts
    ↓
REVIEW     read the diff · run tests · /clear · a fresh session checks the work
    ↓
           findings go into the next plan
```

## Context: start clean, point precisely

`/clear` if this is a new task. Your `CLAUDE.md` loads on its own. Then two lines and some
`@` pointers:

```
Fit the psychometric function per subject. @src/models.py has the
simulator; @data/processed/sub-01_clean.csv shows the format.
Threshold and slope with CIs. Write the recovery test first.
```

That is enough. [Page 2](02-context.md) covers what to leave out.

If you cannot yet say what you want in two lines, run `/interview` first. It asks what
problem you are solving and why before anything gets built — [page 10](10-skills.md).

## Plan: never hand it a nontrivial task cold

Shift+Tab until you are in **Plan Mode**. The agent reads and proposes but cannot edit.
Read the plan properly — most bad sessions were bad plans nobody read. Argue while it is
still text:

- "No — exclusions happen before binning."
- "Use the lab's binning function. Do not write one."
- "Do not touch preprocessing. That is done."

A plan you have argued with is worth ten minutes of watching code appear. Approve when it
says what you meant.

## Execute: stay in the room for the first minute

If the first two edits look wrong, the next twenty will be too. **Esc is free.**
Interrupting after thirty seconds costs nothing; correcting after ten minutes costs the
tokens, the dead code, and the afternoon.

If you have interrupted three times on the same subtask, the task is underspecified or you
understand it better than you can describe. Write that bit yourself and hand the rest back.

## Review: the diff, the tests, then a stranger

1. **Read the diff.** Not the summary the agent gives you. `git diff`.
2. **Run the tests.** If there are none, that was the first thing the plan should have had.
3. **`/clear`, then ask a fresh session.** It has no memory of what was meant, only what
   was done — which is exactly a reviewer's position.

Two framings that work:

```
Read src/hrd_fit.py. I did not write it and I do not trust it.
What would make this produce a wrong slope estimate?
```

```
Compare scripts/run_analysis.py against manuscript/methods.md.
List every place they disagree. Do not summarise. List.
```

Whatever it finds goes into the next plan. That is the loop closing.

## Two terminals

The cleanest way to run this: one terminal writing, one reviewing. They share no context,
which is the point. Anthropic's docs call it the Writer/Reviewer pattern.

## Subagents, briefly

A subagent runs in its own window and returns a summary — [page 2](02-context.md) says why
that matters. Good uses: a read-only reviewer defined in `.claude/agents/`; a searcher
across a legacy pipeline; a figure checker. Bad use: six in parallel because you can. You
will review six half-finished things.

---

[← Writing a CLAUDE.md](05-claude-md.md) · [Contents](../index.md) · [Next: Verification →](07-verification.md)
