# Capstone rubric

Total 100, plus extra credit. The sections are the course spine, made
checkable. Grade the work that is there; a defensible wrong answer scores
higher than an undefendable right one.

**This batch:** Ljung-Box was not covered, so it is not graded. The residual
check in B is done by eye — residual plot plus ACF, both taught. A student
who runs Ljung-Box anyway is not penalised and earns no extra points for it.

**Your own data or method.** The air-passengers notebook is a starter, not a
requirement. A project on a different series, or with a different framework
or model family, is graded against the same sections: each criterion is
read as its equivalent on that project (the floor is the naive that fits
that series' frequency and seasonality; "the framework" is whatever library
fitted the model; the harness keeps rolling origins, h and step chosen to
suit the series). What does not change: a benchmark floor,
rolling-origin cross-validation, intervals with coverage, no leakage, and
the report. Evaluate the project as it is — its data, its method, and how
well the work holds up — not against the starter.

## A — Exploration and shape (20)

| point | criterion |
|---|---|
| 5 | Plots the series and identifies trend and seasonality in plain language, not just "it has trend and seasonality" |
| 5 | STL decomposition; reads all three panels and says which component does the work |
| 5 | Trend and seasonal strength computed (textbook formulas), with a sentence on what they imply for model choice |
| 5 | ACF of the raw series; knows what the lag-12 spike means; states the shape in one or two sentences a non-forecaster could repeat |

## B — The floor and what it leaves (20)

| point | criterion |
|---|---|
| 8 | Fits the seasonal naive (the floor) and at least one other benchmark |
| 7 | Plots the floor's residuals (`y_t - y_{t-12}`) and their ACF; reads what structure is left on the table (trend? autocorrelation at low lags? at 12?) and which kind of model eats it |
| 5 | Gives the floor an honest interval and reads its 80% coverage against the nominal 80% |

## C — The framework (15)

| point | criterion |
|---|---|
| 5 | The data conversion to AutoGluon's frame is done by hand and visible — not hidden behind a helper |
| 5 | Fits a real zoo (more than one model), and the leaderboard is displayed on the held-out months |
| 5 | Reads the leaderboard: names the **sign** of `score_val` and how many windows it scored, and says in one sentence what that ranking can and cannot be trusted to do |

## D — The harness (20)

| point | criterion |
|---|---|
| 8 | Cross-validates the shortlisted model over the SAME rolling origins (8 windows, h=12, step=12) as the floor — through the harness, not one holdout |
| 7 | One table, one row per model: MASE, scaled CRPS, and 80% coverage; reads each model against the floor |
| 5 | Reports where the model beats the floor and where it loses, on which metric — a win on the point and a loss on the distribution is reported as both; coverage verdict included |

## E — The report (25)

| point | criterion |
|---|---|
| 7 | The one-sentence recommendation, and the evidence behind it |
| 6 | The intervals: width, coverage, and a verdict on honesty |
| 6 | The residuals: what the model missed, and what that suggests it is missing |
| 4 | One specific, credible next step |
| 2 | Written for a manager: no unexplained jargon, charts that carry their claims, length actually kept |

## Anti-patterns (deductions, stack)

- MASE reported without CRPS or coverage — the number is half a result (−5)
- One holdout window (including AutoGluon's own single split) presented as
  evidence for a ranking (−10)
- No benchmark floor, or the floor present but not compared (−10)
- No intervals anywhere in the notebook or the report (−10)
- A framework result quoted without saying what it fits or how it ranked
  internally (−5)
- Leakage of any kind: a feature, a fit, or a denominator touching data the
  fold was not allowed to see (−15, and flag it to the student)

## Submission requirements (not points, but checked)

- Submitted as a fork, committed and pushed; the notebook runs as pushed.
- The top of the fork's `README.md` carries the line
  `Submitted by: <your name> — academy: @SDAIAAcademy`, with the name filled
  in.
- Deadline: **10:00 AM (Riyadh time), Thursday 15 October 2026**.

## Extra credit (10 points)

- Dynamic regression on a driver you source and cache (e.g. monthly mean
  temperature from a public weather archive), with the cross-validation
  discipline applied to the regression's residuals.
