# 15. Contributing

[← Resources](14-resources.md) · [Contents](../index.md)

---

This book is only useful if it keeps up. The bar for adding something is low.

## What is worth adding

**Scar tissue.** The best entries in here are things that cost somebody an afternoon. If
you hit a failure that was not obvious, was not in the error message, and took you a while
to understand — that is a paragraph somebody else will thank you for.

**Corrections.** If something here is wrong or out of date, fix it. Do not add a caveat
next to the wrong thing; replace the wrong thing.

**Resources you actually read.** Page 14 only lists things somebody opened. If you add a
link, say what is in it and whether you read it — an unverified link is worse than no link,
because it looks like a recommendation.

## What does not go in

- Anything secret: tokens, passwords, participant identifiers, unpublished results.
- Long prose. One page, one idea, readable in five minutes.
- Generic content already covered better elsewhere. Link to page 14 instead.

## How to add a page

1. `git switch -c labbook-<topic>`
2. Copy the structure of an existing page: `# N. Title`, nav line, `---`, content, nav line
   again at the bottom.
3. Number it. If you insert in the middle, renumber the following pages and fix their nav
   links — `sed -i` handles it, and it is worth doing rather than leaving a `7b`.
4. Add the row to the table in `docs/index.md`, and to the `nav:` block in `mkdocs.yml`.
5. Push and open a PR. Tag Micah.

Nav line format, top and bottom of every page:

```markdown
[← Previous page](0N-previous.md) · [Contents](../index.md) · [Next: Title →](0N-next.md)
```

## Style

Match what is here:

- Plain declarative sentences. Say the thing.
- Concrete over abstract. "8 threads took 50 minutes against 17 single-threaded" beats
  "multithreading can be slower".
- Commands you have actually run, pasted from your terminal.
- No hedging about how exciting the technology is. Everybody reading this already uses it.
- Where something is uncertain or unverified, **say so in the sentence**, not in a footnote.
  A buried caveat is not a caveat.

## Using an agent to edit this book

Fine, and slightly recursive. Two rules:

- **Do not let it invent links or citations.** Every URL in here was fetched and checked.
  If an agent adds one, open it yourself before merging. This is the single most common way
  a document like this rots.
- **Do not let it smooth out the specifics.** Agents like to generalise "the licence server
  drops tasks above roughly 20 launches per minute" into "be mindful of rate limits". The
  specifics are the entire value.

## This repo is public

Deliberately. Most of what is in here is generally useful, few labs write it down, and our
cluster paths and account names are not secrets.

So the bar for adding something is: **would I mind a stranger reading this?** Almost always
no. What must never go in:

- credentials of any kind — tokens, keys, passwords, `.env` contents
- participant data or identifiers, including **real** exclusion lists and subject IDs
- unpublished results, or the specifics of a design that is not out yet
- anything from a collaborator's project that is not ours to publish

Example data in the starter files is fictional and labelled as such. Keep it that way —
invented subject exclusions read as real ones to someone skimming.

If something fails that bar, it belongs in the project's own private repo or in a
gitignored `NOTES.md`, not here.

---

[← Resources](14-resources.md) · [Contents](../index.md)
