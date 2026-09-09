# 2. Working with context

[← Start here](01-start-here.md) · [Contents](../index.md) · [Next: Setup →](03-setup.md)

---

An agent uses your messages, project instructions, files it reads and command output to
work on a task. Together these form its working context. It also has knowledge from
training, but that is not a reliable source for facts about your project.

Make the relevant facts easy to find: the question, data schema, relevant code and a
description of a correct result.

## Missing information and distracting information

Asked to "fit the model" without its definition, an agent has to make assumptions.
A fit can run successfully while using the wrong units, exclusions or parameterisation.

Long context brings a different problem. Chroma's
[*Context Rot* experiments](https://research.trychroma.com/context-rot) found that
performance varied with input length and distractors. Keep context focused, but do not
treat a particular length as a universal limit. Repeated mistakes may also reflect an
unclear task, a software bug or a method the model does not understand.

## What to provide

- Point to files and explain their purpose: "The binning function is in
  `src/confidence.py`; use it rather than adding another."
- Describe columns, units and missing-value conventions. Use a schema or fictional
  examples, not participant rows. See [page 13](13-data-and-ethics.md).
- Include the error and enough surrounding output to diagnose it. Keep full logs on disk
  and ask for a targeted search if more detail is needed.
- State what must stay fixed, such as preprocessing or preregistered model terms.
- For notebooks, use a tool that reads cells or a text representation rather than
  dumping JSON and embedded images into the conversation.

The agent may need more files to understand a dependency. Ask it to identify what else
it needs and why.

## Example: specify the model, then build the pipeline

A request such as "write a Rescorla–Wagner model" leaves the agent to supply equations
and conventions from memory. It may choose a different variant or introduce an error.

Instead, the scientist prepares a context file with the intended equations, initial
values, parameter meanings, update order and a few calculations worked by hand. Ask
the agent to turn that specification into tested functions, input handling, fitting
code and plots.

The [example model context file](../starters/rescorla-wagner-spec.md) shows this for a
two-option learning task. For example, it states that choice probabilities use values
**before** the current trial's reward updates them. That timing decision is part of the
model, not an implementation detail for the agent to guess.

You can ask the agent to help draft or explain the specification, but verify it yourself
before implementation. Good scientific context lets the agent accelerate construction
of a pipeline you understand.

## Persistent context

Put recurring instructions in `CLAUDE.md`: environment commands, directory rules, data
definitions and known pitfalls. Keep current tasks and findings in `TASKS.md` or
`NOTES.md`. [Page 5](05-claude-md.md) explains what belongs in each.

Poldrack distinguishes general working rules ("constitution") from project facts and
progress ("memory"). Both can live in instruction files, but separating their purposes
helps you keep them useful. His practical advice is to compact during a problem and
clear between problems, then reload the relevant notes.
See [sections 5.4.3–5.4.4](https://bettercode-book.org/book-ai-coding-assistants.html).

| Situation | Useful response |
|---|---|
| Starting an unrelated task | Save decisions, then use `/clear`. |
| Continuing with a long conversation | Update task notes; use `/compact` to shorten the conversation. |
| Repeating a misunderstanding | Check the brief and files, then restart with corrected information. |
| Handing work to someone else | Record changes, checks, unresolved questions and the next step. |

Compaction may omit details. Scientific decisions belong in the project record as well
as in the conversation: someone reproducing the analysis should not need your chat history.

When you repeat a task across sessions, consider turning the procedure into a
[skill](10-skills.md). This preserves the useful instructions without carrying forward
the whole conversation. PDF-to-Markdown import, for example, can leave a reusable source
file that later sessions read in relevant sections.

## Task size and separate sessions

Choose a task with an output you can review, such as one function or one pipeline step.
Larger changes need intermediate checks and a record of progress.

A subagent can investigate a specific question in a separate context and return findings
with file references. A fresh review session can check code against a specification.
Give it the requirements and test results: it still needs to know what the code should
do, and it can share the original agent's blind spots.

## Try it

Write a brief with four items: question, input definitions, constraints and completion
check. Ask a lab mate which assumptions they would still have to make. Revise it before
giving it to an agent.

---

[← Start here](01-start-here.md) · [Contents](../index.md) · [Next: Setup →](03-setup.md)
