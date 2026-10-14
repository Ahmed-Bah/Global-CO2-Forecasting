Submitted by: Ahmad Bahwerith - academy: @SDAIAAcademy

# Global CO2 Forecasting

Capstone for the SDAIA time series course. The series is global monthly atmospheric CO2 from NOAA GML, 568 months from March 1979 to June 2026. I used it instead of the AirPassengers default because the brief allows a different series.

## Question

Which model should we ship to forecast CO2 12 months ahead, and how far can we trust its intervals?

## Result

AutoETS beats the seasonal-naive floor on every metric over eight rolling 12-month windows (MASE 0.17 vs 1.37). Full write-up in [report.md](report.md).

## Files

- `project.ipynb` is the notebook: data, exploration, floor, AutoGluon, harness.
- `report.md` is the report for a non-technical reader.
- `data/co2_global_monthly.csv` is the frozen data (`date`, `co2_ppm`).
- `coursekit/` holds the course helper code for plotting and scoring.
- `brief.md` and `rubric.md` are the assignment.