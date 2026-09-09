# Project instructions template

Copy the text inside the block into your project's `CLAUDE.md` and replace placeholders.
Start short; add instructions when they solve a recurring problem.
See [page 5](../pages/05-claude-md.md).

```markdown
# Project: <name>

## Question
<What are we trying to calculate or understand?>

## Scientific context
- Read <MODEL.md or another specification> for equations and conventions.
- Follow that specification. Identify ambiguities before implementation.
- Do not change model terms, exclusions or expected test values just to make code run.
- The scientist reviews scientific choices; help implement and test the pipeline.

## Environment
- Use the project's uv environment.
- Run analysis: <actual command, for example uv run python scripts/analyse.py>.
- Run tests: uv run pytest.

## Data
- Use fictional examples for agent-visible development.
- Never write to raw observations or read restricted participant information.
- Store synthetic observations and simulations in data/generated/ and label them.
- If an input is missing, report it. Do not invent replacement observations.

## Working cycle
- Give a short plan for a substantial change.
- Keep changes small and run the relevant checks.
- Make focused Git commits throughout the task, with descriptive messages.
- Stage only relevant files; exclude research data, credentials and unrelated edits.
- Record check outcomes, including expected failures in a test-first commit.
- Save progress and update task notes before restarting a session.
- Ask before publishing changes or starting an expensive run.

## Data definitions
<!-- FICTIONAL EXAMPLES: replace with reviewed, non-identifying project definitions. -->
- Reaction times are in milliseconds.
- Calculate each participant's mean, then average participants with equal weight.
- Specify missing-value and duplicate handling before implementation.

## Known issues
<Add verified symptoms and fixes when useful.>
```

For cluster work, add the account, storage and submission instructions from
[page 11](../pages/11-hpc.md) after confirming them for your project.
