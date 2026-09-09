# 1. Start here

[← Contents](../README.md) · [Next: Setup →](02-setup.md)

---

## What this is

An agentic coding tool is not a chatbot. Claude Code reads your files, runs commands,
installs things, edits code, and keeps going until it thinks it is done. You can watch it,
redirect it, or walk away.

That autonomy is the whole benefit and the whole problem. It means you can build an
analysis pipeline in an afternoon. It also means you can generate two thousand lines of
plausible, well-commented, subtly wrong statistics in twenty minutes, and no reviewer —
including you — will be able to tell by reading it.

## The one rule

> **Code is generated faster than it can be verified.**

Everything else in this book follows from that sentence. Before agents, writing was the
slow step and verification came free with it: you understood the code because you had
typed it. Now writing is nearly free and verification is the entire job.

So the question is never "did it produce code" but "how do I know this is right". Pages
6 and 7 are the answers. Read them.

## What these tools are genuinely good at

- **Boilerplate and glue.** Loading, reshaping, merging, renaming, file wrangling. The
  work that is tedious but has an obviously correct answer you can check at a glance.
- **Exploratory breadth.** Cheap to try five model specifications instead of one, or to
  plot the data eight ways. The cost of chasing a hunch drops a lot.
- **Refactoring under test.** If you have tests, an agent is very good at reorganising
  code without breaking it. If you have no tests, it is very good at breaking it silently.
- **Unfamiliar tooling.** SLURM syntax, a plotting library you use twice a year,
  a preprocessing tool's flags. It has read the manual so you do not have to.
- **Reading code.** "What does this script actually do, and does it match the paper's
  methods section" is a genuinely strong use.

## What they are bad at

- **Knowing your data.** It has no idea that subject 14's trigger channel is offset, that
  your confidence scale is 1–100 rather than 1–4, or that three participants withdrew.
  It will happily analyse nonsense.
- **Statistical judgement.** It will implement whatever you ask, including things you
  should not do. It does not know your preregistration.
- **Saying "I do not know".** It will produce an answer. The answer may be an invention.
- **Long-horizon consistency.** Over a long session it accumulates dead code, orphaned
  scripts, and files nobody asked for. Commit often so you can see what changed.

## The honest risk for a lab

The people most helped by these tools are experienced researchers, who can smell a wrong
result. The people most at risk are early-stage students, who cannot yet — and who now
produce output fast enough that nobody has time to check it.

If you are a student: slow down and check things. If you are supervising: agent-written
analysis code needs the same scrutiny as an agent-written paragraph, and reading it is not
enough. Ask to see the verification, not the code.

## Your first 30 minutes

Do not start on your real analysis. Do this instead:

1. Pick a small, already-finished analysis of yours where you know the right answer.
2. Ask Claude Code to reproduce one figure from the raw data.
3. Compare with your own result. Note every place it differed.

That exercise will teach you more about where these tools fail than any tutorial,
including this one.

---

[← Contents](../README.md) · [Next: Setup →](02-setup.md)
