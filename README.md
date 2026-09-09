# ECG Lab Book

An internal handbook for the Embodied Computation Group. Short pages, one idea each, meant
to be read in order the first time and used as a reference afterwards.

**Part I — Agentic coding for reproducible science** is the current content: how to use
Claude Code and similar tools on real analyses without quietly destroying the
reproducibility of your results.

Private repo, internal use. Add to it freely — see [Contributing](pages/14-contributing.md).

---

## How to read this

**New to agentic coding?** Pages 1–7 in order. About 45 minutes, and it covers everything
you need to not make a mess.

**Already using Claude Code?** Skim 3, 5, 6, 7 — project layout, the loop, verification,
reproducibility. Those four pages contain the actual lab policy.

**Working on the cluster?** 9 and 10.

**Just want the reading list?** [Resources](pages/13-resources.md).

---

## Contents

### Getting going

| # | Page | What it covers |
|---|------|----------------|
| 1 | [Start here](pages/01-start-here.md) | What these tools are good and bad at, and the one rule that matters |
| 2 | [Setup](pages/02-setup.md) | Install, plans and seats, Python, keys you will use |
| 3 | [Project layout](pages/03-project-layout.md) | The directory contract, and why `data/generated/` exists |
| 4 | [Writing a CLAUDE.md](pages/04-claude-md.md) | Giving the agent your project's rules |

### Doing the work

| # | Page | What it covers |
|---|------|----------------|
| 5 | [The loop](pages/05-the-loop.md) | Plan → Execute → Verify, and how to interrupt |
| 6 | [Verification](pages/06-verification.md) | How to know the analysis is right, not just finished |
| 7 | [Reproducibility](pages/07-reproducibility.md) | Orchestrators, pinned environments, seeds, provenance |
| 8 | [Notebooks and figures](pages/08-notebooks-and-figures.md) | Text-based notebooks, cheap plots, figure review |

### Lab specifics

| # | Page | What it covers |
|---|------|----------------|
| 9 | [Cluster work](pages/09-hpc.md) | GenomeDK and SLURM with an agent in the loop |
| 10 | [Driving the cluster with the `genomedk` skill](pages/10-genomedk-skill.md) | How skills work, and using ours instead of remembering any of it |
| 11 | [Human-subject data](pages/11-data-and-ethics.md) | What must never enter a context window |
| 12 | [Tips and tricks](pages/12-tips-and-tricks.md) | Context hygiene, prompting, MCP servers, time-wasters |

### Reference

| # | Page | What it covers |
|---|------|----------------|
| 13 | [Resources](pages/13-resources.md) | Annotated reading list, every link checked |
| 14 | [Contributing](pages/14-contributing.md) | How to add a page |

### Templates

Copyable starting points in [`templates/`](templates/):

- [`CLAUDE.md`](templates/CLAUDE.md) — project context file, with the data-facts section filled in as an example
- [`Snakefile`](templates/Snakefile) — pipeline skeleton, including a provenance rule
- [`gitignore`](templates/gitignore) — research `.gitignore`
- [`verification-checklist.md`](templates/verification-checklist.md) — run before you believe a result
- [`project-tree.md`](templates/project-tree.md) — the standard layout, and the command to make it

---

## The short version

If you read nothing else:

1. **Code is generated faster than it can be verified.** Verification is the bottleneck in
   your work now, not writing. Budget your time accordingly.
2. **Put an orchestrator between the agent and your outputs** so you always know which code
   produced which file.
3. **Generated data never touches `data/raw/` or `data/processed/`.**
4. **Review in a fresh session.** A context that just wrote the code is a bad judge of it.
5. **Never compute on the GenomeDK frontend.** An agent asked to "test the script" will run
   the script.
6. **No participant data in a context window.** Ever. See page 11.

---

*Started 2026-09-09. Page 13 links were all opened and checked on that date.*
