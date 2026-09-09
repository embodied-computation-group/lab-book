# 5. The loop

[← Writing a CLAUDE.md](04-claude-md.md) · [Contents](../README.md) · [Next: Verification →](06-verification.md)

---

## Plan → Execute → Verify

Never hand an agent a nontrivial task cold. The loop is:

```
Shift+Tab  →  Plan Mode
              describe the task, argue about the plan, no code yet
              ↓
              approve the plan
              ↓
              it executes; you watch the diff, Esc when it goes wrong
              ↓
              /clear, then verify in a fresh session (page 6)
```

**Plan Mode first.** Shift+Tab until you are in it. The agent reads, thinks, and proposes,
but cannot edit. This is where you catch the misunderstanding, cheaply, before it has
written four files based on it. Most bad agent sessions were bad plans that nobody read.

Iterate while the plan is still just text. "No, the exclusions happen before binning."
"Use the lab's binning function." "Do not touch preprocessing, that is already done." A
plan you have argued with is worth ten minutes of watching code appear.

**Execute, but stay in the room** for the first few minutes. If the first two edits look
wrong, the next twenty will be too.

**Esc is free.** Interrupt as soon as it heads somewhere you did not intend. Correcting a
wrong direction after ten minutes costs more than interrupting after thirty seconds, both
in tokens and in dead code you will have to find later.

## Verify in a fresh session

The most important habit in this book after Plan Mode:

> `/clear`, then ask a clean context to check the work.

A session that just wrote the code is biased toward it. It knows what it meant, so it reads
the code as correct. A fresh context has only the code and your question, which is exactly
the position a reviewer is in.

Two framings that work:

```
Read src/hrd_fit.py. I did not write it and I do not trust it.
What would make this produce a wrong slope estimate?
```

```
Compare scripts/run_analysis.py against the methods section in
manuscript/methods.md. List every place they disagree.
```

That second one is worth running before every submission.

## Subagents

Define specialised assistants in `.claude/agents/`. They run in their own context with
their own tool access, so they can read forty files without filling up your main session.

Good uses in an analysis project:

- a reviewer agent that only reads and reports, with no write access
- a "find where X is computed" searcher across a large legacy pipeline
- a figure checker that reads `results/figures/` against the figure legends

Do not spawn six because you can. Parallel task switching burns a lot of context for little
gain, and you end up reviewing six half-finished things.

## Session hygiene

- **One task per session.** `/clear` between unrelated jobs. Context left over from the
  last task makes the agent worse at this one, not better.
- **Quality degrades as context fills.** If it starts forgetting your conventions or
  re-reading files it already read, that is the signal. `/clear` and restate the task.
- **Two terminals is a good pattern:** one writing, one reviewing. They do not share
  context, which is the whole point.
- **Long-running work** needs a way for the agent to check its own progress: a test
  command, a `snakemake -n` dry run, something. Without one it cannot tell whether it is
  finished, so it declares victory.

## When to stop and do it yourself

If you have interrupted three times on the same subtask, the task is underspecified or it
is something you understand better than you can describe. Write that bit yourself and hand
the rest back. Ten minutes of your own typing beats an hour of steering.

---

[← Writing a CLAUDE.md](04-claude-md.md) · [Contents](../README.md) · [Next: Verification →](06-verification.md)
