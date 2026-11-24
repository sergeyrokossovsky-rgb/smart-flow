# Changelog

## v11 — 2026-11-24

### Fixed (full logic audit of v10)
| # | Issue in v10 | v11 |
|---|---|---|
| E1 | The context score was computed before the sweep of the current bar, so sweep quality never reached the grade | Order is now: zones → sweep → context → grade |
| E2 | Divergence compared a pivot with the bar 12 candles back, so it almost never fired | Compares consecutive pivots (`ta.valuewhen`) and stays active for N bars |
| E3 | "Max bars back" did not limit anything | Drawing window and calculation depth now work as described |
| E4 | Alert text showed a price level instead of confidence | `alert()` messages with the plan; classic alerts use named `{{plot("…")}}` |
| E5 | Signal labels had no budget and evicted zone labels | Each layer has its own object budget |
| E6 | One zone cap was shared by all levels | Separate caps for Macro, Local and Micro |
| E7 | The RSI check ran on the reclaim bar | RSI is read at the true sweep extreme |
| E8 | Two overlapping session switches, no time zone | One session filter with a time zone |
| E9 | The VSA colour inputs had no effect | Colours follow the inputs |
| E10 | Liquidity context lagged one bar and contradicted its own description | Same-bar evaluation; redefined as *fuel* (fresh opposite sweep) + *room* (distance to the next liquidity) |
| E11 | The MTF timeframe was fixed at 4H on every chart | Auto higher timeframe, validated to be above the chart timeframe |
| E12 | Dashboard confluence rows were almost always "--" | Shows the data of the last signal |
| E13 | With the divergence hard filter, a bearish divergence blocked **both** sides | Bearish blocks longs, bullish blocks shorts |

Smaller fixes:
- Overlapping SSL zones now keep the deeper zone.
- The running average of sweep volume excludes the current sweep.
- Symbols without volume data no longer disable sweeps.

### Non-repainting
- Higher-timeframe trend and HTF FVG use `expr[1]` with `lookahead_on`.
- Signals are final on bar close. A faded "forming" badge shows the open bar.
- Alerts fire once per bar close.

### Added
- Trade plan per signal (entry, stop, TP1, TP2 at the opposite liquidity) and forward statistics by grade, after costs.
- A "why" tooltip on every signal.
- Visual presets Clean / Standard / Pro / Custom, automatic light/dark theme, compact and expert dashboards.
- Nearest liquidity above and below, in ATR.
- JSON alerts for webhooks and trade-plan event alerts.
- Data checks for missing volume, non-standard chart types and an invalid higher timeframe.
- Calculation depth, to stay inside TradingView execution limits.

### Removed
- "AI" and "Institutional" from the name, and the unsupported "improves win rate" claim.

## v10 — Liquidity Engine (closed source)
The three-level liquidity profiler with volume/delta quadrants and zone health, SweepTracker, the five-factor context engine with grades, FVG on the chart timeframe and HTF, VSA, previous-session HV levels, normalisation, false-sweep detection and a 21-row dashboard.
