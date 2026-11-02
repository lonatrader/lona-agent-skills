# Contributing to Lona Agent Skills

Thank you for your interest in contributing to Lona Agent Skills! This guide will help you get started.

## How to Contribute

### Reporting Issues

- Use [GitHub Issues](https://github.com/lonatrader/lona-agent-skills/issues) to report bugs or suggest improvements.
- Include a clear description of the problem or suggestion.
- For skill-related issues, mention which skill is affected (trading-strategy, market-data, or backtest-analysis).

### Submitting Pull Requests

1. **Fork** the repository.
2. **Create a branch** from `main` for your changes (`git checkout -b feature/my-improvement`).
3. **Make your changes** following the conventions below.
4. **Test** your changes by loading the plugin in Claude Code or Cursor.
5. **Submit a pull request** with a clear description of what you changed and why.

### Adding a New Skill

To add a new skill to this repository:

1. Create a new directory inside `skills/` with a descriptive name (e.g., `skills/portfolio-optimization/`).
2. Add a `SKILL.md` file inside the directory with the following structure:
   ```markdown
   ---
   name: lona-your-skill-name
   description: A clear one-sentence description of when this skill should be activated.
   ---

   # Skill Title

   Explanation of the skill's purpose and available tools.

   ## Available Tools
   - List all MCP tools this skill uses

   ## Workflows
   - Describe step-by-step workflows

   ## Examples
   - Include practical examples

   ## Tips
   - Add usage tips and gotchas
   ```
3. Update the skills table in `README.md`.
4. Add an entry to `CHANGELOG.md`.

### Adding a New Rule (Cursor)

1. Create a new `.mdc` file in the `rules/` directory.
2. Include YAML frontmatter with `name`, `description`, `globs`, and `alwaysApply` fields.
3. Update the rules table in `README.md`.

### Adding a New Command

1. Create a new `.md` file in the `commands/` directory.
2. Use the frontmatter format with `name` and `description` fields.
3. Include clear steps and user prompts.
4. Update the commands table in `README.md`.

## Conventions

- **Skill names** use the `lona-` prefix (e.g., `lona-trading-strategy`).
- **Skills** live in `skills/<skill-name>/SKILL.md`.
- **Rules** live in `rules/<rule-name>.mdc` (Cursor-specific).
- **Commands** live in `commands/<command-name>.md`.
- **Agents** live in `agents/<agent-name>.md`.
- **SKILL.md files** must include YAML frontmatter with `name` and `description`.
- **Tool references** use backtick-wrapped names (e.g., `lona_list_strategies`).
- **Markdown** should be clean, well-structured, and free of unnecessary formatting.

## Platform Compatibility

This plugin supports both Claude Code and Cursor:

| Component | Claude Code | Cursor |
|-----------|------------|--------|
| Skills (`skills/`) | Auto-discovered | Via `plugin.json` path |
| Rules (`rules/`) | N/A | Via `plugin.json` path |
| Commands (`commands/`) | Supported | Supported |
| Agents (`agents/`) | Supported | Supported |
| MCP | `.mcp.json` (HTTP transport) | `mcp.json` via manifest |

Keep the MCP server name and URL synchronized between `.mcp.json` and `mcp.json`. Claude Code declares `type: "http"`; Cursor infers the transport from `url`. Never commit credentials or OAuth tokens. Validate with `claude plugin validate .`, check manifest paths, and follow the README testing checklist in each target host before publication.

## Code of Conduct

Keep discussions respectful, constructive, and focused on the work.

## Questions?

If you have questions about contributing, open a [Discussion](https://github.com/lonatrader/lona-agent-skills/discussions) or reach out at [lona.agency](https://www.lona.agency).
