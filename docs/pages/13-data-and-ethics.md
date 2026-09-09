# 13. Human-subject data

[← Driving the cluster with the genomedk skill](12-genomedk-skill.md) · [Contents](../index.md) · [Next: Tips and tricks →](14-tips-and-tricks.md)

---

Read this before giving an agent access to research files. With a hosted model, file
contents and command output can be sent to the provider. Running the agent's terminal
on a university machine or GenomeDK does not itself keep those contents on that machine.

For initial practice, use schemas, fictional examples and code. For research data,
follow the project's approved arrangements for storage, computation and model access.
GitHub organisation membership gives repository access; it does not by itself determine
which hosted tools may process the data. Use the agreed lab environment for the
[internal tutorial](lab-data-tutorial.md), and keep its data and outputs private.
If an arrangement is unclear, check with Micah before exposing participant information.

## Pseudonymisation is not permission to upload

Replacing names with study IDs does not necessarily anonymise a dataset. Data that can
be linked back to a person remains personal data, as the
[European Commission explains](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/application-gdpr_en).
Trial files, questionnaire scores and derivatives need the project's approved handling,
even when they use study IDs.

Keep these out of the agent's accessible files and outputs:

- names, CPR numbers, contact details and participant keys;
- dates of birth, precise scan dates and identifying metadata;
- clinical notes, interview transcripts and open-ended responses;
- consent forms, screening logs and recruitment records;
- DICOM headers and structural images that may identify participants.

Defacing an image is one processing step; it does not establish that all associated
files and metadata are anonymous.

## Set up the working environment

Keep restricted files in storage the agent cannot access. A separate folder or
`.gitignore` entry does not restrict filesystem access. Ask for help setting permissions
or using an isolated development environment if needed.

Tool permissions provide another layer. For Claude Code, this is an example to adapt
to the project's paths:

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

Check the [current permissions documentation](https://code.claude.com/docs/en/permissions)
for how rules apply to each tool, including shell access. Do not treat these example
patterns as a complete access boundary. Test the configuration with harmless dummy files.

## Develop with fictional examples

Provide a data dictionary and a small fictional file under `data/generated/`. Include
the relevant column types, units and missing-value conventions. Do not paste the first
few rows of a participant file as a convenient example.

Inspect candidate files yourself outside the agent session. Column names alone cannot
establish that a file contains no identifying information. Review logs, filenames,
tracebacks and figures as well as the data: these can expose participant information.

Run approved analysis code on research data through the agreed workflow. Review any
output before sharing it with a model. Do not ask the agent to anonymise restricted data
by reading it first.

## Record AI assistance accurately

Keep a note of the tools used, the tasks they assisted with, the data they could access
and the verification you performed. Use that record when preparing the manuscript's
disclosure, following the journal's instructions.

For example, if accurate:

> We used Claude Code (Anthropic) to assist with analysis code. The authors reviewed
> the implementation and checked it using simulated data and independent calculations.

Only claim that no participant data entered the model if you have established that this
is true. Do not copy a disclosure that describes checks you did not perform.

## If restricted information is read

Stop further access and tell Micah promptly, on the same day. Record which files or fields
were involved and which session, without copying the sensitive content into another tool.
Follow the institution's incident process; Micah can help identify the appropriate contact.

---

[← Driving the cluster with the genomedk skill](12-genomedk-skill.md) · [Contents](../index.md) · [Next: Tips and tricks →](14-tips-and-tricks.md)
