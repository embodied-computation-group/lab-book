# CLAUDE.md template

Copy this into a project root as `CLAUDE.md`, delete what does not apply, and fill in the
data facts. The data facts section is the one that matters most and the one people skip.

See [page 4](../pages/04-claude-md.md) for why each section is here.

---

```markdown
# Project: <name>

## What this is
One or two sentences. What question, what data, what stage.

## Environment
- Python: /c/Users/Micah/AppData/Local/Programs/Python/Python313/python.exe
  (`python` and `python3` do not resolve in Git Bash on this machine — use the full path)
- Package manager: uv. Do not use pip or conda in this project.
- Run tests: `uv run pytest`
- Run pipeline: `snakemake -n` for a dry run. Never run the full pipeline without asking.

## Layout
- data/raw/       READ-ONLY. Never write here.
- data/processed/ derived from raw by code in src/ only
- data/generated/ synthetic, simulated, or AI-generated data. ONLY here.
- src/            importable, tested functions
- scripts/        thin entry points that call src/
- notebooks/      .qmd or marimo .py. Never .ipynb.
- results/        figures and tables, produced only by Snakemake rules

## Hard rules
- Synthetic, simulated, or AI-generated data goes ONLY in data/generated/.
- Never write to data/raw/.
- If an input file is missing, STOP and tell me. Do not create data to get past an error.
- Do not commit. Do not modify uv.lock. I do that.
- Do not add or drop model terms, predictors, or exclusions without asking.
  This analysis is preregistered.
- Write the test first, with simulated data where the true parameters are known.

## Data facts you cannot infer
<!-- This section prevents wrong-but-plausible results. Be specific. -->
- Confidence scale is 1-100 (continuous VAS), NOT 1-4.
- Subjects 07, 14, 22 are excluded: incomplete sessions. See NOTES.md.
- `trial` is 1-indexed in the behavioural files, 0-indexed in the event files.
- Condition 3 is the AUDITORY CONTROL, not a cardiac condition.
- RTs are in milliseconds. IBIs are in milliseconds. Heart rate is BPM.
- Missing values are coded -999, not NaN.

## Known traps
<!-- Add a line every time you lose an afternoon to something. -->
- arviz >= 0.18 changed the default HDI probability; we report 94%, set it explicitly.
- The 2024 scanner upgrade changed slice timing. Sessions before 2024-06 need the old
  timing file.

## Cluster (delete if local-only)
This project runs on GenomeDK. NEVER execute computation on the frontend.
Submit with sbatch, or request a node with `srun --pty`.
Always pass `--account ecg_general`. Use the `short` partition for jobs under 12 h.
Results go to /faststorage/project/ecg_general/<project>/, never $HOME.
Before running anything on the cluster, tell me what it will execute and where.

## Style
- Type hints on public functions. Docstrings with units.
- No bare except. No silent NaN handling — assert or raise.
- Assertions at the top of every processing step: subject count, value ranges,
  duplicates, missingness.
```
