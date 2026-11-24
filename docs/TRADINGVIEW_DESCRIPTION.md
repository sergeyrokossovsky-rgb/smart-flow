# TradingView publication text (v11)

Copy into the TradingView "Publish script" dialog.

**Title:** Smart Flow - Liquidity Sweeps & Trade Plan

**Description:**

Smart Flow maps where liquidity rests, detects when it gets swept, and turns each confirmed sweep into a graded trade plan that you can audit on your own chart.

**How it works**
1. *Liquidity map.* Buy-side and sell-side zones are built from pivots on three levels: Macro, Local and Micro. Each zone tracks the volume traded inside it (health %). In Pro mode it also shows an estimated (candle-based) delta split into four quadrants.
2. *Sweep detection.* A sweep is a run beyond the recent N-bar high or low on above-average volume, followed by a close back inside within a few bars. Sweep quality combines depth, speed of reclaim, volume, rejection, wick and close position.
3. *Context score (rule-based).* Five components are each scored 0–100: trend (local EMAs plus the higher-timeframe trend), volatility regime, location versus VWAP, liquidity and sweep quality. Liquidity rewards a fresh sweep of the opposite zone and room to the next untouched liquidity. If any component strongly disagrees, the score is penalised. Grades: A+ needs FVG confluence, A needs a swept zone, then B and C.
4. *False-sweep check.* A grade is lowered one step when two or more warning signs appear: shallow run, low volume, momentum body, RSI not extreme at the sweep low/high.
5. *Trade plan and statistics.* Every signal gets:
   - entry at the bar close;
   - stop beyond the sweep extreme plus an ATR buffer;
   - TP1 at a fixed R;
   - TP2 at the nearest opposite liquidity or a fixed R.

   The plan is walked forward bar by bar and the results are summarised by grade: trades, win rate, average R and profit factor, after your cost setting.

**How to read it**
- ▲ / ▼ badges show direction and grade. Hover a badge for the full breakdown.
- The red box is the risk, the green box the reward, the dashed line TP1.
- The dashboard shows bias, volatility, the last signal and its live R, the nearest liquidity above and below, and the statistics.

**Alerts:** create one alert with "Any alert() function call". You will get signals and plan events (TP1, TP2, stop, timeout) in text or JSON for webhooks.

**Limitations (please read)**
- Signals are final on bar close and do not repaint. Higher-timeframe data uses completed bars only.
- Pivot zones need right-side bars to confirm. They are drawn from the pivot bar; the level tag marks the bar where the zone became known.
- Delta is an estimate from candle shape. It is not exchange order flow.
- Statistics model the plan with simple rules: if stop and target fall in the same bar, the stop is assumed first. Past behaviour on one chart does not predict future results. This is not financial advice.
- Use standard candles. On Heikin Ashi, Renko and similar charts, plans and statistics are disabled.
- Defaults were designed around 5-minute charts with a 1-hour higher timeframe. Other timeframes work via Auto HTF.

Open source under MPL 2.0.
