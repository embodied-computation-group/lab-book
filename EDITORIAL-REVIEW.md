# Lab book review

Reviewed against the intended audience: PhD students, often novice coders, learning to
use agents for scientific analysis.

## Assessment

The original book had useful examples and practical lab knowledge, but its structure
made advanced tooling appear necessary before a student could begin. It worked better
as an experienced user's reference than as an introduction. Repeated slogans and absolute
claims also obscured which practices were essential, optional or matters of judgement.

The revised book is designed as a teaching resource: an accessible task, copyable prompts,
visible checkpoints, a small expected-answer test and a chance to explain the result.
Whether it teaches effectively still needs to be checked with students.

## Changes made

- Staged the reading paths: start and try, everyday workflow, results to rely on,
  optional extensions.
- Added an internal gender_intero tutorial covering download, context, import, QC,
  plotting, paired descriptive analysis and reproduction. Each step has an example
  prompt and a checkpoint. The source is pinned; participant data and findings are not
  copied into this repository.
- Added a short fictional CSV warm-up for a first session without research-data access.
- Made the scientist's role in supplying context explicit, with a Rescorla–Wagner
  specification containing equations, timing conventions and hand-worked checks.
- Made frequent, focused commits part of the cycle, including commits made by the agent.
  Explained how the history supports PR review, diagnosis and recovery.
- Introduced pipeline as a sequence of analysis steps. A documented script is sufficient
  to start; Snakemake is optional and explained before use.
- Removed blanket notebook restrictions, unsupported guarantees about tests and fresh
  reviewers, arbitrary checklist scores, and repeated admonitions.
- Corrected conflicting data-access language and removed advice to ask for GitHub
  organisation access that lab members already have.
- Kept Ten Simple Rules and Russ Poldrack's AI chapter as the main references, while
  separating their principles from optional tooling and local choices.

## Remaining teaching work

Try the internal tutorial with one or two novice students. Observe where they need help,
whether they can explain participant weighting, and whether they can use a commit or
fresh session to recover from a problem. Ask them to bring a plot and a brief explanation,
not a fully engineered project.

The book primarily teaches coding and analysis with agents. Literature synthesis,
experimental design and other scientific uses would need separate examples if the
scope expands.

Cluster timings and local software notes remain recorded lab observations, not a fresh
audit of the live cluster. The optional Snakefile is labelled as an incomplete skeleton,
not a runnable beginner exercise.

## Verification of the edit

The strict MkDocs build passed, including navigation and internal-link checks. The
fictional CSV's expected mean and the model example's numerical checks were recalculated.
The internal dataset's schema, categories and value ranges were checked at the pinned
commit without copying participant rows into this repository. The tutorial is a guided
agent exercise, not a supplied, fully executed analysis implementation; a student pilot
is still needed to assess its pacing and clarity.
