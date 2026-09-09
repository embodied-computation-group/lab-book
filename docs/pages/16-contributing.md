# 16. Contributing

[← Resources](15-resources.md) · [Contents](../index.md)

---

Add examples, corrections and practical lessons from your work. The intended reader is
a lab member who may be new to coding and wants to try agents on a scientific problem.

## What helps

A useful addition explains a task, shows how to approach it, and gives the reader a way
to check the result. A short account of a mistake and its fix is welcome too.

Keep advanced tools optional until the reader has a reason to need them. Do not describe
a personal preference or suggested tool as established lab policy.

## Style

Use plain language and explain unfamiliar terms on first use. Prefer a concrete example
to a slogan. Avoid claims that a prompt, test or skill guarantees success.

Keep the tone encouraging. Students should feel able to experiment, make small commits
and restart. Scientific care should be taught through the work, not presented as a long
list of prerequisites.

Preserve useful lab details, but distinguish measured observations from general claims.
For a timing comparison, say which task and environment it came from.

Do not turn a detail from your own computer into a claim about the lab. Setup instructions
should work across macOS, Windows and Linux, or clearly state which system they describe.

## Edit or add a page

1. Work on a branch and make focused commits as you go. An agent can help write and
   commit the changes.
2. Use a descriptive title and links to related pages.
3. Keep existing filenames stable where possible. A new tutorial does not need to
   renumber every chapter.
4. Update the reading paths in `docs/index.md` and navigation in `mkdocs.yml`.
5. Run `uvx --with mkdocs-material mkdocs build --strict`.
6. Review the diff, then open a PR.

Use relative links so pages work on GitHub and the rendered site.

New to pull requests? [GitHub with an agent](github-with-agents.md) shows how to prepare
a focused change, ask for help and work through review comments.

## Sources

The main scientific computing references are
[Ten Simple Rules](https://arxiv.org/abs/2510.22254) and
[Poldrack's AI chapter](https://bettercode-book.org/book-ai-coding-assistants.html).
Use current official documentation for tool behaviour.

Open new links and check that they support the accompanying text. Give a source for
substantive claims, and distinguish your own teaching examples from source material.
Do not claim the entire reading list has been rechecked unless it has.

## This repository is public

Keep credentials, participant identifiers, real exclusion lists, unpublished results and
restricted collaborator material out of the book. Do not copy content from a private
project merely because you can access it.

Fictional teaching data must be labelled as such. For a real-data tutorial, confirm the
release and access arrangements, link to the source and record the version.
An internal lab exercise must be labelled as internal.

Private material belongs in its approved project storage. A gitignored file is not
protected from agent access or accidental sharing.

---

[← Resources](15-resources.md) · [Contents](../index.md)
