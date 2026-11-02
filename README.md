# LONA Trading Assistant

Create, backtest, optimize, and analyze Python Backtrader strategies in **Cursor**, **Claude Code**, and other compatible MCP clients using your LONA account.

This public repository contains plugin configuration, skills, commands, and an agent. It connects to LONA's hosted MCP at `https://mcp.lona.agency/mcp` through OAuth. The LONA application and server implementations are maintained separately; no local server, npm package, API key, or user ID is required.

## Get started

1. Create a LONA account at [app.lona.agency/chat](https://app.lona.agency/chat).
2. Add the connection in your assistant using one of the options below.
3. Complete the LONA browser sign-in and authorization when prompted.
4. Try: **List my saved LONA strategies. Do not create or run anything.**

Backtests and optimizations use your account's entitlements or credits. Walk-Forward Analysis requires Pro, Premium, or Quant. Account data and permissions are enforced by the remote service.

## Cursor

### Install the full plugin

While marketplace review is pending, install a local copy of this public package:

```bash
mkdir -p ~/.cursor/plugins/local
git clone https://github.com/lonatrader/lona-agent-skills.git ~/.cursor/plugins/local/lona
```

1. Restart Cursor or run **Developer: Reload Window**.
2. Open **Customize** and confirm the LONA plugin and MCP server are available. Local plugin imports must be allowed by your organization.
3. Enable LONA and complete the browser OAuth sign-in with your LONA account.
4. Ask Cursor: **List my saved LONA strategies. Do not create or run anything.**

This loads the bundled skills, commands, agent, rule, and remote MCP connection. If the folder already exists, update that checkout instead of cloning again. The commands install the repository's default branch; PR changes become available there after merging. For details, see [Cursor's plugin instructions](https://cursor.com/docs/plugins#test-plugins-locally).

### Connect only the MCP

Until marketplace publication is confirmed, connect the MCP manually by merging this entry into `.cursor/mcp.json` in a project, or `~/.cursor/mcp.json` for your user:

```json
{
  "mcpServers": {
    "lona": {
      "url": "https://mcp.lona.agency/mcp"
    }
  }
}
```

Enable the server in Cursor and complete OAuth. This installs the connection only. To load the bundled skills, commands, agent, and rule during development, follow [Testing](#testing). The plugin manifest is `.cursor-plugin/plugin.json`, which loads `mcp.json`.

## Claude Code

To load this entire plugin from a checkout:

```bash
claude --plugin-dir /absolute/path/to/lona-agent-skills
```

Use `/mcp` to authenticate the LONA connection. Alternatively, install just the remote MCP connection:

```bash
claude mcp add --transport http lona https://mcp.lona.agency/mcp
```

Choose one connection method to avoid registering duplicate servers. This repository's Claude Code plugin is separate from the [LONA connector in Claude's directory](https://claude.ai/directory/lona-v2).

## Other MCP clients

Where the host supports remote HTTP MCP with OAuth, enter `https://mcp.lona.agency/mcp` as a custom connector. Tool availability and interactive views depend on the host. A custom connection does not mean LONA is listed in that host's public directory.

## Included workflows

| Component | Purpose |
| --- | --- |
| `skills/trading-strategy/` | Inspect, author, validate, and version Backtrader strategies |
| `skills/market-data/` | Find symbols and inspect cached frequencies and date coverage |
| `skills/backtest-analysis/` | Backtests, reports, optimization, and Walk-Forward Analysis |
| `commands/lona-strategies.md` | List or manage saved strategies |
| `commands/lona-data.md` | Find market data |
| `commands/lona-backtest.md` | Prepare and run an authorized backtest |
| `agents/trading-assistant.md` | Strategy development and analysis guidance |
| `rules/lona-trading.mdc` | Cursor workflow guidance |

The connected server advertises the current tools and schemas; follow those definitions instead of assuming a fixed tool count. Key tools include:

- Strategies: `lona_list_strategies`, `lona_get_strategy`, `lona_get_strategy_documentation`, `lona_run_dry_run_backtest`, `lona_create_strategy`, `lona_update_strategy`.
- Market data: `lona_search_symbols_by_name`, `lona_list_symbols`, `lona_get_symbol`, `lona_download_market_data`.
- Backtests and reports: `lona_run_backtest`, `lona_wait_for_reports`, `lona_get_report`, `lona_list_report_trades`, `lona_show_report`.
- Optimization: `lona_run_optimization`, `lona_wait_for_optimization`, `lona_list_optimization_results`.
- Walk-Forward Analysis: `lona_preview_walk_forward_analysis`, `lona_run_walk_forward_analysis`, `lona_wait_for_walk_forward_analysis`, `lona_get_walk_forward_analysis`.
- Credits: `lona_get_credit_usage`.

Only `lona_show_*` tools request interactive views. Text and structured results remain usable in hosts without widget support. The plugin provides historical strategy testing, not live brokerage execution.

## Testing

Validate the Claude plugin manifest from the repository root:

```bash
claude plugin validate .
```

For Cursor, copy the package into an unused folder at `~/.cursor/plugins/local/lona`, restart Cursor or run **Developer: Reload Window**, and check its components in **Customize**. Copy the hidden manifest directories as well. Local imports must be allowed; an installed marketplace plugin with the same name takes precedence. See [Cursor's local testing instructions](https://cursor.com/docs/plugins#test-plugins-locally).

Check these scenarios in each target host:

1. Authorize with a test account; confirm cancelling sign-in leaves the connection unauthenticated.
2. List strategies, inspect one, search for an instrument, and read an existing report. An empty account should return an empty list, not invented examples.
3. Ask to create a simple strategy. Confirm the assistant reads the documentation, validates complete code with a dry run, and saves the returned strategy ID.
4. Explicitly approve a small backtest using available data. Confirm the returned report reaches a terminal state and actual metrics can be retrieved. Inspect any supported interactive view separately.
5. Request a Walk-Forward Analysis **preview only** on a paid account. Confirm the schedule, out-of-sample share, and estimate are returned without starting the analysis.
6. Verify tool errors are explained and failed or timed-out executions are not resubmitted automatically.

Use a separate test connection and test account when changing environments. The packaged URL points to production. Authenticated end-to-end testing in Cursor and Grok Bot remains required before publication.

## Marketplace submission

After testing and merging this update, submit [lonatrader/lona-agent-skills](https://github.com/lonatrader/lona-agent-skills) at [Cursor's publication form](https://cursor.com/marketplace/publish). The package includes the manifest, MIT license, and a square logo with a background at `assets/lona-icon.svg`. Review and approval are still required; this repository alone does not establish a marketplace listing.

Reference: [Cursor plugin specification](https://cursor.com/docs/reference/plugins), [Claude Code plugin reference](https://code.claude.com/docs/en/plugins-reference).

Support: [feedback@lona.agency](mailto:feedback@lona.agency).

## License

MIT. See [LICENSE](LICENSE). The license applies to this package; remote LONA service access uses your LONA account and plan.
