---
name: lona-trading-strategy
description: Use when the user wants to inspect, create, or modify a Python Backtrader strategy in LONA.
---

# Strategy development

Use the connected LONA tools and their current input schemas. Follow the server's authoring instructions and the documentation returned by `lona_get_strategy_documentation`.

1. For an existing strategy, use `lona_list_strategies` and `lona_get_strategy` to retrieve its actual source and ID. Do not change a strategy when the user only asks to inspect it.
2. Understand the requested entry and exit rules. Ask only necessary questions; do not add position sizing, stops, or other risk rules the user did not request.
3. Read `lona_get_strategy_documentation` before authoring. Write complete Python Backtrader source using its supported interface. Strategy parameters and backtest overrides must be numbers or booleans.
4. Validate the complete source using `lona_run_dry_run_backtest` before saving. Correct reported errors and validate again. A dry run uses a fixed dataset and is a code check, not a performance report.
5. Save a requested new strategy with `lona_create_strategy`, or send complete updated source to `lona_update_strategy`. Updates use immutable versioning and return a new strategy ID; use the returned ID for subsequent runs.
6. Report the saved name, version, and ID. Send source through tool arguments; follow the server's response instructions rather than pasting the entire source into chat by default.

Creating a strategy does not run a full backtest. Never call retired natural-language strategy-generation tools or invent strategy IDs. Do not repeat a successful create call: it would create a separate strategy.
