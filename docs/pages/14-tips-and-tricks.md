# 14. Practical tips

[← Human-subject data](13-data-and-ethics.md) · [Contents](../index.md) · [Next: Resources →](15-resources.md)

---

Once you have tried the first exercise, use agents to explore something you want to do:
understand a script, make a figure or automate a repetitive calculation. Small, recoverable
experiments are a good way to learn.

## Give it something concrete

"Fit a reinforcement-learning model" leaves many scientific choices unstated.
Provide a [model context file](../starters/rescorla-wagner-spec.md) with the equations,
parameter definitions and example calculations, then ask the agent to build the pipeline.

For a simpler task, a few lines may be enough: column definitions, units, the desired
output and one expected answer. Rich context means useful information, not necessarily
a long prompt.

## Learn while it works

Ask the agent to explain a short function, predict an output, or compare two approaches.
Try the calculation yourself before checking its answer. Follow citations to the original
source when a methodological claim matters.

Useful prompts include:

```text
Explain this function using the six-row practice dataset.
Which line determines whether participants or trials get equal weight?
What plausible mistake would the current tests miss?
Show me a simpler version with the same behaviour.
```

## Commit often

Let the agent make small commits with messages that describe the change.
Inspect `git log --oneline` and ask it to explain a diff when you need help.
[Page 4](04-project-layout.md) introduces the commands.

Keep plot styling, calculation changes and dependency updates separate when practical.
This makes it easier to review a PR and to locate a regression.

## Restart when it helps

If the agent repeats unsuccessful fixes, ask it to summarise what was tried and what the
evidence rules out. Save useful work, then start a fresh session from the project files.
Reconsider the approach if the same problem returns.

You can also write a small part yourself or ask a lab mate. There is no requirement to
finish a task through the same agent session that started it.

## Give longer tasks checkpoints

For an analysis across many files or participants, ask for one verified example first.
Agree how progress and completion will be checked before running the rest. On a cluster,
use the [plan, one task, full run sequence](12-genomedk-skill.md).

## Optional connections

Some agents can connect to external tools through MCP, a protocol for exposing tools
and data. A literature manager connection, for example, may let an agent search papers
and annotations.

You do not need these integrations to use the book. If you add one, understand which
account and files it can access, and check source material yourself before relying on
a summary. The [data guidance](13-data-and-ethics.md) applies to connected tools too.

---

[← Human-subject data](13-data-and-ethics.md) · [Contents](../index.md) · [Next: Resources →](15-resources.md)
