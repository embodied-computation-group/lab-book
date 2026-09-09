# 10. Cluster work

[← Notebooks and figures](09-notebooks-and-figures.md) · [Contents](../index.md) · [Next: Driving the cluster with the genomedk skill →](11-genomedk-skill.md)

---

GenomeDK (`ssh genome`, docs at <https://genome.au.dk/docs/>). This page is the agent-
specific part. The full set of hard-won rules lives in the `genomedk` skill — run
`/genomedk` in Claude Code and it will load them.

## The rule that matters most

> **Never compute on the frontend.**

`ssh genome` puts you on `fe-open-01`, a login node shared with the entire cluster. It is
for editing, submitting, and inspecting. Not for work.

This is easy to violate *by accident with an agent*, and that is the reason it is on this
page. An agent asked to "test the script" will run the script. If that script invokes
MATLAB, Python, or a solver directly, the computation happens on the login node and
everyone notices.

Two defences:

1. Put it in your `CLAUDE.md`, in these words:

   ```
   This project runs on GenomeDK. NEVER execute computation on the frontend.
   Submit with sbatch, or request a node with srun --pty.
   Always pass --account ecg_general.
   Before running anything, tell me what it will execute and where.
   ```

2. Read what a helper script actually calls before letting anything run it. A
   `smoke_test.sh` that wraps `matlab -batch` computes on whatever node you are sitting on.

For one interactive job, ask SLURM for a shell rather than using the one you have:

```bash
srun --account ecg_general --mem 16g --pty bash
```

## Always pass --account

Without a project account you get a tiny quota and further submissions are refused.

```bash
sbatch --account ecg_general job.sbatch
```

Account choice also changes priority. `ecg_general` (qos1) outranks a personal account
here, so use it. `priority -a` explains why a job is not running.

## Partitions

| partition | max walltime | when |
|---|---|---|
| `normal` (default) | 7 days | long jobs |
| `short` | 12 hours | anything under 12 h — **use this** |
| `gpu`, `gpu-h200`, `gpu-l40s` | 7 days | GPU work |
| `gpu-short` | 2 hours | GPU debugging |

Sub-12-hour jobs belong in `short`. It is a large partition, usually not full, so they
backfill quickly even behind a deep queue. Run `gnodes` for the live picture.

Size `--time` for the **worst** case, not the typical one. A job killed at the walltime
writes nothing, and the jobs the walltime kills are exactly the slow-to-converge ones —
which biases your surviving sample toward the well-behaved cases. That is a scientific
problem, not just an inconvenience.

## Storage

| location | quota | backup | notes |
|---|---|---|---|
| `/home/<user>` | 100 GB | no | has snapshots, so deletions do not free space promptly |
| `/faststorage/project/<project>` | none | eligible | **results go here** |
| `/tmp/$SLURM_JOB_ID` | — | no | node-local, deleted with the job |

- Results on `/faststorage/project/...`, never `$HOME`.
- **`backup/` is a magic name.** Any directory called `backup`, `Backup`, or `BACKUP` under
  an eligible path is backed up weekly, 14-day retention. Do not write transient multi-GB
  output into one. Moving or renaming backed-up files triggers a full re-transfer.
- **`du` under-reports badly on BeeGFS** — it has shown 38 MB for a tree holding 3.55 GB.
  Use `ls -l` or `find -printf '%s'` when the number matters. Tell your agent this, or it
  will confidently report the wrong disk usage.

## Never let a long job depend on your ssh connection

A dying ssh session takes its children with it. A MATLAB inversion killed at minute 13
leaves a plausible-looking output file with no results in it. It looks like a result until
you open it.

Submit with `sbatch` and let SLURM own the process. If something genuinely must run outside
SLURM, detach it:

```bash
setsid nohup <cmd> > out.log 2>&1 < /dev/null & disown
```

## Verify by content, never by exit code

The cluster-specific version of page 7, and the failure mode agents fall for hardest:

> **Check the number of output files that actually contain results. Not SLURM's COMPLETED
> count.**

Jobs exit zero having done nothing. A misconfigured job array is the classic case: with
`--array=47`, `SLURM_ARRAY_TASK_MIN == MAX == 47`, so a shard count computed as
`max - min + 1` is 1, a selector like `mod(idx, 1) == 47` matches nothing, and every task
exits successfully having computed nothing. SLURM reports COMPLETED. An agent asked "did
the array finish?" will say yes.

So the question to ask is always "how many output files exist and do they contain the
fields a finished run writes", and the design rule is to **make every task skip work that
is already done**, so you can resubmit the same array until the output count is right.

## Monitoring, and telling the agent to stop polling

```bash
squeue -u $USER
jobinfo <job_id>        # GenomeDK-specific, better than stock SLURM
sacct -j <job_id> --format=JobID,State,Elapsed,ExitCode,MaxRSS -P
priority -a             # why is this not running
```

Agents poll far too eagerly. Checking a four-hour job every thirty seconds burns your
session and tells you nothing. Submit, go do something else, check back once.

## MATLAB and SPM here

Lab specifics, so nobody rediscovers them:

- SPM12: `/faststorage/project/ecg_general/toolbox/spm12`
- Always `-singleCompThread -nodisplay -nosplash -batch`. For spectral DCM,
  multithreading is *slower* — 8 threads took over 50 minutes against about 17
  single-threaded.
- Headless SPM needs `DCM.M.nograph` set explicitly. `DCM.options.nograph` is not
  propagated, so `spm_nlsi_GN` calls `spm_figure` and dies.
- Use a pinned MATLAB install, not `matlab` on `PATH`. The system R2025a here demands an
  online sign-in that a batch job cannot do.
- Output paths must be **absolute**. A relative one resolves against the payload root, the
  run succeeds, and the results are simply not where you look for them.
- At high concurrency some tasks die with MathWorks error 5001 — licence-server
  contention, not your bug. It is driven by launches per minute rather than concurrency,
  so throttle the *fast* arms of a job array, not the expensive ones.

---

[← Notebooks and figures](09-notebooks-and-figures.md) · [Contents](../index.md) · [Next: Driving the cluster with the genomedk skill →](11-genomedk-skill.md)
