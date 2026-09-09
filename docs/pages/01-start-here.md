# 1. Start here

[Contents](../index.md) · [Next: Working with context →](02-context.md)

---

An AI coding agent can read files, edit code and run commands. In a research project,
that makes it useful for explaining an inherited script, implementing an analysis you
have specified, or checking whether code matches your methods section. It can also
produce a plausible result from the wrong assumptions.

This book teaches you to work with an agent while taking responsibility for the
scientific decisions. Examples use Claude Code and the lab's Python tools. The habits
apply more widely, although commands and settings differ between tools. The focus is
scientific coding and analysis, rather than every use of AI in research.

Start with something you are curious about. Make a plot, try a small change and see what
happens. Commit often so you can return to a working version. You do not need an elaborate
project structure to begin.

Our main references are Bridgeford and colleagues'
[Ten Simple Rules for AI-Assisted Coding in Science](https://arxiv.org/abs/2510.22254)
and Russ Poldrack's [chapter on coding with AI](https://bettercode-book.org/book-ai-coding-assistants.html).
Read them alongside the practical work here. Lab conventions, such as directory names
and cluster settings, are our implementation choices.

## What you will learn

As you work through the tutorials and return to the core pages, you will learn to:

- turn a scientific question into a small task with explicit assumptions and outputs;
- give an agent useful context without exposing restricted data;
- identify scientific decisions in a proposed plan;
- check a result against a known answer and detect a deliberately introduced error;
- save small, descriptive commits, including commits made by the agent;
- leave code, checks and instructions another researcher can run.

You need basic Python, a terminal, and enough Git to inspect changes. If those are new to
you, work with a lab mate and use the introductory material on [page 15](15-resources.md).

## The workflow

```
CONTEXT → PLAN → EXECUTE → REVIEW
   ↑                        │
   └────────────────────────┘
```

**Context.** State the question, relevant files, data definitions and constraints.
Before granting access to research files, read [the data guidance](13-data-and-ethics.md).

**Plan.** Write down your proposed calculation, then ask the agent to develop a plan.
Check what it will estimate, which observations it will include, and how it will test
the result. For a small, well-defined edit, a sentence may be enough.

**Execute.** Let the agent implement the agreed task in small steps and commit useful
progress. Inspect the first changes and interrupt if it makes an unexpected assumption.

**Review.** Inspect the changes, run the tests and compare the output with an independent
calculation or expected result. A fresh agent session can help find mistakes, but its
agreement does not establish that an analysis is correct.

[Page 6](06-the-loop.md) gives prompts for each step. If a session gets stuck, save what
is useful and restart from the project files. Restarting is part of the process.

## Choose a task you can judge

Start with a function, figure or calculation whose behaviour you understand. Give the
agent a completion check it can run, so it can test and revise its own implementation.

For unfamiliar methods, ask for explanations and original sources before implementation.
Read those sources and discuss consequential choices with your supervisor. Extra context
alone does not resolve statistical uncertainty. Trying additional model specifications
needs a scientific rationale and a record of which analyses were planned or exploratory.

Learning to use agents also means continuing to learn programming and methods. Predict
what a function will return, explain a test, and occasionally implement a small calculation
yourself. These give you ways to judge the work you delegate.

## Choose a first session

The [lab tutorial](lab-data-tutorial.md) uses the internal `gender_intero` dataset to
practise import, quality checks, plotting and a descriptive analysis. It includes prompts,
commit checkpoints and a small known-answer test.

For a shorter exercise without research-data access, try the
[fictional CSV warm-up](first-exercise.md). At your next supervision meeting, bring a plot,
your Git history and one decision you had to make.

---

[Contents](../index.md) · [Next: Working with context →](02-context.md)
