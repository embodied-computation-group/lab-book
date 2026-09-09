# Agents in the Lab

A practical lab book from the Embodied Computation Group for PhD students using AI coding
agents in scientific work. Start with a small analysis, give the agent useful context,
check the result and commit often.

The examples use Claude Code. The main references are
[Ten Simple Rules for AI-Assisted Coding in Science](https://arxiv.org/abs/2510.22254)
and Russ Poldrack's [Coding with AI](https://bettercode-book.org/book-ai-coding-assistants.html).
The book introduces their ideas gradually, with an accessible first exercise and optional
material on modelling, skills and cluster work.

## Read it

[Open the lab book](https://www.the-ecg.org/lab-book/) or start at
[docs/index.md](docs/index.md) on GitHub.

To preview locally with uv installed:

```bash
uvx --with mkdocs-material mkdocs serve
```

Open <http://127.0.0.1:8000>. To check the static build:

```bash
uvx --with mkdocs-material mkdocs build --strict
```

The site is rebuilt automatically on pushes to `main`.

## Contribute

Keep the writing concrete and welcoming. Explain unfamiliar tools before using them,
and distinguish beginner habits from optional extensions.
See [Contributing](docs/pages/16-contributing.md).

This repository is public. Do not add credentials, participant information, unpublished
results or material from collaborators that we do not have permission to publish.
Teaching data must be fictional and labelled as such.

## Layout

```text
docs/
├── index.md        # introduction and staged reading paths
├── pages/          # chapters and the first exercise
└── starters/       # copyable examples
mkdocs.yml          # site configuration and navigation
```

Use relative links so the book works both on GitHub and as a rendered site.
