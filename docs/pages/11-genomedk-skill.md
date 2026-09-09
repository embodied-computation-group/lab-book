# 11. Driving the cluster with the `genomedk` skill

[← Cluster work](10-hpc.md) · [Contents](../index.md) · [Next: Human-subject data →](12-data-and-ethics.md)

---

Page 10 is the rules. This page is the tooling: the lab keeps its GenomeDK knowledge in a
**skill**, so you do not have to remember any of it and neither does the agent.

## What a skill is

A skill is a folder of instructions that Claude Code loads on demand. It sits in
`~/.claude/skills/<name>/` with a `SKILL.md` inside, and it has two ways of firing:

- **you invoke it** — type `/genomedk` in Claude Code
- **it triggers itself** — the description in its frontmatter tells the agent when the
  skill is relevant, so mentioning SLURM or `ssh genome` pulls it in automatically

The point is that it is loaded *only when needed*. It can be long and detailed without
costing you context on unrelated work, which is why it is the right home for a hundred
cluster gotchas.

## Using it

```
/genomedk
```

Then say what you want. It works well when you describe the goal rather than the commands:

```
/genomedk
I need to run the spectral DCM inversion over all 487 subjects in
manifest.csv. Each takes about 20 minutes. Set up the job array and
submit one task as a smoke test first.
```

What the skill supplies, so you do not have to:

- **the frontend rule** — it will submit rather than run, and it knows that
  `smoke_test.sh` calling `matlab -batch` is a trap
- **`--account ecg_general`** on every submission, and why that account beats a personal one
- **partition choice** — `short` for sub-12-hour work, and the current walltime table
- **`--array=0-486%50`** syntax, sharding by `mod(idx, n_tasks)`, and the single-element
  array trap that makes SLURM report COMPLETED having computed nothing
- **storage layout** — results to `/faststorage`, the magic `backup/` directory name, and
  the fact that `du` under-reports on BeeGFS
- **our SPM12 and MATLAB paths**, `-singleCompThread`, the `DCM.M.nograph` requirement
- **verify by content, not exit code** — count output files with real fields in them
- **MathWorks error 5001** at high launch rates, and designing tasks to skip completed work
  so you can resubmit the same array

Without the skill you get generic SLURM advice that is subtly wrong for this cluster. With
it you get our cluster.

## A good session shape

```
/genomedk

Plan only, do not submit yet: I want to fit the RRST psychophysical
model per subject on GenomeDK. Inputs are in
/faststorage/project/ecg_general/rrst/derivatives.
Roughly 90 subjects, a few minutes each.
```

Read the plan. Check the account, the partition, the walltime, and where output lands. Then:

```
Submit exactly one task as a smoke test. Report the output file path
and size, and confirm it contains fitted parameters.
```

Only then the full array. This sequence — plan, one task, verify content, full submit — is
the whole discipline of cluster work, and it maps directly onto page 6.

## Things to still do yourself

The skill removes the recall burden, not the judgement:

- **`--time` sizing.** You know how long your model takes. Size for the worst case
  (page 10), because the jobs a walltime kills are the slow-converging ones and losing them
  biases your sample.
- **Deciding a run is finished.** Ask for the count of output files containing real
  results. Never accept "the array completed".
- **Anything touching participant data.** Page 12 applies on the cluster exactly as it does
  locally.

## Adding to the skill

This is the part that compounds. When you lose an afternoon to a cluster quirk, put it in
the skill and nobody in the lab loses that afternoon again.

The file is at:

```
~/.claude/skills/genomedk/SKILL.md
```

Easiest route is to just ask, in a session where you have the fresh scar tissue:

```
Add to the genomedk skill: jobs on gpu-h200 need --gres=gpu:1 or they
get a node with no GPU visible and fail after 40 minutes with a CUDA
error that looks like a driver problem.
```

Write entries the way the existing ones are written: the symptom you actually saw, why it
happens, and the fix. "A job that succeeded but wrote nothing" is a useful entry.
"Be careful with arrays" is not.

The skill currently lives in Micah's `~/.claude/skills/`. If you want it, ask — the medium-
term plan is to keep the lab's skills in a repo everyone clones into their skills
directory, at which point improvements travel by pull request.

## Other lab skills worth knowing

- **`interoception-hierarchical-models`** — fits hierarchical Bayesian psychophysical and
  metacognitive models (meta-d′, M-ratio, meta-Δ) to HRD (cardiac and auditory-control) and
  RRST trial data. Covers dependency install, mapping raw trial columns onto model
  variables, confidence-scale handling, cell QC, model specification, and sampler
  diagnostics. Use it rather than asking an agent to write a meta-d′ model from scratch;
  it will produce something that runs and is wrong.
- **`nano-banana-pro`**, **`paper-banana`** — figure and diagram generation.
- **`skill-creator`** — for writing your own. Worth reaching for the second time you
  explain the same procedure to an agent.

Run `/help` to see what is currently installed.

---

[← Cluster work](10-hpc.md) · [Contents](../index.md) · [Next: Human-subject data →](12-data-and-ethics.md)
