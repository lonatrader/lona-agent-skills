---
name: lona-backtest-analysis
description: Use when the user wants to run or analyze LONA backtests, parameter optimizations, or Walk-Forward Analysis.
---

# Backtests and analysis

Follow the connected server's current schemas and account limits. Resolve real strategy and symbol IDs before execution. A request for a preview or explanation must not start a run. Use `lona_get_credit_usage` when the user needs their balance; do not invent job costs. Execute only the requested work and avoid automatically resubmitting jobs after a timeout or error.

## Backtests

1. Retrieve the strategy and verify the selected data's cached frequency and coverage.
2. Establish dates, frequency, initial cash, commission, leverage, and any numeric or boolean parameter overrides. Use the advertised fields, including `initial_cash` and an array of `{name, value}` overrides. Apply documented defaults when appropriate; ask if a material choice is missing.
3. If execution is authorized, call `lona_run_backtest`. Keep the returned report ID and wait with `lona_wait_for_reports`.
4. Check each terminal status. Read completed metrics with `lona_get_report`; use `lona_list_report_trades` for paginated trade history. Surface failures instead of inventing results.
5. Include the tested period, assumptions, trade count, return, drawdown, and available risk metrics. Stored report statistics take precedence over trade recounts; timeline-derived trade P&L excludes fees and commissions.

Use `lona_list_reports` to find saved results without rerunning a backtest. Request an interactive view with `lona_show_report` when wanted. Only show tools request UI, and the host may not support it; missing chart objects in a tool response are not a reason to retry or start another execution.

## Optimization

Use `lona_run_optimization` for an authorized parameter grid sweep. Follow its current schema and entitlement/credit requirements. Do not assume tools from another deployment are available; use only those advertised by the connected server.

Wait with `lona_wait_for_optimization`, inspect `lona_get_optimization`, and page through `lona_list_optimization_results`. Present the target metric, direction, parameter grid, tested dates, and actual results. Treat grid results as neutral historical comparisons, not a recommended parameter set. Compare matching assumptions and distinguish optimized in-sample performance from unseen-data validation.

## Walk-Forward Analysis

Walk-Forward Analysis requires Pro, Premium, or Quant. Use `lona_preview_walk_forward_analysis` to inspect the schedule, backtest count, out-of-sample share, and estimated credits before launching. Always present the returned out-of-sample share. If the user requested only a preview, stop there. Launch an authorized analysis with `lona_run_walk_forward_analysis`, wait with `lona_wait_for_walk_forward_analysis`, and inspect `lona_get_walk_forward_analysis`.

Explain rolling versus anchored windows and distinguish in-sample optimization from out-of-sample results. Follow the returned date semantics: configuration dates and displayed window periods include both their first and last value (UTC days, or UTC minutes for hourly steps). Each out-of-sample period starts immediately after its in-sample period ends. Present the returned dates unchanged; do not convert them to exclusive boundaries.

Report historical findings and their limitations without universal performance thresholds or promises of future returns.
