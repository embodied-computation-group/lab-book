# 9. Notebooks and figures

[← Reproducibility](08-reproducibility.md) · [Contents](../index.md) · [Next: Skills →](10-skills.md)

---

Notebooks are useful for exploring data and explaining an analysis. The main questions
are whether you can review changes and rerun the work from a fresh session.

## If you already use Jupyter

You do not need to change tools to complete this book. Restart the kernel and run all
cells in order before trusting saved output. Move repeated calculations into functions
that you can test.

A notebook file contains code, metadata and often embedded outputs. Ask the agent to use
a notebook-aware reader or extract the relevant cells, rather than dumping the JSON into
context. Inspect the code changes and newly generated outputs. Tools such as Jupytext
can pair a notebook with a plain Python file for easier Git review.

## Text-based options

| Tool | When it may help |
|---|---|
| marimo | Python notebooks stored as `.py` files, with reactive cell execution. |
| Quarto (`.qmd`) | Reports combining prose, code and figures. |
| Jupytext | A text representation alongside an existing Jupyter notebook. |

These are optional choices. Keep the project's existing format unless changing it
solves a specific problem.

For results you will reuse, put the calculation in tested functions and provide a script
or documented notebook execution command. A reader should be able to reproduce the
analysis without guessing the order of your interactive work.

## Use plots to check the analysis

Ask for diagnostics that answer a question:

- participant-level distributions: is an aggregate hiding an unusual case?
- observations with fitted curves: where does the model fit poorly?
- values before and after transformation: did the units or scale change as expected?
- residuals, where appropriate: is there structure the model does not capture?

Save useful diagnostics with the run record. Temporary plots can go in an ignored
scratch directory.

## Publication figures

Specify units, the quantity plotted, what intervals represent, and whether points
represent trials or participants. Check labels, colour accessibility and text at the
final printed size. Use axis limits that support an honest comparison and clearly
indicate any truncation.

An agent can help write and revise the plotting code. Inspect the rendered figure
yourself and compare the plotted values with the calculation that produced them.
For raincloud plots, the lab's [RainCloudPlots](https://github.com/RainCloudPlots/RainCloudPlots)
is an existing implementation to consider.

## Try it

For the first exercise, plot both participant means and the group mean. Ask a lab mate
to identify the unit represented by each mark without reading your code.

---

[← Reproducibility](08-reproducibility.md) · [Contents](../index.md) · [Next: Skills →](10-skills.md)
