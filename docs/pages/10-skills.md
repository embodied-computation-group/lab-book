# 10. Skills

[← Notebooks and figures](09-notebooks-and-figures.md) · [Contents](../index.md) · [Next: Cluster work →](11-hpc.md)

---

Skills are optional. Start with ordinary prompts and a short project instruction file.
A skill becomes useful when you want an agent to follow the same procedure across
several tasks or projects.

## What a skill contains

A skill is a folder with a `SKILL.md` instruction file and, optionally, supporting
references or scripts. For example:

```text
~/.claude/skills/genomedk/
├── SKILL.md
├── references/
└── scripts/
```

In Claude Code, a skill can be invoked by name, such as `/genomedk`, or selected by the
agent when its description matches a task. Availability and invocation depend on the
installation; see the [skills documentation](https://code.claude.com/docs/en/skills).

The description helps the agent decide when to load the procedure. Keep general project
facts in `CLAUDE.md` and longer task-specific instructions in the skill.

## Why use one?

A cluster submission procedure can record account settings, output checks and known
failure cases. This gives the agent a concrete starting point instead of having to
infer local practice.

Skills guide behaviour; they do not guarantee it. Check the proposed commands and output.
When a procedure changes, update the shared source and make sure collaborators update
their installed copies.

## The lab's skills

The private [ai-skills repository](https://github.com/embodied-computation-group/ai-skills)
contains lab procedures. Lab members already belong to the GitHub organisation;
sign in with your lab-linked account and follow its README for installation.
The repository is maintained separately from this book.

| Skill | Purpose |
|---|---|
| `genomedk` | Cluster job preparation and verification; see [page 12](12-genomedk-skill.md). |
| `interoception-hierarchical-models` | Lab guidance on hierarchical psychophysics and metacognition analyses. |

Use a modelling skill alongside a scientist-checked model specification. It does not
replace the equations or your choice of analysis.

Micah's `interview` procedure helps clarify an underspecified task. Check whether it is
available in your installation. You can get started without it:

```text
Help me clarify this analysis before writing code.
Ask about the scientific question, inputs, assumptions and intended outputs.
```

## Write a skill when you need it

Save a procedure when you expect to repeat it. Describe when it applies, the steps,
what to check and what to do when a step fails. Include a concrete failure example.

Try it on a small case before sharing it. Commit the source with a description of the
change, and use the lab repository's contribution instructions for any generated copies.

External collections, such as
[Crawfurd's academic research skills](https://lcrawfurd.github.io/claude-skills/),
include review and reproducibility procedures. Read what a skill does before installing
it, and check the findings it produces as you would any other agent output.

---

[← Notebooks and figures](09-notebooks-and-figures.md) · [Contents](../index.md) · [Next: Cluster work →](11-hpc.md)
