# 8. Reproducibility

[← Verification](07-verification.md) · [Contents](../index.md) · [Next: Notebooks and figures →](09-notebooks-and-figures.md)

---

Verification asks "is this right". Reproducibility asks "could anyone, including me in six
months, get this number again". Agents make the second question much harder, because they
regenerate files freely and cheerfully.

## Put an orchestrator between the agent and your outputs

This is the highest-leverage thing on the page. Use **Snakemake** (preferred in this lab)
or `make`. Skeleton at [`starters/Snakefile`](../starters/Snakefile).

Why it matters more with an agent than without: an agent will re-run a script, overwrite a
figure, and move on. Without a dependency graph you cannot tell which outputs are current,
which are stale, and which code produced any of them. Provenance dissolves in an afternoon
of enthusiastic iteration.

With a Snakefile you get, for free:

- **`snakemake -n`** — dry run. What would rebuild, and why. Have the agent run this
  before it runs anything.
- **stale detection** — outputs older than their inputs get rebuilt, so you cannot
  accidentally report a figure from last week's exclusions.
- **one command to reproduce everything** — `snakemake --cores 4 all`. That command is
  what goes in your README and your replication package.
- **a readable map of the analysis** — which is also the best possible context for an
  agent joining the project.

Rule for the lab: **if a figure in a paper was not produced by a rule in the Snakefile, it
does not go in the paper.**

## Pin the environment

```bash
uv add pymc arviz     # writes uv.lock
uv run python scripts/fit.py
```

Commit `uv.lock`. "It worked on my machine in March" is not a method.

For conda projects, export an explicit environment and commit it:

```bash
mamba env export --no-builds > environment.yml
```

For anything with heavy neuroimaging dependencies (fMRIPrep, FreeSurfer, FSL), use the
container. Version-pinned containers are the only thing that makes those pipelines
reproducible across machines and across years. Record the exact image tag, not `:latest`.

## Seeds

Every stochastic step takes an explicit seed, set in one place:

```python
SEED = 20260909
rng = np.random.default_rng(SEED)
```

Not `np.random.seed()` scattered through the code. Pass `rng` down. For MCMC, set the seed
in the sampler call and record the sampler version — different PyMC versions can give
different draws from identical seeds.

## Provenance: what produced this file

Cheap habit, large payoff. Have every output carry its origin:

- write a small sidecar with each result: git commit hash, timestamp, input file hashes,
  seed, package versions
- or stamp the commit hash into figure metadata or a corner of the figure while drafting
- Snakemake logs already give you much of this if you keep the `.snakemake/` directory

The question you are protecting against is a reviewer asking, in month eleven, why table 2
disagrees with figure 3.

## What an agent must never do

Put these in your `CLAUDE.md`:

```
Do not write to data/raw/.
Do not modify uv.lock or environment.yml without being asked.
Do not commit. I commit.
Do not run the full pipeline; run `snakemake -n` and show me the plan.
Do not create data files to make a script run. If input is missing, stop and say so.
```

The last one prevents the worst failure mode there is: the agent inventing plausible data
to get past an error, and that data ending up in a result. If it must create test data, it
goes in `data/generated/` (page 4) and it says so.

## The replication package

When you submit, someone should be able to run the analysis from a clean machine. That
means:

- [ ] `README.md` with the one command that reproduces everything
- [ ] pinned environment (`uv.lock`, `environment.yml`, or a container tag)
- [ ] Snakefile or Makefile covering every figure and table in the paper
- [ ] data either included, or a script that fetches it, or a clear access statement
- [ ] seeds set and recorded
- [ ] tests that pass on a clean checkout
- [ ] a note on what was AI-assisted (increasingly expected; see page 14)

Before submitting, run the reproducibility audit skill from
[Crawfurd's skill set](https://lcrawfurd.github.io/claude-skills/) against your own repo.
Being your own Referee 2 is cheaper than the real one.

---

[← Verification](07-verification.md) · [Contents](../index.md) · [Next: Notebooks and figures →](09-notebooks-and-figures.md)
