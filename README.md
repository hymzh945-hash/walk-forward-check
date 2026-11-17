# Walk-Forward Check

A single HTML file that answers one question: **does your backtest survive a window it never saw?**

Most backtests look good because the parameters were chosen while looking at the answers. This tool does the opposite — it optimises nothing for you, it takes one frozen parameter set, runs it on the first part of your data, then runs it on the part it never touched.

No install. No account. No API keys. It never connects to an exchange and never places an order.

## Why

The most common failure I see posted in trading forums is not a bad strategy — it is a strategy whose parameter set was picked by looking at the whole sample. It reports +300%/yr, then loses money live. The number that would have warned you is the same parameters, run on data after the optimisation window.

## Use

1. Download `wf-lite.html`.
2. Double-click it. It opens in any browser, offline.
3. Click **Load sample data** to see a worked example, or drop your own CSV.
4. Press **Run the check**.

CSV format — header names are detected automatically:

```
time,open,high,low,close,volume
2024-01-01T00:00:00Z,100.00,101.20,99.40,100.80,1234
```

Bar length is inferred from the timestamps and used for funding costs.

## What it computes

- Split the series into in-sample (default 70%) and out-of-sample (30%)
- Run one EMA-cross parameter set on both halves
- Charge fees, slippage and funding on every trade — **all numbers are net**
- Show in-sample vs out-of-sample return, trade count, max drawdown, and the decay
- Warn you when the out-of-sample window has too few trades to mean anything

## What it does not do

- It does not place orders or connect to a broker
- It does not search parameters for you
- It does not tell you what to trade. It tells you whether your test was honest.

## Free vs full

This repo is the free edition: one strategy, one parameter set, no grid, no export.

The full kit adds a parameter grid with an out-of-sample heatmap, Donchian breakout, long/short mode, a one-page PDF report, and a "is only the best cell green?" read on the grid — $19 on Gumroad: <https://hymz.gumroad.com/l/walkforward-audit-kit>

## Reading the result

If out-of-sample is sharply worse than in-sample, the edge was in the search, not the strategy. Expectation should be set from the out-of-sample number, not the one you optimised.

## License

MIT. Use it, fork it, break it.
