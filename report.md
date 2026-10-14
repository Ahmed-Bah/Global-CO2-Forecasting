# Forecasting global atmospheric CO2: report

## Recommendation

Ship AutoETS. Over eight rolling 12-month forecasts its MASE is 0.17, against 1.37 for the seasonal-naive floor, about eight times more accurate than repeating last year's values.

The data is monthly global CO2 from NOAA GML: 568 months, March 1979 to June 2026. It rises steadily (about 337 to 429 ppm) with a yearly cycle of about 5 ppm, so a model needs both a trend and a season. The floor has the season but no trend, and that is why it loses.

| Model | MASE | CRPS | 80% coverage |
|---|---|---|---|
| Seasonal naive (floor) | 1.37 | 0.0033 | 0.60 |
| Random walk with drift | 0.92 | 0.0030 | 0.70 |
| AutoETS | 0.17 | 0.0005 | 0.75 |

The gap holds in every window. AutoETS's worst window (MASE 0.44) beats the floor's best (1.17). A single holdout would have hidden this, so the comparison uses eight origins.

## The intervals

The 80% band for AutoETS averages 0.89 ppm wide, narrow next to the 5 ppm yearly swing.

It is slightly overconfident, though. An 80% band should contain the truth 80% of the time and this one does so 75% of the time. That is still the best of the three (the floor covers 60%, drift 70%). For planning, treat the band as a little tighter than advertised. With only 96 forecast points, the gap is small and imprecisely estimated.

## What the model missed

The floor's errors (this year minus last year) average +1.93 ppm, are almost always positive, and move slowly (lag-1 autocorrelation 0.96). This is the missing trend: the floor repeats last year and ignores the yearly rise. A model with an adaptive trend can absorb it, and AutoETS does.

AutoETS has two remaining weaknesses:

- **Bias.** Its mean error is +0.22 ppm, so it tends to forecast slightly low.
- **Horizon.** Its average absolute error grows from 0.11 ppm one month ahead to 0.51 ppm twelve months ahead, roughly fivefold.

Both are small relative to the signal. The model is most reliable over the next few months and less so near the end of the year.

## Limits of this work

- Only AutoETS went through the full eight-window evaluation. AutoARIMA was on the shortlist from the AutoGluon run but was not tested the same way, so I can't say it wouldn't do as well.
- The most recent months of data are provisional and get revised, so the last windows carry extra uncertainty.

## One change

Calibrate the interval and re-check coverage. Scale the AutoETS band using the errors from the eight evaluation windows so it covers 80% instead of 75%, and run AutoARIMA through the same eight-window harness. I expect the point forecast to stay the same (MASE about 0.17) and coverage to move to about 0.80, with a slightly wider band. If AutoARIMA matches AutoETS on accuracy and has better coverage, ship that one.