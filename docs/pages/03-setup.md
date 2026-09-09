# 3. Setup

[← Context is king](02-context.md) · [Contents](../index.md) · [Next: Project layout →](04-project-layout.md)

---

## Install

```bash
npm install -g @anthropic-ai/claude-code
claude
```

First run walks you through login. Run `claude` from inside a project directory — it takes
the current directory as its working root and reads any `CLAUDE.md` it finds there.

## Plans and seats

Relevant if you are paying for this yourself. Usage is quoted as multiples of the Pro
plan's per-session allowance:

| Tier | Usage per session | Price |
|------|-------------------|-------|
| Pro | 1x | $20/mo |
| Team standard seat | 1.25x | $20/mo (free under the scientists programme) |
| Max 5x | 5x | $100/mo |
| Team premium seat | 6.25x | $100/mo ($15/mo under the scientists programme) |
| Max 20x | 20x | $200/mo |

The [Claude Team plan for scientists](https://claude.com/programs/team-plan-for-scientists)
gives eligible PIs free standard seats and $15 premium seats, fixed for 12 months. A
premium seat is slightly more headroom than Max 5x at 15% of the price, so if you were
about to buy Max 5x, do this instead. Neither seat reaches Max 20x.

Caveat: only the *per-session* multiple is published. Both Team seats and Max plans also
carry a weekly cap across all models, and its absolute size is not documented for any
tier, so the weekly ceilings are not directly comparable.

Ask Micah before buying anything — the lab may already have seats.

## Python

Python 3.13 on the lab Windows machines lives at:

```
/c/Users/<you>/AppData/Local/Programs/Python/Python313/python.exe
```

`python` and `python3` do not resolve correctly in Git Bash on these machines, so use the
full path, and tell the agent to as well — put it in your `CLAUDE.md` (page 5).

Use `uv` for project environments. It is fast, it writes a lockfile, and a lockfile is the
difference between a reproducible environment and a hopeful one:

```bash
uv venv
uv add numpy scipy pandas arviz pymc
uv run python analysis.py
```

Use `mamba`/`conda` only where you need non-Python binaries that are not on PyPI
(FSL, FreeSurfer, MATLAB toolchains). Do not mix the two in one project. Whichever you
pick, say so in `CLAUDE.md` — otherwise the agent will guess, and it guesses `pip`.

## Terminal basics you will actually use

| Key | Does |
|-----|------|
| `Shift+Tab` | Cycle modes — get to **Plan Mode** before any nontrivial task |
| `Esc` | Interrupt. Use it early and often; you are not being rude |
| `Esc Esc` | Rewind to an earlier point in the conversation |
| `/clear` | Wipe context and start fresh. Do this between unrelated tasks |
| `/model` | Switch model |
| `!` prefix | Run a shell command yourself, output goes into the conversation |
| `@` prefix | Reference a file so it gets read into context |

## Sanity check before you start real work

- `git status` is clean and you are **not** on `main`.
- The data you are pointing at is a copy, or is read-only.
- You have a `CLAUDE.md`. Even three lines is better than none.

---

[← Context is king](02-context.md) · [Contents](../index.md) · [Next: Project layout →](04-project-layout.md)
