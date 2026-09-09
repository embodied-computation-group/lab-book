# 15. Resources

[← Practical tips](14-tips-and-tricks.md) · [Contents](../index.md) · [Next: Contributing →](16-contributing.md)

---

Start with the two references below. The rest is there for questions that arise as you
work; it is not a prerequisite reading list.

## Our main references

[Ten Simple Rules for AI-Assisted Coding in Science](https://arxiv.org/abs/2510.22254),
by Bridgeford and colleagues, is the starting point for this book. Its ten rules cover
preparation, interaction, testing, review and focused improvement. Read it early, then
return to it after a few sessions with an agent. The paper links to companion worked
examples. It was published in *PLOS Computational Biology* in July 2026.

[Russ Poldrack, Coding with AI](https://bettercode-book.org/book-ai-coding-assistants.html),
chapter 5 of *Better Code, Better Science*, develops the practical workflow: context
files, test-first development, recognising failed approaches and using version control.
Read the sections relevant to your current task. The chapter is being revised, so
specific tool details may change.

For this lab book, the progression is deliberate: first make a small analysis work, then
learn to check and maintain increasingly complex analyses. You do not need all the
infrastructure in these references on day one.

## Learning the programming basics

The rest of [Better Code, Better Science](https://bettercode-book.org/) covers software
testing, project structure, workflows and scientific validation.

[The Good Research Code Handbook](https://goodresearch.dev/) is Patrick Mineault's guide
to organising research code. His
[Claude Code for Scientists](https://www.neuroai.science/p/claude-code-for-scientists)
also informed the original lab book's workflow and treatment of generated test data.
These are supplementary reading alongside our main references.

## Tool documentation

- [Claude Code installation](https://code.claude.com/docs/en/installation):
  current setup instructions.
- [Claude Code best practices](https://code.claude.com/docs/en/best-practices):
  context, planning and review workflows.
- [Claude Code permissions](https://code.claude.com/docs/en/permissions):
  what access settings control.
- [Claude Code skills](https://code.claude.com/docs/en/skills):
  writing and loading reusable procedures.
- [uv projects](https://docs.astral.sh/uv/guides/projects/):
  Python environments and dependency records.
- [Snakemake tutorial](https://snakemake.readthedocs.io/en/stable/tutorial/basics.html):
  optional reading once you need to coordinate several analysis steps.

For evidence about context length, see
[Chroma's Context Rot report](https://research.trychroma.com/context-rot).
Its experiments are useful background, not a universal token limit for your sessions.

## Lab resources and optional tools

Lab members can access [ai-skills](https://github.com/embodied-computation-group/ai-skills)
through the lab's GitHub organisation. Follow its README for current installation
instructions; [page 10](10-skills.md) introduces the idea.

[GenomeDK documentation](https://genome.au.dk/docs/) is the reference for cluster work.
Pages [11](11-hpc.md) and [12](12-genomedk-skill.md) cover lab examples and known issues.

[RainCloudPlots](https://github.com/RainCloudPlots/RainCloudPlots) is the lab's plotting
project. [Crawfurd's academic research skills](https://lcrawfurd.github.io/claude-skills/)
contains optional review procedures. Inspect any procedure before adding it to your
workflow.

---

[← Practical tips](14-tips-and-tricks.md) · [Contents](../index.md) · [Next: Contributing →](16-contributing.md)
