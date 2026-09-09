# 3. Project layout

[← Setup](02-setup.md) · [Contents](../index.md) · [Next: Writing a CLAUDE.md →](04-claude-md.md)

---

Lab standard. Use it unless you have a reason not to, and if you do, write the reason in
your `CLAUDE.md`.

```
project/
├── CLAUDE.md              # rules for the agent (page 4)
├── README.md              # what this is, how to run it
├── pyproject.toml         # deps, pinned
├── uv.lock                # committed
├── Snakefile              # the pipeline (page 7)
├── data/
│   ├── raw/               # READ-ONLY. Never written to. Never by an agent.
│   ├── processed/         # derived from raw by code in src/
│   └── generated/         # anything an AI produced. Quarantine.
├── src/                   # importable, tested functions
├── scripts/               # thin entry points that call src/
├── notebooks/             # .qmd or .py, not .ipynb (page 8)
├── results/
│   ├── figures/
│   └── tables/
└── tests/
```

## The three rules

**1. `data/raw/` is read-only.**

Make it actually read-only, not aspirationally:

```bash
chmod -R a-w data/raw          # macOS / Linux / cluster
icacls data\raw /deny "%USERNAME%":(W) /T   # Windows
```

An agent that can write to your raw data can destroy an irreplaceable scanning session
while trying to be helpful. This has happened to people. Take the thirty seconds.

**2. `data/generated/` exists and is separate.**

This is the one directory that is new since agents. Anything an AI produced — synthetic
data for testing, an imputed column, a simulated dataset, a mock file it made to get a
script running — goes here and nowhere else.

The failure mode this prevents is real and it is bad: the agent needs test data, invents
some, writes it into `data/processed/`, and six weeks later it is in your figure. Keeping
it physically separate means the question "is any of this made up" has a one-line answer.

Add to `CLAUDE.md`, verbatim:

```
Synthetic, simulated, or AI-generated data goes ONLY in data/generated/.
Never write to data/raw/. Never write generated values into data/processed/.
```

**3. `src/` holds functions, `scripts/` holds entry points.**

Anything you would want to test lives in `src/` and gets imported. Scripts should be short
enough to read in one screen. Agents write enormous monolithic scripts by default; ask for
this split explicitly and it will comply.

## Git hygiene with an agent

Agents generate dead code fast — abandoned helpers, superseded scripts, files from a plan
that changed halfway through. Git is how you see it.

- **Branch per task.** `git switch -c hrd-slope-fix`. Never let an agent work on `main`.
- **Commit before you let it loose,** so `git diff` shows exactly what it did.
- **Commit at every working state,** not at the end of the session. Small commits let you
  bisect when the pipeline breaks two hours later.
- **Read the diff.** Not the summary the agent gives you. The diff.
- **Delete aggressively.** If you cannot say what a file is for, it goes. Tests make this
  safe, which is one more reason to have them.

Data does not go in git. See [`starters/gitignore`](../starters/gitignore). For sharing
data use the lab's usual channels; for versioning large derived files, ask before adding
`git-lfs` or DataLad to a project.

---

[← Setup](02-setup.md) · [Contents](../index.md) · [Next: Writing a CLAUDE.md →](04-claude-md.md)
