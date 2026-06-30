# BTC→Altcoin Lag: A Research Study and Partial Trading-System Build

*A self-directed quantitative research project conducted with Claude (Sonnet 4.6), March–April 2026, by a first-time, non-technical user. The work runs from a stated hypothesis through data collection, statistical analysis, and a partially implemented execution system. It is unfinished by design: the strategy is supported in historical data but has not been backtested or paper-traded at scale, and no capital has been deployed. This document summarizes the methodology, the findings, and the current status.*

---

## 1. Hypothesis and operating discipline

**Hypothesis.** Liquid altcoins move in the same direction as Bitcoin with a slight but consistent lag, on the order of seconds, and that lag can be measured and potentially exploited with limit orders placed in the window before the altcoin catches up.

**Discipline.** One rule was fixed before any code was written: the goal was to find out whether the hypothesis was true, not to confirm it. If the data did not support it, the project would stop. If it did, the project would proceed to a build. That framing, test to find out rather than test to prove, governed every later decision, including which assets were ultimately selected and which were dropped.

---

## 2. Constraints: regulation first

The first real fork was exchange selection, and it was a compliance question before it was a technical one. New York's BitLicense regime is among the strictest in the United States, and several major venues (Binance.US, Kraken, Crypto.com) do not hold one and are unavailable to a New York resident.

- **Trading venue:** Gemini as primary (0.10% maker fee at base tier; roughly 0.28% round-trip break-even including estimated slippage), with Coinbase Advanced as backup (roughly 0.46% break-even). That fee gap materially affects which edges survive at the position sizes involved.
- **Data source:** Kraken is unavailable for trading in New York, but its free historical tick-data endpoint is one of the best available. Kraken was therefore used for data only, supplying 730 days of tick history at no cost, while trading was confined to the BitLicensed venues.

---

## 3. Data

The analysis used raw trade ticks, not candles. A data pipeline pulled tick-level history for five assets across 730 days (March 2024–March 2026): approximately 79.9 million trade records after deduplication, stored in a local SQLite database.

| Asset | Ticks | Role |
|-------|-------|------|
| BTC | 27.58M | Signal source |
| XRP | 18.03M | Analysis candidate |
| SOL | 16.24M | Original intended target |
| ETH | 13.56M | Analysis candidate |
| LINK | 4.55M | Analysis candidate |

Roughly 2.3M duplicate records, introduced when the multi-day download process resumed after interruptions, were identified and removed automatically before analysis.

**Why ticks rather than candles.** Collapsing trades into one-minute candles destroys the sub-minute timing the strategy depends on. A one-minute candle cannot distinguish a BTC move at second 5 from one at second 55; for a lag that may be under 30 seconds, that timing is the entire signal.

---

## 4. Findings

The original plan was to build a bot on SOL, which was chosen first for its size and liquidity. The analysis was run across all four altcoin candidates simultaneously, and the data reordered the priorities.

| Asset | Verdict | Outcome |
|-------|---------|---------|
| ETH | Edge present, stable | Selected — micro-bot (sub-minute scalping) |
| LINK | Edge present, strengthening | Selected — intraday bot (1-hour momentum) |
| XRP | Edge present, conditional | Not selected — fees consume the edge |
| SOL | Edge present, conditional | Not selected — ranked third; ETH and LINK were cleaner |

Two findings are worth highlighting:

- **SOL was demoted by its own data.** The project began as a SOL bot and was named accordingly, but SOL ranked third once the analysis ran. ETH and LINK showed cleaner, more consistent edges, so the build moved to them. This was the discipline from Section 1 working as intended: the original preference did not survive the evidence.
- **The LINK edge is strengthening, not decaying.** The most recent third of the history showed roughly a 70% follow-through rate on qualifying signals; the oldest third showed roughly 50%. Most backtested edges decay over time, so an edge that has grown is unusual and was flagged for close monitoring rather than treated as settled. (LINK's availability on Gemini is flagged for explicit verification; if unavailable there, the intraday bot defaults to Coinbase Advanced.)

The measured BTC→ETH lag peaked at one second (cross-correlation r ≈ 0.27 at one-second resolution). The two selected strategies were distinct enough to warrant separate parameter sets: a 10-second-resolution micro-bot on ETH (0.30% BTC threshold, ~53% US-session follow rate) and a 1-hour-resolution intraday bot on LINK (1.0% BTC threshold, ~55% US-session follow rate).

---

## 5. Methodology

The analysis was designed around the safeguards professional quantitative researchers use, arrived at from first principles rather than copied from a template: walk-forward validation instead of random train/test splits, minimum sample-size requirements before any model is trained, regime-aware model versioning, counterfactual logging of near-miss signals, and explicit guards against overfitting, edge decay, and lookahead bias. The analysis prompt that encoded these requirements went through roughly ten meaningful iterations, each adding a safeguard the prior version had missed.

---

## 6. Build status

Seven Python files were written. The data-feed layer (asynchronous WebSocket management) was implemented and live-tested against Gemini; the signal-detection layer was integrated but is awaiting a market-hours test to confirm signals fire correctly. Components include a market-state object tracking 22 rolling features, an authenticated order-placement client, a write-behind journaling layer, and a plain-English decision narrator that converts each gate decision, signal evaluation, and safety trigger into a human-readable line and assembles a daily briefing. The narrator was not in the original specification; it was added on the reasoning that a system trading unattended should be able to explain what it did.

A first live connection on April 4, 2026 processed 165 BTC and 104 ETH ticks in an overnight session at roughly 0.02 ms average processing latency, with all safety checks passing and no signal firing, which was the expected result during low-volume hours.

---

## 7. Risk constraints

Deliberate limits were set at the outset: spot only, long only, no leverage, $500–$1,000 per trade, and $2,000 maximum combined exposure. The system was designed to be explainable, controllable, and survivable if something went wrong, rather than to maximize return. The full stack uses only free, open-source tooling; the only recurring cost contemplated for live operation is trading fees plus a small monthly VPS.

---

## 8. On scope and value

Valued by what it would cost to commission rather than by any profit it might earn, the work completed to this point, most of it research and infrastructure, would plausibly run into the low tens of thousands of dollars at standard freelance rates. That figure is a production cost, not a validated return: a backtested micro-edge carries no guarantee of surviving live trading once fees, latency, and decay are accounted for, and most do not. The value of the analysis is that it was done rigorously and honestly, including being willing to drop the original target when the data did not support it; whether the edge is real in production remains an open question that only paper trading and live testing can answer.

---

## 9. Status and remaining work

The project is unfinished. Completed: hypothesis design, regulatory and venue analysis, the data pipeline, the statistical analysis and asset selection, and the first two layers of the execution system. Remaining: a tick-accurate backtest engine, the machine-learning pipeline, order-execution logic, a self-learning/retraining layer, a 30-day paper-trading period, and live deployment. The honest current state is a validated-in-history, not-yet-validated-live strategy with a partially built system around it.

---

*Research summary | Conducted with Claude (Sonnet 4.6) | March–April 2026*
