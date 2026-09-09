# 8. Notebooks and figures

[← Reproducibility](07-reproducibility.md) · [Contents](../index.md) · [Next: Cluster work →](09-hpc.md)

---

## Stop using .ipynb with agents

Jupyter notebooks are a bad fit for agentic work, for three concrete reasons:

1. **They are JSON.** A notebook with a few plots in it is mostly base64 image data. Ask
   an agent to read one and you have spent a large slice of your context window on
   pictures it cannot see properly anyway.
2. **They are stateful.** Cell 12 works because cell 4 ran an hour ago with different
   code. The agent edits cell 4, everything still "works", and the output is now
   meaningless. Nothing about the file records this.
3. **Diffs are unreadable.** You cannot review what the agent changed, which breaks the
   one control you have (page 3).

Use a text-based format instead:

| Tool | Good for |
|------|----------|
| **marimo** | Reactive Python notebooks stored as plain `.py`. No hidden state — cells re-run when their inputs change. Best default for new work. |
| **Quarto** (`.qmd`) | Manuscript-adjacent documents mixing prose, code, and figures. Renders to PDF and HTML. Good for analysis reports and supplements. |
| **Jupytext** | Keeps a `.py` paired with an existing `.ipynb`. The migration path if you have notebooks you cannot abandon. |

All three are plain text, so they diff, they version, and an agent can read them without
burning context.

If you must keep `.ipynb`, at least strip outputs before committing (`nbstripout`) and
never ask the agent to read a notebook with figures embedded.

## Notebooks are for looking, not for pipelines

A notebook is a place to look at data. It is not where an analysis lives. Anything a
figure in a paper depends on should be a function in `src/`, called by a script, invoked by
a Snakemake rule (page 7). Notebooks import from `src/`; they do not define the analysis.

The test: if deleting all your notebooks would break your ability to reproduce the paper,
your pipeline is in the wrong place.

## Generate lots of cheap plots

Plots are now nearly free to produce, and they are the fastest way to catch an agent that
has misunderstood your data. Use them recklessly during development:

- one panel per subject, however ugly
- the fitted curve drawn over the actual data points, every time you fit anything
- the same variable before and after every transformation
- residuals, always
- histograms of anything you are about to average

Ask for a grid of throwaway diagnostics and skim it. Then delete them. `results/figures/`
holds only figures that a Snakemake rule produces; scratch plots go somewhere ignored.

## Publication figures

Two things worth knowing:

**Agents are decent at figure code and poor at figure judgement.** They will produce a
technically correct plot with an unreadable colour map, a misleading axis, and a legend
covering the data. Specify the constraints: colourblind-safe palette, no truncated axes,
show individual data points, fonts at final size.

**Get them critiqued.** The [Tufte visualisation skill](https://lcrawfurd.github.io/claude-skills/)
reviews figures on data-ink ratio and graphical integrity, which is a reasonable second
opinion before a figure goes into a manuscript.

For raincloud plots use the lab's own [RainCloudPlots](https://github.com/RainCloudPlots/RainCloudPlots) —
if an agent starts reinventing one, stop it and point it at the package.

---

[← Reproducibility](07-reproducibility.md) · [Contents](../index.md) · [Next: Cluster work →](09-hpc.md)
