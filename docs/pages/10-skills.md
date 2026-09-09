# 10. Skills

[← Notebooks and figures](09-notebooks-and-figures.md) · [Contents](../index.md) · [Next: Cluster work →](11-hpc.md)

---

A `CLAUDE.md` gives the agent facts. A **skill** gives it a procedure — how the lab does a
thing, written once, loaded whenever that thing comes up. Skills are how knowledge stops
living in one person's head, and they are the most underused feature of Claude Code.

## What a skill is

A folder with a `SKILL.md` in it:

```
~/.claude/skills/genomedk/
├── SKILL.md          # frontmatter (name, description) + the procedure
├── references/       # detail, loaded only when needed
└── scripts/          # runnable helpers
```

The frontmatter `description` is what makes it fire. Two ways:

- **You invoke it:** `/genomedk`.
- **It invokes itself:** mention SLURM or `ssh genome`, the description matches, and the
  agent pulls the skill in without being asked.

Either way it loads **only when relevant**. That is the point, and it is why skills and
[page 2](02-context.md) belong together: a skill can hold a hundred cluster gotchas without
costing a single token until you are actually on the cluster. Compare a `CLAUDE.md`, which
loads every session and should therefore stay short.

## Why they matter for reproducibility

Three people asking an agent to submit a SLURM array get three different job scripts —
different partitions, different walltimes, one of them computing on the frontend. Three
people with the `genomedk` skill get the lab's job script. A skill turns a procedure the
agent would otherwise reinvent, plausibly and slightly differently each time, into one it
follows.

And when the procedure is wrong, you fix it in one place, and everyone's next session is
right.

## The lab's skills

They live in **[`embodied-computation-group/ai-skills`](https://github.com/embodied-computation-group/ai-skills)** —
private, so ask for access. Written once as Claude Code skills, then generated into the
formats ChatGPT, GitHub Copilot and Microsoft 365 Copilot read, so the guidance is the same
whichever tool you are in.

```bash
git clone git@github.com:embodied-computation-group/ai-skills.git ~/code/ai-skills
~/code/ai-skills/install.sh     # symlinks every skill into ~/.claude/skills/
```

Restart Claude Code so it re-scans. Then:

| skill | what it is for |
|---|---|
| `/genomedk` | Everything about the cluster. [Page 12](12-genomedk-skill.md) is the worked example. |
| `/interoception-hierarchical-models` | Hierarchical Bayesian psychophysics and meta-d′ / M-ratio / meta-Δ for HRD and RRST data: column mapping, confidence binning, cell QC, model specs, sampler diagnostics. Use it rather than asking an agent to write a meta-d′ model from scratch — that produces something that runs and is wrong. |

The repo's README also lists external collections we use without copying — pymc-labs'
`python-analytics-skills` (PyMC modelling, model evaluation, prior elicitation, marimo) and
`humanizer` — installed as plugins with `/plugin marketplace add`, so a `git pull` brings
upstream fixes.

## `/interview` — for when you do not yet know what you want

Most of this book assumes you can state the task. Often you cannot yet: a vague sense that
the analysis should do *something* about the confidence data, or a supervisor's comment you
are not sure how to act on.

`/interview` runs a short discovery conversation before anything gets built. It asks what
problem this solves and why now, surfaces the assumptions the agent was about to make
silently, offers options, and gets agreement on both the problem and the approach before
proceeding. It belongs at the **Context** step of the loop: use it when the request is
ambiguous, multi-part, or expensive to get wrong; skip it for anything you can state in two
lines.

The failure it prevents is the one [page 1](01-start-here.md) warns about — the agent
taking a surface request literally and building the wrong thing well. Currently a personal
skill of Micah's; it is being added to `ai-skills`.

## Others worth installing

- **[Crawfurd's academic research skills](https://lcrawfurd.github.io/claude-skills/)** —
  **Referee 2** runs a five-part reproducibility audit over your replication package; also
  a pre-submission reviewer and a Tufte figure critic. Copy the folders into
  `~/.claude/skills/`.
- **`/skill-creator`** — writes skills. Reach for it the second time you explain the same
  procedure to an agent.

## Writing one

The lab repo's own guidance is the best short version: *keep the body operational — the
rules that are easy to violate silently, and what going wrong actually looks like.*
Concretely:

- **A description that fires correctly.** It is the trigger. Say *when* to use the skill,
  in the words someone would actually type.
- **Symptom → cause → fix.** "A job that succeeded but wrote nothing" is a good entry.
  "Be careful with arrays" is not.
- **Lean body, detail in `references/`.** The body loads whenever the skill fires;
  references load only when the agent decides it needs them. Same principle as page 2.
- **No secrets.** A skill is a text file that gets copied around.

Add to a skill the day you lose an afternoon to something, in a session where you still have
the scar tissue:

```
Add to the genomedk skill: jobs on gpu-h200 need --gres=gpu:1 or the
node comes up with no GPU visible and fails after 40 minutes with a
CUDA error that looks like a driver problem.
```

Then push to `ai-skills`, regenerate the ports (`python3 scripts/build_ports.py`), and
open a PR. Nobody else in the lab loses that afternoon.

---

[← Notebooks and figures](09-notebooks-and-figures.md) · [Contents](../index.md) · [Next: Cluster work →](11-hpc.md)
