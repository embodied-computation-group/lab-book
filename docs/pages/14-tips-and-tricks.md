# 14. Tips and tricks

[← Human-subject data](13-data-and-ethics.md) · [Contents](../index.md) · [Next: Resources →](15-resources.md)

---

Grab bag. Add yours.

## Context

Has its own page: [page 2](02-context.md). The two-line version: `/clear` between tasks,
`@point` at files rather than letting it browse, and never paste a long log —
`tail -50 slurm-*.out` answers most questions.

## Prompting that works for analysis

- **Say what "correct" means.** "Fit a psychometric function" is weak. "Fit a cumulative
  normal by maximum likelihood, return threshold and slope with 95% CIs, and include a
  test recovering known parameters from simulated data" is a specification.
- **Give it the shape of your data**, or point at a `head -5`. Half of all wrong analyses
  start with a wrong assumption about columns.
- **Ask for the failure modes.** "What would make this give a wrong answer?" is the single
  most useful question you can ask about code you did not write.
- **Ask it to disagree.** "What is wrong with this approach?" gets you real objections;
  "does this look right?" gets you agreement.
- **When it is confidently wrong, do not argue — restate.** Correcting the same
  misunderstanding three times in one context rarely works. `/clear` and give a better
  brief.

## Useful patterns

| Pattern | What it is |
|---|---|
| **Writer / Reviewer** | Two terminals. One writes, the other reviews with a clean context. The reviewer catches things the writer structurally cannot. |
| **Test first** | Ask for the test and the simulator before the implementation. Better brief, and the code cannot be tuned to a test that already passes. |
| **Plan, one, all** | Plan it, run one case, verify the output has real content, then run everything. Essential on the cluster (page 12). |
| **Methods diff** | Point it at your methods section and your pipeline, ask for discrepancies. Before every submission. |
| **Explain this legacy script** | Best-value use of an agent on an inherited project, and it costs nothing. |

## Skills

Have their own page: [page 10](10-skills.md). Three tips that belong here anyway:

- **`/interview` before Plan Mode** when you cannot state the task in two lines. It asks
  why before what, and it is the cheapest way to avoid building the wrong thing well.
- **The second time you explain a procedure, make it a skill.** `/skill-creator` writes
  them; the lab's live in `ai-skills`.
- **[Referee 2](https://lcrawfurd.github.io/claude-skills/)** on your own replication
  package before you submit, not after a reviewer asks.

## MCP servers

MCP servers give the agent tools beyond your filesystem. Configured ones worth knowing:

- **Zotero** — search the library, pull full text, read annotations, add by DOI. Good for
  "find the papers in my library that used this measure" and for checking a citation
  actually says what you claim.
- **NotebookLM** — build a notebook from sources and query across them. Useful for a
  literature pass over a stack of PDFs.
- **Gmail / Calendar / Drive** — admin work, not analysis.

Do not point an MCP server at anything containing participant data (page 13).

## Small things that save time

- **Voice input** for dictating plans. Plans are prose, and prose is faster spoken. Good
  match for Plan Mode.
- **`!` prefix** runs a command yourself with the output landing in the conversation.
  Perfect for interactive things an agent cannot do — `ssh` with 2FA, `gcloud auth login`.
- **`Esc Esc`** rewinds the conversation. Better than trying to talk it out of a hole.
- **Ask for a commit message,** not a commit. You keep the veto.
- **`snakemake -n` before anything.** Applies to agents twice over.
- **Keep a `NOTES.md`** in the project. When you correct the agent about something
  structural, that line belongs in `CLAUDE.md`; when you learn something about the *data*,
  it belongs in `NOTES.md` and often in the paper.

## Things that waste tokens and time

- Six parallel subagents on one problem. You will review six half-finished things.
- Letting it "clean up the codebase" unprompted. Scope it or it will refactor working code.
- Asking it to fix a failing test without looking yourself. It will sometimes delete the
  test. Read the diff.
- Long autonomous runs with no way to check progress. Give it a test command or it cannot
  tell whether it is done.

---

[← Human-subject data](13-data-and-ethics.md) · [Contents](../index.md) · [Next: Resources →](15-resources.md)
