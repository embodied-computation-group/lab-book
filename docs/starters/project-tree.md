# Standard project layout

The lab default. Reasoning on [page 4](../pages/04-project-layout.md).

```
project/
├── CLAUDE.md                  # rules for the agent — committed, lab knowledge
├── README.md                  # what this is + the one command that reproduces it
├── NOTES.md                   # what you learned about the DATA (often ends up in the paper)
├── VERIFICATION.md            # filled-in checklist
├── pyproject.toml
├── uv.lock                    # committed
├── config.yaml                # subjects, seed, interpreter path
├── Snakefile                  # the pipeline — every figure and table is a rule
├── .gitignore
├── .claude/
│   ├── settings.json          # permission denies for sensitive paths (page 13)
│   └── agents/                # project-specific subagents, e.g. a read-only reviewer
├── data/
│   ├── raw/                   # READ-ONLY. chmod a-w. Never written by anything.
│   ├── processed/             # derived from raw by src/ only
│   └── generated/             # AI-generated / simulated. Quarantine. Never mixed in.
├── src/
│   └── <package>/             # importable, tested functions
│       ├── __init__.py
│       ├── io.py
│       ├── preprocess.py
│       └── models.py
├── scripts/                   # thin CLI entry points that call src/
│   ├── preprocess.py
│   ├── fit_subject.py
│   └── make_figures.py
├── notebooks/                 # .qmd or marimo .py. Not .ipynb.
├── results/
│   ├── figures/               # only Snakemake writes here
│   ├── tables/
│   └── provenance.txt
├── logs/
└── tests/
    ├── test_preprocess.py
    └── test_models.py         # includes recovery-from-simulation tests
```

## Making it

```bash
mkdir -p data/{raw,processed,generated} src scripts notebooks \
         results/{figures,tables} logs tests .claude/agents
touch data/raw/.gitkeep data/processed/.gitkeep data/generated/.gitkeep
cp <labbook>/starters/gitignore .gitignore
cp <labbook>/starters/CLAUDE.md CLAUDE.md      # then EDIT the data facts section
cp <labbook>/starters/Snakefile Snakefile
cp <labbook>/starters/verification-checklist.md VERIFICATION.md
uv init && uv venv

# make raw data actually read-only, not aspirationally
chmod -R a-w data/raw                                    # mac/linux/cluster
# icacls data\raw /deny "%USERNAME%":(W) /T              # windows
```

## The three things that matter if you deviate

Change the rest freely, but keep these, and if you drop one, write the reason in
`CLAUDE.md`:

1. **`data/raw/` is read-only**, enforced at the filesystem level.
2. **`data/generated/` exists and nothing else contains AI-generated values.**
3. **Every paper figure comes from a Snakemake rule.**
