# 12. Tips and tricks

[← Human-subject data](11-data-and-ethics.md) · [Contents](../README.md) · [Next: Resources →](13-resources.md)

---

Grab bag. Add yours.

## Context hygiene

- **`/clear` is underused.** A stale context is worse than an empty one. Between tasks,
  clear it. It costs you nothing except re-stating the task in one line.
- **The signal that you should have cleared already:** it re-reads files it read twenty
  minutes ago, forgets a convention it followed earlier, or starts summarising instead of
  doing. Clear and restate.
- **`@file` beats "look around".** Pointing at three files is faster and safer than letting
  it explore, and it keeps a lot of junk out of the window.
- **Long outputs are context poison.** Do not paste a 4000-line log. Save it and point at
  it, or `grep` it first — `tail -50 slurm-*.out` answers most questions.

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
| **Plan, one, all** | Plan it, run one case, verify the output has real content, then run everything. Essential on the cluster (page 10). |
| **Methods diff** | Point it at your methods section and your pipeline, ask for discrepancies. Before every submission. |
| **Explain this legacy script** | Best-value use of an agent on an inherited project, and it costs nothing. |

## Skills and slash commands

If you have explained the same procedure twice, make it a skill. `~/.claude/skills/<name>/SKILL.md`,
description in the frontmatter, and it loads on demand — see page 10 for how the lab uses
this for GenomeDK. `/skill-creator` writes them for you.

Worth installing from outside the lab:

- [Crawfurd's academic research skills](https://lcrawfurd.github.io/claude-skills/) —
  **Referee 2** is a reproducibility audit that runs five parallel checks over your
  replication package. Run it on your own repo before submitting. Also a pre-submission
  reviewer and a Tufte figure critic.

## MCP servers

MCP servers give the agent tools beyond your filesystem. Configured ones worth knowing:

- **Zotero** — search the library, pull full text, read annotations, add by DOI. Good for
  "find the papers in my library that used this measure" and for checking a citation
  actually says what you claim.
- **NotebookLM** — build a notebook from sources and query across them. Useful for a
  literature pass over a stack of PDFs.
- **Gmail / Calendar / Drive** — admin work, not analysis.

Do not point an MCP server at anything containing participant data (page 11).

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

[← Human-subject data](11-data-and-ethics.md) · [Contents](../README.md) · [Next: Resources →](13-resources.md)
