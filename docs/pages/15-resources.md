# 15. Resources

[← Tips and tricks](14-tips-and-tricks.md) · [Contents](../index.md) · [Next: Contributing →](16-contributing.md)

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
Patrick Mineault. Much of pages 4, 6 and 9 of this book comes from here: the
Plan–Execute–Evaluate loop our Context → Plan → Execute → Review is built on, the
`data/generated/` quarantine, the argument for dropping
`.ipynb`, and the observation that code is generated faster than it can be verified. Also
the warning worth repeating to supervisors: junior researchers often lack the metacognition
to notice when an agent is wrong.

**[The Good Research Code Handbook](https://goodresearch.dev/)** — same author, pre-dates
agents entirely, and is still the best short introduction to structuring a research
codebase. Everything in it got *more* important, not less. His
`true-neutral-cookiecutter` template on GitHub is a reasonable project skeleton.

## On context management

The evidence behind [page 2](02-context.md):

- **[Poldrack, *Better Code, Better Science*, ch. 5](https://bettercode-book.org/book-ai-coding-assistants.html)** —
  the chapter on AI coding assistants. Context rot, the constitution/memory-file
  distinction, clear-versus-compact, task sizing. The clearest single treatment written
  for scientists.
- **[Hong, Troynikov & Huber, *Context Rot*](https://research.trychroma.com/context-rot)** —
  Chroma technical report, July 2025. Eighteen models, including Claude 4, GPT-4.1 and
  Gemini 2.5: performance grows less reliable as input length grows, even on simple tasks,
  and semantically similar distractors make it worse. The measurement behind the folklore.
  Replication toolkit on [GitHub](https://github.com/chroma-core/context-rot).
- **[Anthropic, *Effective context engineering for AI agents*](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)** —
  the "attention budget" framing, just-in-time retrieval, compaction, structured
  note-taking, and sub-agents as context isolation. Written for people building agents,
  but every practice maps onto using one.

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
  the seat programme. Numbers on page 3.

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
- **[`ai-skills`](https://github.com/embodied-computation-group/ai-skills)** — the lab's
  skills repo (private; ask for access). `genomedk` and `interoception-hierarchical-models`,
  with generated ports for ChatGPT, GitHub Copilot and Microsoft 365 Copilot, plus pointers
  to the external collections we install as plugins. Page 10 explains skills; page 12 is
  the `genomedk` worked example.
- **`/interview`** — a discovery conversation before anything gets built. A personal skill
  of Micah's for now, being added to `ai-skills`. Page 10.

---

[← Tips and tricks](14-tips-and-tricks.md) · [Contents](../index.md) · [Next: Contributing →](16-contributing.md)
