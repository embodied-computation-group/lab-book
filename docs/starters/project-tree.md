# Example project layouts

Use only the folders you need. See [page 4](../pages/04-project-layout.md) for Git and data
organisation.

## Start small

```text
project/
├── README.md              # question and run command
├── CLAUDE.md              # agent instructions
├── pyproject.toml
├── uv.lock
├── .gitignore
├── data/
│   └── generated/         # fictional practice data
├── scripts/
│   └── analyse.py
├── results/
└── tests/
```

Ask the agent to create this structure in your practice project. Copy the text inside
the [instruction template](CLAUDE.md), rather than its explanatory wrapper.
The [CSV for the first exercise](practice-trials.csv) contains fictional observations.

## Add structure as the project grows

```text
project/
├── MODEL.md               # scientist-checked equations and conventions
├── TASKS.md               # current work and next steps
├── VERIFICATION.md        # checks and evidence
├── src/                   # reusable functions imported by scripts
├── notebooks/             # exploration and reports
├── logs/                  # run records, reviewed before sharing
└── Snakefile              # optional: dependencies between pipeline steps
```

Research projects may also need read-only raw storage and a processed-data directory,
with access arranged under [page 13](../pages/13-data-and-ethics.md).

A Snakefile is optional. Start with a script and documented run command; see
[page 8](../pages/08-reproducibility.md) when you need more automation.
