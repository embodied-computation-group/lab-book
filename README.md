# ECG Lab Book

Internal handbook for the Embodied Computation Group. **Part I — Agentic coding for
reproducible science**: how to use Claude Code and similar tools on real analyses without
quietly destroying the reproducibility of your results.

Fourteen short pages plus copyable starter files. Written for our lab; public because
most of it is generally useful and none of it is secret.

## Read it

### → **<https://www.the-ecg.org/lab-book/>**

Sidebar nav, full-text search, dark mode. Rebuilt automatically on every push to `main`.

**On GitHub** — start at **[docs/index.md](docs/index.md)** and click through. Every page
has prev/next links, so it pages like a book either way.

**Locally**, if you are editing it — one command, no
install, no hosting:

```bash
uvx --with mkdocs-material mkdocs serve
```

Then open <http://127.0.0.1:8000>. That is the nicer way to read it and the better way to
search it when you are looking for one specific thing.

To build static HTML instead: `uvx --with mkdocs-material mkdocs build` → `site/`
(gitignored).

## What does not go in here

The repo is public, so:

- no credentials of any kind — tokens, keys, passwords, `.env` contents
- no participant data or identifiers, including **real** exclusion lists and subject IDs
- no unpublished results, or specifics of a design that is not out yet
- nothing from a collaborator's project that is not ours to publish

Example data in `docs/starters/` is fictional and labelled as such. Cluster paths and
account names are fine — they are not secrets, and they are the specifics that make the
cluster pages worth reading.

Full guidance in [Contributing](docs/pages/14-contributing.md).

## Layout

```
docs/
├── index.md        # the book's cover and contents table
├── pages/          # 01–14, one idea per page
└── starters/       # copyable: CLAUDE.md, Snakefile, gitignore, checklists
mkdocs.yml          # site config; nav lives here
```

Links are all relative, so they work both in the rendered site and when browsing raw `.md`
on GitHub. Keep it that way — see [Contributing](docs/pages/14-contributing.md).

## The short version

1. **Code is generated faster than it can be verified.** Verification is the bottleneck
   now, not writing.
2. **Put an orchestrator between the agent and your outputs** so you know which code
   produced which file.
3. **Generated data never touches `data/raw/` or `data/processed/`.**
4. **Review in a fresh session.** A context that just wrote the code is a bad judge of it.
5. **Never compute on the GenomeDK frontend.** An agent asked to "test the script" will run
   the script.
6. **No participant data in a context window.** Ever.
