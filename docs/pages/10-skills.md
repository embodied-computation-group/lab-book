# 10. Skills

[← Notebooks and figures](09-notebooks-and-figures.md) · [Contents](../index.md) · [Next: Cluster work →](11-hpc.md)

---

## Doing the same thing again? Make it a skill

If you keep explaining the same procedure to an agent, that procedure is a good candidate
for a skill. You might repeatedly import papers, prepare cluster jobs, generate an
illustration or clarify an analysis before coding. Save the useful instructions once,
then reuse them in the next session.

Skills also help manage context. A successful session often contains a useful procedure
mixed with false starts, temporary paths and details of one particular task. Turn that
experience into a short, checked set of instructions: what to do, what information is
needed and how to check the output. The next session can load that context without
replaying the whole conversation.

This is what we mean by sanitised, reusable context: remove irrelevant history and
sensitive details, replace one-off values with inputs, and preserve the lessons that
matter. Packaging instructions as a skill does not clean them automatically.

Start with ordinary prompts. Once a workflow is useful enough to repeat, make it easier
to reuse.

## Skills Micah uses almost every day

These examples come from Micah's working setup. Check the lab repository or your installed
skills for availability; these names are not all built-in Claude Code commands.

| Skill | What it does | Context you no longer need to rebuild each time |
|---|---|---|
| `/interview` | Helps clarify a task before implementation. | A sequence of questions about the goal, constraints, assumptions and desired outcome. |
| `/nano-banana` | Generates images through the Gemini API from within Claude Code. | The procedure for calling the image service and handling the generated files. |
| `/opendataloader` | Converts PDFs to Markdown for use as context. | A repeatable way to extract paper text into files the agent can read and refer back to. |
| `/genomedk` | Helps agents use the cluster efficiently. | Local submission conventions, resource choices, monitoring and output checks. |

For example:

```text
/interview
I want to explore confidence and accuracy in this task, but I am not
sure how to frame the analysis. Help me clarify the question before coding.
```

```text
/opendataloader
Convert this public methods paper to Markdown and save it in references/.
Keep a reference to the original PDF and flag equations or tables that
need checking against it. We will use the extracted text as model context.
```

Keeping an extracted paper in a file makes it easier to load relevant sections in later
sessions. Check important equations and tables against the PDF; conversion can introduce
errors or lose structure.

```text
/nano-banana
Create an illustration explaining the context, plan, execute and review
cycle for a lab presentation. Use simple labels and save the image so
we can inspect and revise it.
```

```text
/genomedk
Read the analysis plan and prepare a suitable cluster job.
Explain the resource request and how we will check one task before
running the full batch.
```

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

## Keep the procedure easy to update

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

## Turn a working session into a skill

After a useful session, ask the agent to extract the repeatable procedure:

```text
We have now done this workflow several times. Draft a reusable skill
from the procedure that worked.
Describe when to use it, the inputs it needs, the steps and output checks.
Replace task-specific filenames and settings with explicit inputs.
Remove failed attempts, private data and credentials from the instructions.
Keep useful failure symptoms and their verified fixes.
Put longer reference material in separate files, loaded when relevant.
Show me the draft and identify anything that needs my judgement.
```

Try it on a small case before sharing it. Commit the source with a description of the
change, and use the lab repository's contribution instructions for any generated copies.
Try a different input as well: a reusable procedure should not depend on hidden facts
from the conversation that created it. When you improve the workflow, update the skill
so the next session benefits.

External collections, such as
[Crawfurd's academic research skills](https://lcrawfurd.github.io/claude-skills/),
include review and reproducibility procedures. Read what a skill does before installing
it, and check the findings it produces as you would any other agent output.

---

[← Notebooks and figures](09-notebooks-and-figures.md) · [Contents](../index.md) · [Next: Cluster work →](11-hpc.md)
