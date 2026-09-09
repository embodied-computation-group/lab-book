# 13. Resources

[← Tips and tricks](12-tips-and-tricks.md) · [Contents](../README.md) · [Next: Contributing →](14-contributing.md)

---

Annotated, and ordered by value per hour of your time. Every link here was opened and
checked on 2026-09-09.

## Read these two first

**[Better Code, Better Science](https://bettercode-book.org/)** — Russ Poldrack (Stanford).
Free online, CC BY-NC-ND, 12 chapters. The closest thing to a textbook for this whole
subject, written by a neuroimager, so the examples land. Ch. 5 is the AI chapter, but the
reproducibility content is in Ch. 4 (testing), 8 (workflow management), 9 (validating
scientific software), 11 (HPC), 12 (sharing research objects). The book's own code was
written through human–AI collaboration, so the advice is lived rather than speculative.
*Note the URL has moved twice; older `poldrack.github.io/BetterCodeBetterScience` links
still circulate.*

**[Ten Simple Rules for AI-Assisted Coding in Science](https://arxiv.org/abs/2510.22254)** —
Bridgeford, Campbell, Chen, Lin, Ritz, Vandekerckhove & Poldrack. Published in *PLOS
Computational Biology*, 27 July 2026. Twenty minutes. Organised around problem
preparation, managing context and interaction, testing and validation, and code quality.
**This is the one to cite** when a reviewer asks how your analysis code was produced, and
the one to send to a new student in week one.

## The best practitioner write-up

**[Claude Code for Scientists](https://www.neuroai.science/p/claude-code-for-scientists)** —
Patrick Mineault. Much of pages 3, 5 and 8 of this book comes from here: the
Plan–Execute–Evaluate loop, the `data/generated/` quarantine, the argument for dropping
`.ipynb`, and the observation that code is generated faster than it can be verified. Also
the warning worth repeating to supervisors: junior researchers often lack the metacognition
to notice when an agent is wrong.

**[The Good Research Code Handbook](https://goodresearch.dev/)** — same author, pre-dates
agents entirely, and is still the best short introduction to structuring a research
codebase. Everything in it got *more* important, not less. His
`true-neutral-cookiecutter` template on GitHub is a reasonable project skeleton.

## Official Anthropic material

- **[Best practices for Claude Code](https://code.claude.com/docs/en/best-practices)** —
  the docs page. Organised around the real constraint: context fills fast and quality
  degrades as it does. Covers subagents and the Writer/Reviewer pattern.
- **[Claude Code 101](https://anthropic.skilljar.com/claude-code-101)** — free, install to
  customisation. Send new students here.
- **[Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action)** — free,
  and the more useful one once you are past the basics: steering long sessions, rules the
  agent cannot skip, verifying results you did not watch happen.
- **[How Claude Code is used in practice](https://www.anthropic.com/research/claude-code-expertise)** —
  Anthropic's own usage research. Useful for calibrating what to delegate.
- **[Claude Team plan for scientists](https://claude.com/programs/team-plan-for-scientists)** —
  the seat programme. Numbers on page 2.

## Installable tooling

- **[Claude Code Skills for Academic Research](https://lcrawfurd.github.io/claude-skills/)** —
  Lee Crawfurd. Built for economists; three of the six transfer to any quantitative field.
  **Referee 2** is a computational reproducibility audit run as five parallel checks (code,
  cross-language replication, directory and replication package, output automation,
  field-specific stats). **Pre-Submission Review** runs six parallel agents over spelling,
  internal consistency, unsupported claims, mathematics, tables and figures. **Tufte
  Visualization** critiques figures. Install by copying the markdown into `~/.claude/skills/`.

## Neuroimaging specifically

Thin, honestly. There is no good BIDS/fMRI-specific agentic coding tutorial as of
September 2026. Poldrack's book is the closest thing, since he writes for this audience.

**[NeuroClaw](https://arxiv.org/html/2604.24696v1)** is worth reading for its architecture:
a multi-agent neuroimaging assistant (sMRI/fMRI/dMRI/EEG → BIDS → fMRIPrep, FreeSurfer,
seed connectivity, task GLM) built around checkpointed execution, structured verification,
and audit logging, with pinned environments and Docker.

**Two caveats, stated up front:** it is an unreviewed technical report, and the paper gives
a project homepage but no code release, so **we could not verify the code is actually
obtainable.** Do not plan work around it. It is also model-agnostic rather than a Claude
Code integration. Read it for the checkpoint-plus-audit-log pattern, which is worth
stealing into your own Snakefile regardless.

## Community, treat with care

- **[codewithclaude.net researcher hub](https://codewithclaude.net/start-here/claude-code-for-researchers)** —
  Python and R/tidyverse tracks, a Git guide, a `CLAUDE.md` generator, printable cheat
  sheets. Decent for onboarding. **Its own footer says it is independent and not affiliated
  with or endorsed by Anthropic**, so treat it as community material rather than
  authoritative on how the tool behaves.
- `FlorianBruniaux/claude-code-ultimate-guide` on GitHub — large community guide.
  **Not opened or checked by us.** Listed only so you know it exists.

## Lab tooling

- **[RainCloudPlots](https://github.com/RainCloudPlots/RainCloudPlots)** — ours. If an agent
  starts reinventing a raincloud, stop it and point it here.
- **`genomedk` skill** — page 10.
- **`interoception-hierarchical-models` skill** — HRD and RRST psychophysics and meta-d′.
  Use it instead of asking an agent to write a meta-d′ model from scratch.

---

[← Tips and tricks](12-tips-and-tricks.md) · [Contents](../README.md) · [Next: Contributing →](14-contributing.md)
