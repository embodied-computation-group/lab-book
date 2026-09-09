# 4. Project layout and Git

[← Setup](03-setup.md) · [Contents](../index.md) · [Next: Writing a CLAUDE.md →](05-claude-md.md)

---

A project can start small. You need somewhere for inputs, a script, a short description
of how to run it, and a history of changes.

## A first project

```text
project/
├── README.md              # question and run command
├── CLAUDE.md              # instructions for the agent
├── pyproject.toml         # Python dependencies
├── uv.lock                # saved dependency versions
├── .gitignore             # files Git should leave untracked
├── data/
│   └── generated/         # fictional practice observations
├── scripts/
│   └── analyse.py
├── results/
└── tests/
```

Ask the agent to create only the folders you need. As calculations grow, move reusable
functions into `src/` and import them from scripts. The
[starter layout](../starters/project-tree.md) includes an optional larger structure.

## Keep observations and test data distinct

For research projects, preserve original observations in read-only storage. Derived
data belongs in `data/processed/`; fictional test observations and simulations belong
in `data/generated/`. Label simulations so they cannot be mistaken for collected data.

An output calculated from real data is a derived result even if an agent helped write
the code. A planned imputation method also needs documentation; invented replacement
values must not be used to bypass a missing input.

Filesystem permissions protect raw files from accidental writes. They do not prevent
reading or replace backups. [Page 13](13-data-and-ethics.md) explains agent access.
A `.gitignore` file controls what Git tracks, not what the agent can read.

## Git commits during the work

A **commit** saves a named version of selected files. Frequent commits let you see what
changed, compare a working version with a broken one, and recover earlier work.
A focused history also helps an agent diagnose regressions and review a **pull request**
(PR), the proposed set of changes you ask someone else to review.

Agents can make commits. Tell them to keep each commit about one change and describe
what it does. For an analysis task, useful checkpoints might be:

```text
Document reaction-time units and participant weighting
Add tests for participant means and duplicate rows
Implement CSV loading and participant means
Add a plot of participant and group means
```

Save the starting version before a substantial change. Commit tests once you have checked
that they express the intended behaviour; a test-first commit can have expected failures.
Commit the implementation when the relevant checks pass, then save later improvements
separately. Record the checks in commit messages when useful.

You can ask:

```text
Work in small steps and make a descriptive Git commit after each coherent
change. Check the diff and stage only files for that change.
Run the relevant checks and record their outcome.
Do not include research data, credentials or unrelated edits.
```

This history makes it easier to investigate a regression than one large "update analysis"
commit. Commits are local: publishing them with a push is a separate action.

## A few Git commands to learn

Run these inside an existing repository:

```bash
git status
git diff
git log --oneline -10
```

They show changed files, edits to tracked files, and recent commits. Newly created files
need to be opened separately until they are staged.

Before a substantial task, make a branch:

```bash
git switch -c participant-means
```

A **branch** lets you develop a change separately from the main version. If your practice
folder is not a repository yet, ask the agent to initialise Git, add a suitable
`.gitignore` and make the first commit. Review which files it includes.

## When you need to restart

First save useful changes and a short note of what worked, what failed and what to try
next. Then clear the conversation and point the new session to those files.

If a code change caused a problem, ask the agent to compare it with the last working
commit. It can propose a new commit that reverses the relevant change. You do not need
to erase the whole branch or discard unrelated work.

In [Poldrack's version-control discussion](https://bettercode-book.org/book-ai-coding-assistants.html#version-control-for-agentic-workflows),
saving progress before clearing context is part of the workflow. The aim is to make
experimentation recoverable.

---

[← Setup](03-setup.md) · [Contents](../index.md) · [Next: Writing a CLAUDE.md →](05-claude-md.md)
