# One building, one week, three contextual judgments

The example follows Atlas office through **12–18 October 2026**.
Chronos-2 forecasts the complete 168-hour week from the preceding 1,344 hourly
readings. Comparing observations with its 0.01-0.99 quantile band flags 29
hours, which form three consecutive deviation episodes.

| Episode | Detected interval (Europe/Zurich) | Hours | Mean observed kWh | Mean forecast kWh | Jev response |
|---|---|---:|---:|---:|---|
| 1 | 13 October, 04:00–22:00 | 18 | 12.19 | 41.98 | `LOG_EXPLAINED` |
| 2 | 14 October, 22:00 to 15 October, 06:00 | 8 | 39.70 | 13.56 | `ALERT` |
| 3 | 16 October, 13:00–16:00 | 3 | 104.94 | 61.27 | `VERIFY_CONTEXT` |

## Walk through the week

**13 October: a quiet building on a working day.** The forecast expects the
usual weekday activity. The meter stays near the essential-services load.
The room calendar still lists an on-site planning day, but the 12 October office
manager email moves everyone to an external venue and leaves the office
closed. Jev selects `LOG_EXPLAINED`.

**14–15 October: consumption persists after closing.** The meter stays
well above the overnight forecast for eight hours. The closing handover
establishes that staff have left and no overnight activity or overrides are
approved. Jev selects `ALERT`.

**16 October: a short load surge with incomplete paperwork.** A contractor
reports completing a load-bank test in the same three-hour window. The
dispatch group covers the office and a detached workshop, which have separate
utility meters. The completion sheet leaves the address blank. Whether the
test accounts for this office meter's surge therefore remains unresolved.
Jev selects `VERIFY_CONTEXT`.

These episodes occur in one continuous meter series and one chronological
facility log. Every detected window is sent to Jev. Each request includes the
hourly observations, forecast median and bounds, and only records published
before that episode's assessment time. All three use the same generic choice
question. Python returns the selected labels unchanged.

## Saved material

- [Executed notebook](context_aware_anomaly_triage.ipynb): the complete workflow and saved outputs.
- [The continuous week](results/weekly_anomalies.png), also available as [SVG](results/weekly_anomalies.svg).
- [Episode close-ups with decisions](results/episode_decisions.png), also available as [SVG](results/episode_decisions.svg).
- [Exact requests and complete responses](results/triage_run.json).
- [Forecast](results/forecast.csv), [every monitoring hour](results/monitoring_week.csv), and [decision table](results/decisions.csv).

The meter readings and notes are authored teaching fixtures. The forecast and
three responses in the saved notebook come from the completed execution at
2026-10-25T20:21:12.449601+01:00. Chronos-2 ran locally on CUDA,
using revision `29ec3766d36d6f73f0696f85560a422f50e8498c`;
OpenRouter returned `typesafe/jev-1.14-20261014`.
