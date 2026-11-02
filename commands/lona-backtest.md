---
name: lona-backtest
description: Prepare, run, and inspect an authorized LONA backtest.
---

Follow the backtest-analysis skill. Resolve the actual saved strategy, symbol IDs, cached frequency, date coverage, and simulation settings using the connected tools' schemas. Run only the work the user authorizes; keep a preview-only request read-only. Call `lona_run_backtest`, retain its report ID, and wait with `lona_wait_for_reports`. Read completed results with `lona_get_report` and full trade history with `lona_list_report_trades`. Use `lona_show_report` for a requested interactive view where supported. Show terminal errors and do not automatically resubmit failed or timed-out executions.
