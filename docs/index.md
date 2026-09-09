# Agents in the Lab

**Claude Code for reproducible science.** A handbook from the Embodied Computation Group,
written for PhD students and postdocs starting to use agentic coding tools on real analyses
— who want the results to still be right, and still be reproducible, afterwards.

Short pages, one idea each. Read in order the first time; use as a reference after that.

Public on purpose. Add to it — see [Contributing](pages/16-contributing.md).

---

## The loop

The whole book hangs on four steps:

```
    CONTEXT  →  PLAN  →  EXECUTE  →  REVIEW
       ↑                               │
       └───────────────────────────────┘
```

Decide what the agent knows. Make it say the plan back before it codes. Watch the first
edits. Check the diff in a fresh session, and feed what you find into the next plan.
[Page 1](pages/01-start-here.md) explains it in a screen; [page 6](pages/06-the-loop.md)
has the keystrokes.

## How to read this

**New to agentic coding?** Pages 1 and 2, then 3–10 in order. About an hour, and it covers
everything you need to not make a mess.

**Already using Claude Code?** Read 2 — context is the step experienced users skip too.
Then 4, 6, 7 and 8: project layout, the loop, verification, reproducibility. Those hold the
actual lab policy.

**Working on the cluster?** 11 and 12.

**Just want the reading list?** [Resources](pages/15-resources.md).

---

## Contents

### Foundations

| # | Page | What it covers |
|---|------|----------------|
| 1 | [Start here](pages/01-start-here.md) | The loop, the one rule, who this is for |
| 2 | [Context is king](pages/02-context.md) | The context window, context rot, what belongs in it, clear vs compact |

### Getting going

| # | Page | What it covers |
|---|------|----------------|
| 3 | [Setup](pages/03-setup.md) | Install, plans and seats, Python, keys you will use |
| 4 | [Project layout](pages/04-project-layout.md) | The directory contract, and why `data/generated/` exists |
| 5 | [Writing a CLAUDE.md](pages/05-claude-md.md) | Persistent context: the agent's memory of your project |

### Doing the work

| # | Page | What it covers |
|---|------|----------------|
| 6 | [Running the loop](pages/06-the-loop.md) | Plan Mode, Esc, fresh-session review — the keystrokes |
| 7 | [Verification](pages/07-verification.md) | How to know the analysis is right, not just finished |
| 8 | [Reproducibility](pages/08-reproducibility.md) | Orchestrators, pinned environments, seeds, provenance |
| 9 | [Notebooks and figures](pages/09-notebooks-and-figures.md) | Text-based notebooks, cheap plots, figure review |
| 10 | [Skills](pages/10-skills.md) | Procedures the agent follows instead of reinventing; the lab skills repo; `/interview` |

### Lab specifics

| # | Page | What it covers |
|---|------|----------------|
| 11 | [Cluster work](pages/11-hpc.md) | GenomeDK and SLURM with an agent in the loop |
| 12 | [Driving the cluster with the `genomedk` skill](pages/12-genomedk-skill.md) | The worked example: a skill doing the remembering for you |
| 13 | [Human-subject data](pages/13-data-and-ethics.md) | What must never enter a context window |
| 14 | [Tips and tricks](pages/14-tips-and-tricks.md) | Prompting, patterns, MCP servers, time-wasters |

### Reference

| # | Page | What it covers |
|---|------|----------------|
| 15 | [Resources](pages/15-resources.md) | Annotated reading list, every link checked |
| 16 | [Contributing](pages/16-contributing.md) | How to add a page, and what does not go in |

### Starters

Copyable starting points, in [`docs/starters/`](starters/project-tree.md):

- [`CLAUDE.md`](starters/CLAUDE.md) — project context file, with the data-facts section filled in as an example
- [`Snakefile`](starters/Snakefile) — pipeline skeleton, including a provenance rule
- [`gitignore`](starters/gitignore) — research `.gitignore`
- [`verification-checklist.md`](starters/verification-checklist.md) — run before you believe a result
- [`project-tree.md`](starters/project-tree.md) — the standard layout, and the command to make it

---

## The short version

If you read nothing else:

1. **Context first.** The agent knows only what is in the window. Too little and it
   guesses; too much and it forgets. Point at files; `/clear` between tasks.
2. **Plan before code.** Plan Mode, and argue with the plan while it is still text.
3. **Code is generated faster than it can be verified.** Review is the job now.
4. **Review in a fresh session.** A context that wrote the code is a bad judge of it.
5. **An orchestrator between the agent and your outputs**, so you know which code produced
   which file.
6. **Generated data never touches `data/raw/` or `data/processed/`.**
7. **Never compute on the GenomeDK frontend.** An agent asked to "test the script" will run
   the script.
8. **No participant data in a context window.** Ever. See page 13.

---

*Started 2026-09-09. Page 15 links were all opened and checked on that date.*
