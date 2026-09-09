# Agents in the Lab

A practical lab book for PhD students using AI agents to write scientific code.
Start with a small dataset, ask a question, and make something you can check.
The examples use Claude Code, but the working habits apply to other agents too.

AI makes it much easier to try an idea, learn an unfamiliar tool or turn a calculation
into a useful script. Have fun with it. Give the agent good context, commit often, and
do not be afraid to restart when an approach is going nowhere.

## Start small

The [lab-data tutorial](pages/lab-data-tutorial.md) takes you through importing, checking,
plotting and analysing the internal `gender_intero` dataset. For a quick start without
research-data access, use the [fictional CSV warm-up](pages/first-exercise.md). You need basic Python and a terminal; the agent can help with the
mechanics. No cluster, custom skills or workflow framework is required.

Read [Start here](pages/01-start-here.md), get [set up](pages/03-setup.md), and try the
tutorial. Use the other pages as questions arise.

## The working cycle

```text
Give context → agree a plan → let the agent work → check the result
     ↑                                                 │
     └──────── save useful progress in Git ──────────────┘
```

You provide the scientific question, definitions and expected behaviour. The agent helps
build the code and pipeline. Save small, descriptive commits throughout, including
commits made by the agent. A fresh session can pick up from the files and history.

[The workflow page](pages/06-the-loop.md) gives example prompts.
[Working with context](pages/02-context.md) shows how a model specification can guide
implementation.

## Choose how far to go

| Stage | Read and try | What you should be able to do |
|---|---|---|
| First session | [Start here](pages/01-start-here.md), [setup](pages/03-setup.md), [lab tutorial](pages/lab-data-tutorial.md) or [quick warm-up](pages/first-exercise.md) | Import a table, check it, make a plot, answer a small question and save commits. |
| Everyday work | [Context](pages/02-context.md), [layout and Git](pages/04-project-layout.md), [project instructions](pages/05-claude-md.md), [the loop](pages/06-the-loop.md), [practical tips](pages/14-tips-and-tricks.md) | Give a useful brief, work in small steps and recover from an unhelpful session. |
| Results you will rely on | [Verification](pages/07-verification.md), [reproducibility](pages/08-reproducibility.md), [figures](pages/09-notebooks-and-figures.md) | Explain your checks and reproduce a result from saved files. |
| Optional extensions | [Skills](pages/10-skills.md), [cluster work](pages/11-hpc.md), [genomedk example](pages/12-genomedk-skill.md) | Reuse procedures or scale an analysis when your project needs it. |

Before working with participant files, read [Human-subject data](pages/13-data-and-ethics.md).
The internal tutorial uses the lab's approved access arrangements; the warm-up uses
fictional observations.

## The references behind the book

Our main references are
[Ten Simple Rules for AI-Assisted Coding in Science](https://arxiv.org/abs/2510.22254)
and Russ Poldrack's [Coding with AI](https://bettercode-book.org/book-ai-coding-assistants.html).
They provide the scientific computing principles; this book helps you practise them in
small steps. You do not need to adopt every tool or advanced practice at once.

[Resources](pages/15-resources.md) suggests where to read further.
[Contributing](pages/16-contributing.md) explains how to improve the book.

## Copyable starters

- [Fictional trial data](starters/practice-trials.csv) for the first exercise.
- [Project instructions](starters/CLAUDE.md) and [project layout](starters/project-tree.md).
- [Rescorla–Wagner model specification](starters/rescorla-wagner-spec.md) for a later modelling task.
- [Verification checklist](starters/verification-checklist.md) for results you will rely on.
- [Git ignore rules](starters/gitignore).
- [Snakefile](starters/Snakefile), an optional advanced pipeline example.
