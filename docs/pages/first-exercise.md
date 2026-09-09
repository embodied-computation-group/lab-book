# First exercise: a CSV, a calculation and a plot

[Contents](../index.md) · [Setup](03-setup.md) · [Workflow guide](06-the-loop.md)

Allow about 20–30 minutes for the first pass. Start in a new practice folder, with
[the environment set up](03-setup.md). The aim is to experience the whole cycle on
something small: give context, make a plan, build it, check it and save your progress.

All observations in [practice-trials.csv](../starters/practice-trials.csv) are fictional.
Copy the file into `data/generated/` in your practice project.

## 1. Decide what you want to calculate

The file has two fictional participants. A has two reaction times, 200 and 400 ms.
B has four, 500, 600, 700 and 800 ms.

We want the mean reaction time **giving each participant equal weight**. Work out the
two participant means, then their mean. You should get 300 ms, 650 ms and 475 ms.

The mean of all six trials is about 533.33 ms. That answers a different question because
B contributes twice as many trials. This small choice is the scientific context the
agent needs.

## 2. Give the agent a brief

```text
These are fictional practice data in data/generated/practice-trials.csv.
Make a small Python analysis that loads the CSV, calculates each
participant's mean reaction time, then averages those means.
Each participant must have equal weight. Reaction times are in milliseconds.
Save a table and a labelled plot in results/.
Keep the code simple and explain anything I may not know.
Show me a short plan first.
Use Git and make small, descriptive commits as we go.
```

Read the plan. Does it include two stages of averaging? Does it stay within the task?
Correct it if needed, then let the agent build the script.

## 3. Run it and check

Ask the agent to run the script and show you the output. Open the plot yourself.
Do the participant means match 300 and 650 ms, and does the group mean equal 475 ms?
Are the units and the meaning of each point clear?

Ask it to put this known-answer check into a test and add the run commands to
`README.md`. Rerun the test, then let the agent commit the working calculation and plot
code. Keep generated outputs out of Git; the code should recreate them.

Look at `git log --oneline` together. The messages should tell you what was built.

```text
Run the analysis and show me the table and plot.
Check participant means of 300 and 650 ms and a group mean of 475 ms.
Add a test for these values, then run it.
Put the run and test commands in README.md.
Commit the working code and instructions; keep results out of Git.
Show me the recent commit messages.
```

## 4. Try a small change

Change the plot's colours or add a title that states the question. Ask the agent to keep
the calculation unchanged, run the test again and make a separate commit.

```text
Add a clear title and try a different colour scheme for the plot.
Keep the calculation unchanged. Rerun the test and regenerate the plot.
Show me the result and make a separate commit for this change.
```

If a session gets confused, save the useful work and start a fresh one with the README
and relevant files. A restart is a normal part of working with these tools.

You have finished the first pass when you can run the script, explain why the answer is
475 ms, and find the commit that added the plot. Bring it to a lab mate and compare notes.

## When you want to go further

Try one of these challenges:

- Duplicate B's trials with new trial IDs. Predict whether the equally weighted mean
  changes, then check. It should remain 475 ms.
- Save the working version, then temporarily replace the calculation with the pooled
  trial mean. Check that the test fails, restore the intended calculation and rerun it.
- Decide how missing values or duplicate trial rows should be handled, and add tests.
- Ask a fresh agent session to review the code against your original question.
- Ask a lab mate to reproduce the result using only the README and saved files.

These lead into [verification](07-verification.md) and
[reproducibility](08-reproducibility.md). You do not need all of them to enjoy your first
session, but they matter increasingly as you move towards results you will rely on.
