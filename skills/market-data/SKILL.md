---
name: lona-market-data
description: Use when the user needs to find market datasets or check symbol coverage and frequencies for a LONA backtest.
---

# Market data

Use the currently advertised tool schemas. Discover actual datasets rather than assuming a ticker is a valid LONA ID.

1. Search a known ticker or name with `lona_search_symbols_by_name`. Use `lona_list_symbols` for browsing, applying its ownership and asset-class filters when relevant.
2. Inspect the selected instrument with `lona_get_symbol`. Present its ticker, name, asset class, exchange, equity market when provided, date coverage, and cached frequencies. Distinguish instruments with similar names or different listings.
3. `data_availability` describes provider coverage; it does not prove the data is cached. `cached_frequencies` lists the frequencies available for a run now.
4. If a supported global symbol has no cached data and the user requests preparing it, call `lona_download_market_data` with its `symbol_id`. For queued/running status, call the same tool with that ID to continue waiting. Use the data only after completion.
5. Check the requested frequency exists in every selected symbol's cached frequencies and that the requested period is covered. Global equity and ETF data is daily-only; supported global crypto and forex frequencies depend on the symbol. Global intraday data requires a paid plan; Free can use daily global data or its own uploaded data.

Keep symbol/data IDs distinct from strategy and report IDs. Do not invent candle previews, use retired data-preview tools, or pass historical Binance-specific download arguments. Explain unavailable frequencies and tool errors directly.
