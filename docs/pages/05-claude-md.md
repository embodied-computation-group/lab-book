# 5. Writing a CLAUDE.md

[← Project layout](04-project-layout.md) · [Contents](../index.md) · [Next: The loop →](06-the-loop.md)

---

`CLAUDE.md` sits in your project root and is read at the start of every session. It is the
difference between explaining your conventions forty times and explaining them once.

There is a ready-made one at [`starters/CLAUDE.md`](../starters/CLAUDE.md). Copy it and
edit. What follows is why each part is there.

## What belongs in it

**Environment facts it cannot guess.** The interpreter path, the package manager, how to
run the tests, how to run the pipeline. This alone saves the most time.

**Your directory contract.** Page 4, stated as rules. Especially the `data/generated/`
quarantine and the read-only raw data.

**Domain facts about your data.** This is the highest-value section and the one people
skip. The agent does not know:

- what your confidence scale actually is (1–100? 1–4? relabelled?)
- which subjects are excluded and why
- that your trial column is 1-indexed but your event file is 0-indexed
- that "condition 3" is the auditory control, not a heartbeat condition
- units. Milliseconds or seconds. BPM or IBI.

Every one of these has produced a wrong-but-plausible analysis somewhere. Write them down.

**Hard-won bug notes.** When you lose an afternoon to something — a library version that
breaks, a cluster quirk, a silent NaN — add a line. This is where a `CLAUDE.md` starts
paying compound interest, and it is the closest thing the lab has to institutional memory.

**Statistical guardrails.** "This analysis is preregistered; do not add predictors that
are not in the registration." "Do not drop outliers without asking." "Confidence must be
binned with the lab's standard function, not `pd.qcut`."

## What does not belong

- Anything secret. This file is committed and readable by anyone with repo access.
- Participant identifiers or clinical detail. See page 11.
- Long prose. It is read every session and it consumes context. Bullet points, imperatives.
- Things that are true of all your projects — those go in your personal
  `~/.claude/CLAUDE.md` instead, which applies everywhere.

## Two levels

| File | Scope | Put here |
|------|-------|----------|
| `~/.claude/CLAUDE.md` | you, everywhere | Python path, your general preferences |
| `<project>/CLAUDE.md` | one project, whole lab | Data facts, layout, pipeline commands |

Project-level is committed, so a rule you add helps everyone who touches the repo.

## Keeping it alive

The useful habit: when you find yourself correcting the agent about the same thing twice,
that correction is a `CLAUDE.md` line. You can just say so mid-session —
*"add that to CLAUDE.md"* — and it will.

Review the file when you finish a project. Half of it will be scaffolding you no longer
need; the other half is worth copying into the next project.

---

[← Project layout](04-project-layout.md) · [Contents](../index.md) · [Next: The loop →](06-the-loop.md)
