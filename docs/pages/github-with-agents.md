# Working with GitHub, with an agent's help

[Contents](../index.md) · [Git basics](04-project-layout.md) · [Contributing](16-contributing.md)

This optional page is for when you want to share a change, get help or work on the same
project as someone else. You do not need to memorise Git commands first. An agent can
handle the mechanics while you learn what each action means.

A useful first goal is to open a small pull request for Micah or a lab mate to look at.
It does not have to be a finished solution. A clear example of a problem is useful work.

## The terms you need

Git records versions of files. GitHub hosts repositories and provides tools for discussing
and reviewing changes. The [commit workflow](04-project-layout.md) introduces local Git;
this page takes that work into a shared project.

| Term | What it means in your project |
|---|---|
| Branch | A separate line of development, such as `paired-confidence`, where you work on one change. |
| Push | Upload your local commits to a branch on GitHub. |
| Pull request (PR) | A proposal to bring changes from your branch into another branch, usually `main`, with a place for discussion and review. |
| Draft PR | Work in progress that can be discussed but cannot yet be merged. |
| Merge | Incorporate the proposed changes into the destination branch. |
| Issue | A place to describe a bug, question or planned task when you do not yet have code changes to show. |

Opening a PR does not change `main`. You can keep adding commits to its branch while
people review it. See [GitHub's PR guide](https://docs.github.com/en/pull-requests/reference/pull-requests).

## 1. Start a branch for one question

Suppose you are extending the [lab-data tutorial](lab-data-tutorial.md) with a paired
confidence summary. Keep that change separate from restyling every figure or updating
all the dependencies.

```text
Help me work on a paired confidence summary in this repository.
Check the current branch, uncommitted changes and remote repository.
Preserve existing work. Fetch the current main branch and create a
branch called paired-confidence from the appropriate starting point.
Explain where the branch starts and what will stay separate from main.
Keep this task focused on the paired summary and its tests.
```

If your work has already started on another branch, tell the agent. It can help move or
separate the relevant changes without discarding them.

**Check:** you know the branch name and can describe the proposed change in one sentence.

## 2. Build something a reviewer can inspect

Give the agent the scientific context, then work in small commits. If you are stuck,
capture the problem in a small example rather than waiting until you have solved it.

```text
Read ANALYSIS.md. Implement the paired summary in small steps, with
tests using fictional data. Include reordered rows and an incomplete pair.
Commit the reviewed tests and implementation separately, recording checks.
If the specification leaves a scientific decision open, describe it
and show the smallest example that makes the decision concrete.
Do not invent an answer just to finish the task.
```

For example, the implementation might use complete pairs, while you want Micah's advice
on what to report about participants who contributed only one condition. Label that
choice as provisional. Keep real participant rows out of the PR description and logs;
the internal tutorial's data and outputs stay in approved private storage.

**Check:** you can explain what works, what fails and what you want help deciding.

## 3. Open a focused PR to get help

An agent with GitHub access can push the branch and open the PR. GitHub CLI (`gh`) is
one way to do this; the agent can help set it up. Complete any interactive login yourself.
Use your existing lab account and the intended repository.

```text
Review this branch's changes against main, including new files.
Check that it contains only the paired-summary work and no research data,
credentials or unrelated edits. Run the relevant checks.
Push this branch and open a draft PR in this repository targeting main.
Describe the question, changes, checks and remaining uncertainty.
Make the specific question for Micah easy to find. Return the PR link.
Do not merge it.
```

Read the description before asking someone to spend time on it. A useful example is:

```markdown
Title: Add paired confidence summary; discuss incomplete pairs

This adds participant-level Intero minus Extero confidence differences.
The current calculation uses participants with both conditions.

Checks: the fictional two-pair example gives a mean difference of zero;
reordering rows leaves the result unchanged. The relevant tests pass.

Question for Micah: is a complete-pair summary appropriate for this
descriptive question, and what should we report about incomplete pairs?

Please start with ANALYSIS.md and the paired-summary test.
The inclusion decision is provisional; this PR is not ready to merge.
```

Replace the example's check claims with what actually happened. A failing test is fine
in a help request if you explain the failure and how to reproduce it.

Creating a draft does not automatically get Micah's attention. Share the link with him,
or explicitly ask the agent to post a comment mentioning his confirmed GitHub username
and the question. For finished work, mark it ready and request his review. Do not have
the agent guess his username. If drafts are unavailable in the repository, use a clearly
labelled work-in-progress PR and state that it should not be merged yet.

**Check:** the PR targets the right branch, and a reader can find the question without
reading your entire chat history. [GitHub explains PR creation and updates here](https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/creating-a-pull-request).

## 4. Work through review comments

Review is a conversation about the work. Ask the agent to help you understand a comment
before implementing it if the scientific meaning is unclear.

```text
Read the comments on PR <number>. Explain each requested change and
separate straightforward code fixes from decisions we need to discuss.
Implement the agreed changes, run the relevant checks and make focused
commits on this PR's branch. Push them to update the existing PR.
Draft a short reply connecting each change to the comment it addresses.
Leave unresolved scientific questions explicit.
```

You do not need a new PR for each correction. Inspect the agent's changes and reply,
then post the reply yourself or ask it to post the wording you have reviewed.

**Check:** comments have been addressed in substance, not merely marked resolved.

## 5. Understand checks and conflicts

A repository may run automated tests or builds on a PR. These are often called
**continuous integration**, or CI. Passing checks are evidence about those tests, not
approval of the scientific method. Some repositories have no automated checks yet.

A **merge conflict** means Git cannot combine overlapping changes automatically.
It is usually a question about which edits to keep, not evidence that you broke Git.

```text
Inspect the failing checks or merge conflict on this PR.
Explain the cause before changing files. For a conflict, show what each
branch intended and propose a resolution that preserves both where possible.
Ask me about competing scientific choices. After resolving the issue,
run the relevant tests and inspect the complete diff again.
Do not disable checks or discard someone else's changes to make it merge.
```

The agent can help resolve a conflict, but a file that merges cleanly can still behave
incorrectly. Recheck the combined result. See [GitHub's conflict guide](https://docs.github.com/en/pull-requests/reference/merge-conflicts).

## 6. Merge the reviewed change

Once the scientific questions are settled and the required review and checks are
complete, you can ask the agent to merge. A draft must first be marked ready.

```text
Check PR <number> against the latest branch state: review requirements,
test results, unresolved comments and the final diff.
If it is ready, merge it using this repository's normal merge method.
Do not bypass branch protections. Report the merged commit and PR link.
Then help me update my local main branch while preserving any unfinished work.
```

Repositories differ in whether they preserve individual commits or combine them when
merging. Follow the project's convention. The small commits still helped during review
and diagnosis, even if the final merge combines them.

If you decide against the approach, close the PR with a brief explanation. A useful
discussion or a test that exposes a problem is worthwhile even without a merge.

## Try it with a lab mate

Open a small PR that improves a README, adds one input check or demonstrates a bug with
fictional data. Ask your lab mate to leave one review comment, use the agent to address
it, and follow the repository's review process through to a merge or a documented close.

You have practised the workflow when you can explain what your branch changes, point to
the evidence, and use the PR to ask a precise question. The agent can handle the commands;
you provide the purpose and judge the result.
