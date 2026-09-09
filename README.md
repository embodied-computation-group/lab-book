# ECG Lab Book

Internal handbook for the Embodied Computation Group. **Part I — Agentic coding for
reproducible science**: how to use Claude Code and similar tools on real analyses without
quietly destroying the reproducibility of your results.

Fourteen short pages plus copyable starter files. Private repo, internal use.

## Read it

**On GitHub** — start at **[docs/index.md](docs/index.md)** and click through. Every page
has prev/next links, so it pages like a book.

**As a proper site**, with a sidebar, dark mode, and full-text search — one command, no
install, no hosting:

```bash
uvx --with mkdocs-material mkdocs serve
```

Then open <http://127.0.0.1:8000>. That is the nicer way to read it and the better way to
search it when you are looking for one specific thing.

To build static HTML instead: `uvx --with mkdocs-material mkdocs build` → `site/`
(gitignored).

## Why it is not a hosted site

GitHub Pages is **not available for private repos on the org's current free plan** —
verified, the API refuses with *"Your current plan does not support GitHub Pages for this
repository."* Wikis are unavailable on private repos on this plan too.

Upgrading to Team would not fix it: Pages published from a private repo is a **public**
site, and access-controlled private Pages is Enterprise Cloud only. Since this book
contains cluster paths, account names, and data-handling policy, publishing it is not the
answer.

If we want a real internal URL, the route is a private host — Cloudflare Pages behind
Cloudflare Access is free at our size. Ask Micah.

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
