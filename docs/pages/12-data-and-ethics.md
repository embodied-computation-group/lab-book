# 12. Human-subject data

[← Driving the cluster with the genomedk skill](11-genomedk-skill.md) · [Contents](../index.md) · [Next: Tips and tricks →](13-tips-and-tricks.md)

---

We work with data from people, under ethics approvals and GDPR. Agentic tools change the
risk picture in one specific way: **an agent reads files and sends what it reads to a
server.** That is the whole hazard, and it is easy to trigger without noticing.

This page is lab policy, not advice. If you are unsure about anything here, ask Micah
before running the command.

## The line

> **Personal data does not enter a context window.**

That means an agent must never read:

- name, CPR number, email, address, phone, or any direct identifier
- date of birth, or dates precise enough to re-identify (scan dates included)
- free-text clinical notes, interview transcripts, or open-ended questionnaire responses
- unanonymised DICOM headers — these carry `PatientName`, `PatientBirthDate`,
  `PatientID`, `StudyDate` and more, routinely
- **defaced-but-not-anonymised structural MRI**: a T1 is a facial reconstruction. Treat
  raw structurals as identifiable
- consent forms, screening logs, recruitment spreadsheets, the participant key

Working with pseudonymised, de-identified trial-level data is fine. That is the great
majority of what we analyse — HRD and RRST trial files, questionnaire scores under a study
ID, preprocessed derivatives.

## Practical protections

**Keep identifiers out of the working directory entirely.** The participant key lives
somewhere the project directory cannot reach. Not in `data/`, not one level up, not in a
sibling folder. An agent exploring "the project" should be physically unable to find it.

**Deny the paths in settings.** Project `.claude/settings.json`:

```json
{
  "permissions": {
    "deny": [
      "Read(./data/raw/**)",
      "Read(**/*.dcm)",
      "Read(**/participant_key*)",
      "Read(**/consent/**)",
      "Read(**/*identifiable*)"
    ]
  }
}
```

This is a real seatbelt, not a formality, and it costs a minute. Adjust the globs to your
project's actual layout.

**Anonymise before the agent sees anything.** Run the de-identification step yourself,
outside the agent session. Then let it work on the output. Do not ask an agent to
anonymise data — you cannot verify what it read on the way through.

**Grep before you hand over a file.** If you are unsure whether a spreadsheet has
identifiers in column BF, check:

```bash
head -1 data/processed/questionnaires.csv | tr ',' '\n' | nl
```

Ten seconds, and it has caught things.

**Be specific about scope.** "Have a look at the project and see what you find" is how an
agent ends up reading a folder you forgot about. Point at files.

## Cluster and cloud

Data governed by our approvals stays where the approval says it stays. Do not copy
participant data to a laptop, a personal cloud drive, or a scratch directory outside the
project to make an agent's life easier. If a workflow seems to require that, the workflow
is wrong.

On GenomeDK the agent runs on the cluster and reads cluster files, so all of the above
applies identically there.

## Disclosure in papers

Journals increasingly ask how AI tools were used. Keep a short note as you go — it is much
harder to reconstruct later:

> Analysis code was written with AI assistance (Claude Code, Anthropic). All code was
> reviewed by the authors, and analyses were validated against simulated data with known
> ground truth. No participant data was processed by the model.

That last sentence should be true. This page is how it stays true.

## If something does get read

It happens. Tell Micah the same day. What we need to know is which file, which fields, and
which session — not a confession. There may be a reporting obligation depending on what
was in it, and that clock starts when we find out.

---

[← Driving the cluster with the genomedk skill](11-genomedk-skill.md) · [Contents](../index.md) · [Next: Tips and tricks →](13-tips-and-tricks.md)
