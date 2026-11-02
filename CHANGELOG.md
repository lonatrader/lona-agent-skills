# Changelog

All notable changes to this project will be documented in this file.

## [2.2.0] - 2026-11-02

### Changed

- Replace the local npm/API-key connection with the hosted remote MCP and OAuth sign-in.
- Add Cursor's `mcp.json`, retain Claude Code's `.mcp.json`, and update both manifests.
- Refresh skills, commands, and agent guidance for current tools, strategy validation, immutable versions, data availability, optimization, and Walk-Forward Analysis.
- Replace retired tool examples and fixed tool counts with current schema guidance.
- Add setup, reviewer testing, and marketplace submission instructions, with a square logo on a background.

## [2.1.0] - 2026-03-12

### Added

- **Cursor Marketplace support**: `.cursor-plugin/plugin.json` manifest for Cursor plugin discovery
- **Rules**: `rules/lona-trading.mdc` — Cursor-specific guidelines for Lona MCP tool usage
- **Logo asset**: `assets/lona-icon.svg` for marketplace display
- **Platform compatibility table** in README

### Changed

- **Skills directory restructured**: Moved from root-level directories to `skills/` subdirectory for cross-platform compatibility
  - `trading-strategy/` → `skills/trading-strategy/`
  - `market-data/` → `skills/market-data/`
  - `backtest-analysis/` → `skills/backtest-analysis/`
- **README**: Updated for dual-platform (Claude + Cursor) installation instructions
- **CONTRIBUTING**: Updated skill creation guide to reflect `skills/` directory convention

## [2.0.0] - 2026-02-26

### Added

- Initial public release of the Lona Agent Skills plugin
- **Skills**:
  - `lona-trading-strategy` — Create and manage Backtrader strategies + AI generation
  - `lona-market-data` — Browse datasets and download crypto data from Binance
  - `lona-backtest-analysis` — Run backtests and analyze performance metrics
- **Commands**:
  - `/lona-backtest` — Full end-to-end backtest workflow
  - `/lona-strategies` — Strategy CRUD operations
  - `/lona-data` — Market data browsing and download
- **Agent**:
  - `trading-assistant` — Specialized agent for trading strategy development
- Plugin manifest (`.claude-plugin/plugin.json`)
- MCP server connection (`.mcp.json`) via `npx @lona/mcp-server`
