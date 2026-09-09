# 12. Driving the cluster with the genomedk skill

[← Cluster work](11-hpc.md) · [Contents](../index.md) · [Next: Human-subject data →](13-data-and-ethics.md)

---

This optional example combines the workflow from [page 6](06-the-loop.md) with the lab's
cluster procedure. Use it when you have an analysis that needs GenomeDK, after you have
checked the code on a small case.

A **job array** runs the same script for several inputs, such as one model fit per
participant. A **smoke test** is a small initial run to check that the setup works.

## Load the procedure and plan

With the skill installed from the lab's [ai-skills repository](https://github.com/embodied-computation-group/ai-skills),
invoke `/genomedk`. For example:

```text
/genomedk
Plan a job array for the analysis described in MODEL.md.
Each input takes about 20 minutes. Use the approved project storage.
Check the account, partition, resource requests and output paths.
Do not submit yet. Show how each array task selects its input,
including when we submit only one task.
```

Read the plan against [page 11](11-hpc.md) and the current cluster documentation.
The skill supplies local procedure, but you still need to check that it was applied
correctly. Save the job script and configuration in a focused commit.

## Run one task

```text
Submit one task as a smoke test using the agreed configuration.
Confirm that computation runs on an allocated node.
Check the output against the expected schema and completion criteria.
Report job status and output validation, without printing participant data.
```

A successful exit is not enough. Check that the file contains the expected fitted
parameters and diagnostics, and that the intended input was processed.

If the single-task selection is wrong, fix and commit the indexing before proceeding.
Submitting one element of an array must not change the mapping from task IDs to inputs.

## Run the remaining work

```text
The smoke test passed. Submit the remaining tasks.
Keep the same input mapping and configuration.
Validate existing outputs before skipping them.
Record job IDs and the code commit, and check progress at an interval
appropriate to the expected run time.
```

Count validated outputs and account for missing or failed tasks. Check whether timeouts
disproportionately affect particular inputs. Keep the run record with the results in
approved storage.

## Record a useful fix

When you discover a cluster issue, describe the symptom, cause and tested remedy in the
shared skill. For example, a missing GPU request belongs beside the GPU submission
instructions.

```text
Draft a short update to the genomedk skill describing the failure we
just diagnosed and the fix we tested. Include the conditions under
which it applies. Show me the change before committing it.
```

Follow the ai-skills repository's current instructions for updating generated copies and
opening a PR. Other lab members receive the change when they update their installation.

---

[← Cluster work](11-hpc.md) · [Contents](../index.md) · [Next: Human-subject data →](13-data-and-ethics.md)
