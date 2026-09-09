# 5. Writing a CLAUDE.md

[← Project layout](04-project-layout.md) · [Contents](../index.md) · [Next: The loop →](06-the-loop.md)

---

`CLAUDE.md` sits in your project root and is read at the start of every session. It gives the
agent recurring project instructions without having to repeat them in each prompt.

There is a ready-made one at [`starters/CLAUDE.md`](../starters/CLAUDE.md). Copy the instruction block and
edit it. What follows is why each part is there.

## What belongs in it

**Environment and commands.** The package manager, how to run the tests and analysis,
and an interpreter path if the project needs one.

**Directory rules.** Include where fictional test observations belong and how raw data
is protected; see [page 4](04-project-layout.md).

**Data definitions.** Document facts that affect the calculation:

- what your confidence scale actually is (1–100? 1–4? relabelled?)
- exclusion criteria and how they are applied; keep participant lists in approved storage
- that your trial column is 1-indexed but your event file is 0-indexed
- that "condition 3" is the auditory control, not a heartbeat condition
- units, such as milliseconds or seconds, and beats per minute (BPM) or interbeat
  interval (IBI).

These definitions let both the agent and your collaborators interpret the files correctly.

**Known pitfalls.** Record relevant library incompatibilities, cluster behaviour and
missing-value conventions. Describe the symptom and the verified fix.

**Statistical guardrails.** "This analysis is preregistered; do not add predictors that
are not in the registration." "Do not drop outliers without asking." "Confidence must be
binned with the lab's standard function, not `pd.qcut`."

## What does not belong

- Anything secret. This file is committed and readable by anyone with repo access.
- Participant identifiers or clinical detail. See [page 13](13-data-and-ethics.md).
- Long prose. It is read every session and it consumes context. Bullet points, imperatives.
- Things that are true of all your projects — those go in your personal
  `~/.claude/CLAUDE.md` instead, which applies everywhere.

## Start with the project file

A short project file is enough for the first exercise. Personal defaults are optional:
use them when you find yourself repeating the same instructions across projects.

## Two levels

| File | Scope | Put here |
|------|-------|----------|
| `~/.claude/CLAUDE.md` | your user account | General preferences and relevant local setup |
| `<project>/CLAUDE.md` | one project, whole lab | Data facts, layout, pipeline commands |

Project-level is committed, so a rule you add helps everyone who touches the repo.
Prefer portable commands such as `uv run python` to a path on one person's machine.
Keep machine-specific settings local rather than presenting them as lab conventions.

## Keeping it alive

When a correction will matter again, ask the agent to add it to `CLAUDE.md`, then review
the wording. Task status belongs in `TASKS.md`; analysis decisions and their rationale
belong in project notes.

Review the file periodically. Remove obsolete instructions and check copied rules
against the new project's needs.

## Try it

Adapt the starter file for the first exercise. Ask a fresh session to describe the
intended calculation using only the project files. Any missing or incorrect assumption
is a reason to improve the instructions.

---

[← Project layout](04-project-layout.md) · [Contents](../index.md) · [Next: The loop →](06-the-loop.md)
