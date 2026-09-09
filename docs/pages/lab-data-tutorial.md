# Lab tutorial: explore an interoception dataset

[Contents](../index.md) · [Quick warm-up](first-exercise.md) · [Workflow guide](06-the-loop.md)

Use an agent to turn a real lab dataset into a small analysis you can explain:
download it, check it, explore it, make a plot and answer a question. Allow about an hour
for a first pass, or stop after the plot and come back later.

This is an **internal lab exercise** using
[gender_intero](https://github.com/embodied-computation-group/gender_intero).
Lab members already have organisation membership; use your lab-linked GitHub account.
The source repository is private. This public page contains instructions, not its
participant data or findings. Work in the lab-approved environment and keep your
practice repository and outputs private. See [data access](13-data-and-ethics.md).
For an exercise that needs no research-data access, use the [fictional warm-up](first-exercise.md).

## The question

**How does mean reported confidence differ between the cardiac and auditory conditions
for participants who completed both?**

We will use the heartbeat discrimination (HRD) trial file. In the cardiac condition,
participants compare a stimulus with their heartbeat; the auditory condition is an
external comparison task. Begin with a descriptive comparison. A difference in mean
confidence is not, by itself, a difference in metacognitive ability.

You can explore other questions later. Keeping the first question small makes it easier
to see what the agent is doing and check the result.

## 1. Get the data and save the starting point

Create a new practice project with [the basic environment](03-setup.md).
Ask the agent:

```text
Help me start a small, private learning project using gender_intero.
Use the lab-approved data environment. Download only
data/raw/hrd_trials.tsv from source commit
146f64fc20eefa1aefea9ba09a2d6880a50b445a,
using my existing GitHub authentication. Save it under data/raw/.
Do not print participant rows into the conversation.

Record the repository URL, commit, file path and a file hash in DATA_SOURCE.md.
Keep the downloaded file unchanged. Ignore data/ and results/ in Git.
Set up a minimal Python project with pandas, matplotlib and pytest.
Write a short README and make an initial commit of the setup and source record.
Do not push or publish this practice project.
```

A **source commit** fixes the version you download, so changes to the upstream repository
will not change the exercise halfway through. The source file and its extraction code
were inspected at this version when preparing the tutorial.

The download can use GitHub CLI (`gh`). If authentication needs an interactive login,
do that yourself in the terminal; do not paste a token into the agent conversation.
A missing file or access error should be reported, not replaced with invented data.

**Checkpoint:** the input file exists, its version is recorded, and `git status` does
not propose committing it. The agent can explain the folders it created.

## 2. Give the agent the data context

A TSV is a table separated by tabs. Ask the agent to read the extraction script,
[code/00_extract_raw.R at the same commit](https://github.com/embodied-computation-group/gender_intero/blob/146f64fc20eefa1aefea9ba09a2d6880a50b445a/code/00_extract_raw.R),
for the definitions. Write a short `ANALYSIS.md` together:

| Column | Meaning for this exercise |
|---|---|
| `Subject` | Participant grouping key; keep values out of chat and public outputs. |
| `Modality` | `Intero` for cardiac, `Extero` for auditory. |
| `Confidence_raw` | Reported confidence on a 0–100 scale. Zero is a valid endpoint. |
| `Accuracy` | 0 for an incorrect response, 1 for a correct response. |

There are other columns, but these are enough to begin. Use `Confidence_raw` rather than
guessing that a model-preparation file's binned confidence represents the same quantity.

This file is already an extract: the source script filters for provided decisions and
ratings. It is not every acquired trial, and it is not automatically the paper's final
analysis sample. Read the project's exclusion documentation before claiming to reproduce
the paper. For this exercise, label the result as a descriptive exploration of the
downloaded extract and record any additional filtering.

Try this prompt once the source notes are available:

```text
Read the extraction script at our recorded source commit.
Help me write ANALYSIS.md for this descriptive question:
How does participant mean confidence differ between Intero and Extero
among participants with valid observations in both?

Document the columns, the 0–100 confidence scale, what the extract already
filters, and what we are not claiming to reproduce.
Calculate means within participant and modality first; give participants
equal weight in the paired summary. Do not infer model choices from the
repository name or add a gender comparison.
List any ambiguities and give me a short plan before writing analysis code.
After we agree it, commit the context and plan.
```

**Checkpoint:** the plan matches the question, uses the right confidence scale and
makes the participant weighting explicit.

## 3. Import and run quality checks

**Quality control (QC)** means checking that the data has the structure and values the
analysis expects. Ask:

```text
Write a small script to load the TSV and produce a QC report.
Check required columns, numeric parsing, missing values, modality labels,
confidence in [0, 100], and Accuracy in {0, 1}.
Report trial counts per participant and modality, and how many participants
have both modalities. Keep row-level details in local files, not chat.
Flag duplicate-looking rows for investigation; do not silently remove them.
Do not drop outliers or add participant exclusions.
Make a focused commit after the import and QC work.
```

Check whether parsing introduced missing values. Ask how duplicate rows were assessed:
identical responses can be legitimate repeated trials, so matching values alone are
not sufficient evidence for removal.

**Checkpoint:** you can explain the QC report, any warnings and whether the analysis
can proceed. If a definition is unclear, fix the context before adding more code.

## 4. Make a first plot

Ask for a table with one row per participant and modality: mean confidence, proportion
correct and the number of valid trials contributing to each measure. Have the agent
state how missing values are handled, even if none are present.

Plot the distribution of participant mean confidence separately for the two modalities.
Give each participant equal weight in the summary. Label the confidence scale and the
number of participants represented.

Open the figure. Try a histogram, then ask for a dot plot or box plot and compare what
you can see. Change colours or labels if you like; keep the calculation unchanged.
Commit the summary code and plotting code in separate steps.

```text
Using ANALYSIS.md and the QC report, calculate mean Confidence_raw,
proportion correct and valid-trial counts for each Subject and Modality.
State how missing values are handled. Save the table locally in results/.
Plot the distribution of participant mean confidence for each modality,
with clear labels, a 0–100 confidence axis and participant counts.
Show me the figure and explain what each mark represents.
Keep participant labels out of the figure and raw rows out of chat.
Commit the summary code and plotting code as separate changes.
```

**Checkpoint:** you know whether a plotted point represents a trial or a participant,
and you can identify which source column produced it.

## 5. Answer the paired question

Now restrict the comparison to participants with valid mean confidence in both
modalities. Match them by `Subject`, not by their row positions.

For each participant, calculate:

```text
difference = mean cardiac confidence - mean auditory confidence
```

Ask for the mean of those differences, the number of complete pairs, and a plot of the
differences with a reference line at zero. Report how many participants were omitted
because a pair was incomplete. This is the descriptive answer to our question.

Use a fictional fixture to check the calculation:

| Participant | Cardiac mean | Auditory mean | Cardiac minus auditory |
|---|---|---|---|
| A | 70 | 60 | 10 |
| B | 40 | 50 | -10 |
| C | 80 | missing | excluded from paired summary |

The paired mean difference is 0 for two participants. Ask the agent to write that test
before implementing the paired summary. Reordering the rows must not change the answer.

Use the fictional table above in this prompt:

```text
Use this fictional fixture to write a test for the paired summary first.
Match participants by Subject, keep complete pairs, and calculate
Intero minus Extero for each participant. The expected group mean
difference is 0 for two pairs; C is omitted because Extero is missing.
Reordering either input must not change the result.
Commit the test with its expected initial failure recorded.

Then implement the paired summary for the real input.
Report complete-pair and omitted-participant counts, save the mean
difference, and plot the differences with a reference line at zero.
This is descriptive: do not add a significance test or a causal claim.
Run the tests, inspect the outputs and commit the implementation.
```

**Checkpoint:** the fixture passes, row order does not affect pairing, and your Git
history shows the test and implementation separately.

## 6. Save a result you can return to

Ask the agent to make the analysis rerunnable with one documented command, and to update
the README with the input version, QC decisions and output files. Close the plot and
rerun from the saved script to check that it recreates the result.

```text
Make the analysis rerunnable with one command and put it in README.md.
Record the source commit, environment, QC decisions and output filenames.
Run the tests and rerun the analysis from the saved script.
Check that the saved summary agrees with the plotted values.
Keep data and results out of Git, and commit the code and documentation.
Summarise remaining limitations and show me the recent commit history.
Do not push this internal exercise to a public repository.
```

**Checkpoint:** the README command recreates the outputs, and another lab member can
understand what was done from the files and commits.

Write three sentences yourself: what you compared, what the descriptive result shows,
and what it cannot tell you. Avoid calling a confidence difference a causal effect or
a measure of metacognitive efficiency.

At your next lab meeting, bring the plot, a brief explanation and the Git history.
If the agent took an unhelpful turn, show the restart or correction too.

## Try another question

You might explore whether confidence differs between correct and incorrect trials,
or add uncertainty to the paired comparison. Before adding an interval or test, discuss
what it should estimate and how it should handle repeated observations within people.
Do not let the ease of generating another analysis decide the scientific question.

If you get stuck, ask the agent to save the working code and a note of the problem.
Start a fresh session with `ANALYSIS.md`, the README and recent commits. You have not lost
the work; you are trying a different route.

```text
Pause here. Save useful work in a focused commit and write TASKS.md with
what works, what failed, checks already run and the next question.
Do not keep trying the same fix or change the scientific specification.
```

In the new session:

```text
Read ANALYSIS.md, README.md, TASKS.md and the recent Git history.
Restate the unresolved problem and propose one small next step.
Run the existing checks before changing anything.
```
