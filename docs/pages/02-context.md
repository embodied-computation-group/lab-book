# 2. Context is king

[← Start here](01-start-here.md) · [Contents](../index.md) · [Next: Setup →](03-setup.md)

---

The context window is everything the model can see: your messages, the files it has read,
the commands it has run and their output, its own earlier replies. It is the model's entire
knowledge of your project. Nothing outside it exists.

Managing that window is the highest-leverage skill in agentic coding, and the least taught,
because it feels like housekeeping. It is not. It is the difference between an agent that
does what you asked and one that does what it guessed.

## Two ways to get it wrong

**Too little.** A fresh session does not know your confidence scale, which subjects are
excluded, or that `data/raw/` is read-only. Asked to "fit the model", it fits *a* model,
plausibly and wrongly. Page 1's list of what these tools are bad at is a list of things
they could not have known.

**Too much.** The less obvious failure. Models do not use their context uniformly: as the
window fills, their ability to find and use what is in it *degrades*. This is measured, not
folklore. Chroma's 2025 report tested 18 models and found performance growing less reliable
as input length grew, even on simple tasks, and worse when the window held semantically
similar distractors. Anthropic describes the same thing as a finite *attention budget* that
every token spends down. Poldrack's reading of the evidence: degradation can begin on some
benchmarks beyond a thousand tokens, and gets bad beyond a hundred thousand.

The symptom has a name, **context rot**, and you have seen it. An agent that followed your
conventions for an hour starts ignoring them. It re-reads a file it read twenty minutes
ago. It summarises instead of doing. It goes in circles on a bug. The model has not got
worse; the window has filled with things that no longer matter, and the things that do
matter have become hard to find.

The target, in Poldrack's words: *the context window should contain all of the information
relevant to the current task, and as little as possible irrelevant information.*

## Why this is a reproducibility problem

Two sessions given the same request produce different analyses if their context differs —
one still holds the exclusion list, the other lost it under forty thousand tokens of log
output. Same instruction, different result, and nothing in the code records why. That is a
reproducibility failure in the most literal sense.

An agent going in circles also *produces things*: abandoned helpers, half-finished scripts,
files from a plan that changed midway. Each is a provenance question you will answer later.
Clean context means fewer errors and a cleaner repo, for the same reason.

## What belongs in the window

The three files that matter, not the project. A `head -5` of the data, not the data. The
error, not the log. Two lines saying what you want and what "correct" means.

- **Point, do not browse.** `@src/fit.py` beats "have a look at the code". Faster, safer,
  and nothing irrelevant comes along.
- **Just in time, not just in case.** Give it paths; let it read what it needs when it
  needs it. Do not pre-load everything that might be relevant.
- **Trim outputs.** `tail -50 slurm-*.out`, `grep ERROR` — never paste four thousand lines.
  Long outputs are the commonest way a window fills with nothing useful.
- **Never a notebook with figures in it.** Base64 images cost enormous context and the model
  cannot see them properly anyway ([page 9](09-notebooks-and-figures.md)).

## Persistent context: what survives `/clear`

The window empties; files do not. Poldrack distinguishes two kinds, and each has a home:

| Kind | Holds | Lives in |
|---|---|---|
| **Constitution** — rules that apply everywhere | interpreter path, package manager, your general standards | `~/.claude/CLAUDE.md` |
| **Memory** — this project's facts | data facts, layout, known traps, the current plan and task list | project `CLAUDE.md`, plus `PLAN.md` / `TASKS.md` / `NOTES.md` |

`CLAUDE.md` loads at the start of every session — the one piece of context you get free,
every time. [Page 5](05-claude-md.md) is about writing it. The other memory files you point
at when relevant, and you have the agent *update* them as it works, so a cleared session
picks up where the last one stopped.

## Clear, compact, or keep going

| Situation | Do |
|---|---|
| Finished a task, starting an unrelated one | `/clear`. Always. Leftover context makes the next task worse, not better. |
| Mid-problem, window filling | `/compact`. It summarises so far and continues — better than letting it auto-compact at the worst moment. |
| Ignoring conventions, re-reading files, summarising instead of doing | `/clear`, restate the task in two lines, point at the files. |
| Long work that must survive many clears | Have it keep `TASKS.md` current; reload from that. |

Poldrack's rule: clear at a breakpoint *between* problems, compact in the *middle* of one.

## Size the task to the window

A task too big rots its own context before it finishes — by step nine the agent has
forgotten step two. Too small wastes the setup. The right size is one a fresh session can
complete, including review, without you seeing any of the symptoms above. Usually that is
one function, one figure, one pipeline rule. A twelve-step plan is three tasks.

## Subagents are context isolation

A subagent runs in its own window and returns a summary. That is what they are *for*:
reading forty files to find where something is computed, without those forty files landing
in your main session. Use them to keep the main window clean, not to parallelise for its
own sake.

## The reviewer needs a clean window most of all

A session that wrote the code holds its own intentions in context, and reads the code as
doing what it meant. A fresh session has only the code. That asymmetry is why *Review* in
the loop begins with `/clear` — a reviewer sharing the writer's context is not a reviewer.

---

**Sources.** Poldrack, *Better Code, Better Science*,
[ch. 5, "Coding with AI"](https://bettercode-book.org/book-ai-coding-assistants.html) ·
Hong, Troynikov & Huber, [*Context Rot*](https://research.trychroma.com/context-rot),
Chroma, July 2025 · Anthropic,
[*Effective context engineering for AI agents*](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents).

[← Start here](01-start-here.md) · [Contents](../index.md) · [Next: Setup →](03-setup.md)
