# 1. Start here

[Contents](../index.md) · [Next: Context is king →](02-context.md)

---

## The loop

Everything in this book is an elaboration of four steps. Learn these and the rest is
detail.

```
    CONTEXT  →  PLAN  →  EXECUTE  →  REVIEW
       ↑                               │
       └───────────────────────────────┘
```

**Context.** Before anything else, decide what the agent knows. A fresh session knows
nothing about your project: not your data, not your conventions, not what you did
yesterday. What you put in front of it — a `CLAUDE.md`, the three files that matter, two
lines saying what you want — is the entire basis for what it does next. Too little and it
guesses. Too much and it loses the thread. This is the step people skip, and it is where
most bad sessions are already lost. [Page 2](02-context.md) is about it.

**Plan.** Say what you want, then make the agent say it back as a plan before it writes any
code. Plan Mode (Shift+Tab) does exactly this. Argue with the plan while it is still text:
this is where you catch that it thinks your confidence scale is 1–4, or that it intends to
touch preprocessing. Cheap here, expensive later.

**Execute.** Let it work. Watch the first few edits. Interrupt (Esc) the moment it heads
somewhere you did not intend — after thirty seconds, not ten minutes.

**Review.** Read the diff, not the summary. Run the tests. Then `/clear` and have a fresh
session, which has no memory of what was *meant*, check what was actually *done*. Feed what
it finds into the next plan.

Round and round. A task is a few turns of this loop; a project is hundreds. The loop is
small on purpose — you should be able to hold all of it in your head while you work.
[Page 6](06-the-loop.md) is the keystrokes.

## The one rule

> **Code is generated faster than it can be verified.**

Before agents, writing code was slow and understanding it came free — you had typed it. Now
writing is nearly free and understanding is the entire job. Every practice in this book
exists to make the *Review* step cheap enough that you actually do it.

## What these tools are for

**Good at:** boilerplate and glue; trying five model specifications instead of one;
refactoring under tests; unfamiliar tooling — SLURM flags, a plotting library you use twice
a year; explaining an inherited script.

**Bad at:** knowing your data — subject 14's trigger offset, who withdrew, what
"condition 3" is; statistical judgement; saying "I do not know"; staying consistent across
a long session.

Notice the pattern. Everything in the second list is something the agent cannot know unless
you put it in front of it. That is why context comes first.

## Who this is for, honestly

The people most helped by these tools are experienced researchers, who can smell a wrong
result. The people most at risk are early-stage students, who cannot yet — and who now
produce output fast enough that nobody has time to check it.

If you are a student: slow down and review. If you are supervising: ask to see the
verification, not the code.

## Your first 30 minutes

Do not start on your real analysis.

1. Pick a small, finished analysis of yours where you know the right answer.
2. Ask Claude Code to reproduce one figure from the raw data.
3. Compare. Note every place it differed — and what it would have needed to know.

Step 3 is the point. The list you make is your first `CLAUDE.md`.

---

[Contents](../index.md) · [Next: Context is king →](02-context.md)
