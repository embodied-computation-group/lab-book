# 3. Setup

[← Working with context](02-context.md) · [Contents](../index.md) · [Next: Project layout →](04-project-layout.md)

---

## Install

Follow the [official installation guide](https://code.claude.com/docs/en/installation)
for your operating system, then open a terminal in your project and run `claude`.
The native installer is the recommended route. If you already use npm, the guide also
covers that installation method.

First run walks you through login. Run `claude` from inside a project directory — it takes
the current directory as its working root and reads any `CLAUDE.md` it finds there.

## Plans and seats

Ask Micah before buying a subscription: the lab may already have seats. Check the
[scientists programme](https://claude.com/programs/team-plan-for-scientists) for current
eligibility and terms. Prices and usage limits change, so they are not reproduced here.

## Python

Lab members use macOS, Windows and Linux, including the Cybertron server. There is no
single lab-wide Python path. Use the environment documented by the project you are
working on; for a new practice project, the setup below works across these platforms.

Use `uv` to manage the project's Python environment: a separate set of packages for
this analysis. Its lockfile records the dependency versions. If setup is unfamiliar,
ask the agent:

```text
Help me set up a new practice project. Check my operating system and shell,
then check whether Git, Python and uv are installed. Explain anything
missing and help me install what I need using instructions for this system.
Keep the setup local to this project where possible.
Use pandas and matplotlib for a small analysis, and pytest for tests.
Explain the commands and save the setup in a Git commit.
```

With uv installed, these commands initialise a new practice directory:

```bash
uv init
uv add pandas matplotlib
uv add --dev pytest
uv run python --version
uv run pytest --version
```

These commands check the environment; they do not run an analysis. See the
[uv project guide](https://docs.astral.sh/uv/guides/projects/) for details.

For an existing project, follow its environment instructions. Some neuroimaging tools
need conda, containers or separately installed software. Record the chosen setup in
`CLAUDE.md` and avoid adding a second package-management workflow without a reason.

On a shared server, follow its existing environment and installation arrangements.
Cybertron and GenomeDK are different systems; the SLURM instructions later in this book
are specifically for GenomeDK.

## Terminal basics you will actually use

| Key | Does |
|-----|------|
| `Shift+Tab` | Cycle modes — get to **Plan Mode** before any nontrivial task |
| `Esc` | Interrupt the current response or action |
| `Esc Esc` | Rewind to an earlier point in the conversation |
| `/clear` | Wipe context and start fresh. Do this between unrelated tasks |
| `/model` | Switch model |
| `!` prefix | Run a shell command yourself, output goes into the conversation |
| `@` prefix | Reference a file so it gets read into context |

## Sanity check before you start real work

- Save the starting state in Git and use a branch for substantial changes. The agent can
  help initialise a practice repository; see [page 4](04-project-layout.md).
- You are using fictional practice data. Read [page 13](13-data-and-ethics.md) before
  granting access to research files.
- You have a short `CLAUDE.md` with the environment, scope and data-access rules.

Continue with the [internal lab tutorial](lab-data-tutorial.md) or the
[fictional warm-up](first-exercise.md). You can add more project structure later.

---

[← Working with context](02-context.md) · [Contents](../index.md) · [Next: Project layout →](04-project-layout.md)
