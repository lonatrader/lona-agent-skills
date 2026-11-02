---
name: lona-strategies
description: List and inspect LONA strategies or save requested strategy changes.
---

Use `lona_list_strategies` and `lona_get_strategy` to resolve saved strategies and their source. For authoring, follow the trading-strategy skill: read `lona_get_strategy_documentation`, write complete source, validate it with `lona_run_dry_run_backtest`, then save through `lona_create_strategy` or `lona_update_strategy`. Use the newly returned ID after an immutable update. Listing or inspecting a strategy must not launch a backtest.
