# 8. Reproducibility

[← Verification](07-verification.md) · [Contents](../index.md) · [Next: Notebooks and figures →](09-notebooks-and-figures.md)

---

A reproducible analysis can be rerun from its saved code, inputs and settings. Start with
one documented command. You do not need a workflow framework for a small project.

A **pipeline** is simply the sequence of steps that turns inputs into results: for
example, load data, check it, calculate participant means and save a figure.

## Start with a script and a README

Put the steps in a script that runs from beginning to end without requiring you to
remember which notebook cells to execute. In the exercise, that might be:

```bash
uv run python scripts/analyse.py
```

This command is an example: use the actual filename in your project. In `README.md`,
record the environment setup, required input files, settings, output locations and test
command. State whether a rerun overwrites results.

Ask the agent to assemble the pipeline from your specification, then test it on the
fictional example. Keep the calculation in a function you can test separately.

## Save the environment and settings

Commit `pyproject.toml` and `uv.lock`. These record Python dependencies. A collaborator
with uv installed can restore the locked project environment using:

```bash
uv sync --locked
```

Record the Python version too. For an existing conda or container-based project, follow
its documented setup rather than replacing it.

For random simulations or sampling, record a seed and pass it explicitly. For example:

```python
import numpy as np

rng = np.random.default_rng(20260909)
```

A seed helps repeat a run under the same conditions. Changes in software or hardware
can still affect numerical results.

## Record which version produced the result

Small Git commits are part of the analysis cycle. See the
[commit workflow on page 4](04-project-layout.md#git-commits-during-the-work).

For each result you intend to keep, record the code commit, input version or hashes,
settings, seed, software versions and run command. Also record whether the code had
uncommitted changes. A commit hash alone cannot identify those changes.

Keep this record next to the output or in a run log. Do not include participant
information in records sent to the agent.

## Check a clean rerun

Ask a lab mate to follow the README from a clean checkout and environment, using the
fictional exercise data or approved access to research inputs. A **checkout** is a local
copy of the repository at a particular version.

Can they produce the expected result without your chat history or manual instructions?
If something is missing, fix the instructions or script and try that step again.
A reproducible result can still be scientifically wrong; keep the verification checks
from [page 7](07-verification.md).

## Optional: automate a larger pipeline with Snakemake

Once an analysis has several scripts, manual execution can become awkward. You may
forget to rerun a figure after changing a preprocessing step. A workflow tool such as
**Snakemake** records the dependencies and decides which steps need to run.

A **Snakefile** is the text file in which you describe those steps. Each **rule** states
the input files, output files and command for one step. Here is an illustrative rule
for a script that already exists:

```python
rule participant_means:
    input:
        data="data/generated/trials.csv",
        code="scripts/participant_means.py"
    output:
        "results/participant_means.csv"
    shell:
        "uv run python {input.code:q} --input {input.data:q} --output {output:q}"
```

If the CSV or script changes, Snakemake can recognise that the output needs rebuilding.
Other influences, such as configuration files, must also be declared.

With Snakemake installed, `snakemake -n` shows what it would run without running the
analysis. `snakemake --cores 1` executes it with one CPU core available. These examples
assume you have written the script, provided the input and created any needed output
directories.

The larger [starter Snakefile](../starters/Snakefile) illustrates a multi-step analysis.
It needs project-specific scripts and configuration; it is not a runnable tutorial.
There is no need to adopt it for the first exercise. Learn it when maintaining the
sequence of analysis steps becomes a problem. The
[official tutorial](https://snakemake.readthedocs.io/en/stable/tutorial/basics.html)
walks through a working example.

## Before sharing an analysis

- Document the command, environment, inputs and expected outputs.
- Save code and specifications in Git, with small, descriptive commits.
- Run the relevant tests and inspect the results.
- Reproduce the analysis from the saved files in a clean environment.
- Record AI assistance accurately; see [page 13](13-data-and-ethics.md).

---

[← Verification](07-verification.md) · [Contents](../index.md) · [Next: Notebooks and figures →](09-notebooks-and-figures.md)
