# Capstone — Air passengers, start to finish

## The series

Monthly international air passenger numbers, 1949-01 to 1960-12: 144
observations, no gaps. The Box & Jenkins classic — one of the most-studied
series in the field. The notebook fetches it straight from statsmodels'
R-datasets; no download step.

## The job

The course pipeline, on this series: explore it, decompose it, set the
benchmark floor, check what the floor leaves on the table, fit a model
through the framework, cross-validate, and read the result against the
floor.

## Your own data or method

This series and this notebook are a starter for anyone who wants a worked
path. They are not the only path. You may:

- **use a different series** — any regularly spaced series with enough
  history for rolling-origin cross-validation (at least a few seasonal
  cycles), from a public source or your own work, cached in the repo or
  fetched by the notebook;
- **use a different framework or model** — statsforecast, Darts, Prophet,
  sktime, a hand-built model, or another AutoML library in place of
  AutoGluon.

The pipeline and the rules below do not change: explore it, set a benchmark
floor (the naive that fits your series' frequency and seasonality),
cross-validate over rolling origins (choose `h`, step and the number of
windows to suit your series), score the point *and* the interval, and
write the report. Your project is evaluated on its own terms: the rubric is
read against its equivalent on your project.

## Deliverables

1. **The notebook**, built on `project.ipynb`, in order: exploration,
   the floor, your model, the cross-validation. Every chart carries its
   claim. Runs top to bottom in under ten minutes on Colab.

2. **The report**, two to three pages, for a manager who will not open the
   notebook:
   - **The recommendation.** Which model you would ship, in one sentence, and
     the one number that earns it.
   - **The intervals.** How wide, what they covered, and whether the band is
     honest.
   - **The residuals.** What your model missed, and what that means (read
     from the residual plot and its ACF — Ljung-Box is not required this
     batch).
   - **One change.** A specific next step — data, driver, frequency, or
     horizon — and what you expect it to do.

3. **Extra credit (optional).** Dynamic regression on a driver you source
   (e.g. monthly mean temperature from a public weather archive such as
   Open-Meteo — free, no key), cached as a CSV — the cross-validation
   discipline still applies to the regression's residuals.

## What is graded

**The process, not the number.** A low MASE from one holdout with no
intervals scores worse than an honest analysis that concludes the benchmark
wins.

## Rules

- **Harness only.** Every number comes out of the rolling-origin harness. A
  number that could not have come out of it does not count.
- **The floor is not optional.** It is the thing every other model has to
  beat. If nothing beats it, that is a result.
- **No leakage.** A fold's fit and its denominator use only data that fold
  was allowed to see.

## Submission

1. **Fork** this repo on GitHub (Fork → create it under your own account).
2. **Solve** it in your fork: fill in the TODO cells in `project.ipynb` (or
   your own notebook, if you changed the data or method) and write the
   report as `report.md`. At the top of `README.md`, fill in the line
   `Submitted by: <your name> — academy: @SDAIAAcademy` with your name.
3. **Commit** your work to your fork.
4. **Push**, so the notebook and the report live on GitHub — not just in a
   runtime.
5. Submit **your fork's URL**. The notebook is graded as it runs, in the
   state you pushed.

Deadline: **10:00 AM (Riyadh time), Thursday 15 October 2026**.
