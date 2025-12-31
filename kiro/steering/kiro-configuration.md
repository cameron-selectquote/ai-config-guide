# Kiro Configuration

Purpose: Provide Kiro configuration paths, what each location controls, and reference links for debugging and setup.

## Configuration Locations
- Kiro config root: `~/.kiro/`
  - Stores global Kiro state, settings, and rules.
- Kiro settings: `~/.kiro/settings/`
  - Holds configuration JSON files for Kiro features.
- Kiro MCP config: `~/.kiro/settings/mcp.json`
  - Defines MCP servers. Expects JSON with a top-level `mcpServers` object. Use `command`/`args` for local servers or `url` for hosted servers.
- Kiro CLI settings: `~/.kiro/settings/cli.json`
  - CLI behavior toggles (small JSON key/value settings).
- Kiro agents: `~/.kiro/agents/`
  - Agent definitions and prompts. JSON files with agent name, description, prompts, tools, and optional hooks.
- Kiro hooks: `~/.kiro/hooks/`
  - Workflow hooks triggered by IDE events. JSON files with hook metadata and instructions.
- Kiro steering (global rules): `~/.kiro/steering/`
  - Global steering rules as Markdown. Use clear, focused files; avoid secrets.
- Kiro extensions: `~/.kiro/extensions/`
  - Extensions metadata and registry files.
- Kiro extensions registry: `~/.kiro/extensions/extensions.json`
  - List of installed extensions (JSON array).
- Kiro local args/state: `~/.kiro/argv.json`
  - Local runtime arguments/state (JSON).

## MCP Configuration Locations
- Kiro MCP config: `~/.kiro/settings/mcp.json`
- ai-cli MCP global config: `~/.ai.cli/mcp/mcp-global.json`
- ai-cli MCP runtime dir: `~/.ai-cli-mcp/`

## Structure Notes
- `mcp.json` uses JSON with `mcpServers` as the root key.
- Steering files are Markdown and should be short, focused, and reusable.
- Hooks and agents are JSON files; keep prompts and instructions concise.
- Workspace steering files live in `.kiro/steering/` and override global on conflict.

## Reference Links
- Steering (rules): https://kiro.dev/docs/steering/
- Specs: https://kiro.dev/docs/specs/
- Hooks (workflows): https://kiro.dev/docs/hooks/
- Commands (terminal integration): https://kiro.dev/docs/chat/terminal/
- Agents (chat overview): https://kiro.dev/docs/chat/
- MCP overview: https://kiro.dev/docs/mcp/
- MCP servers catalog: https://kiro.dev/docs/mcp/servers/
- MCP configuration: https://kiro.dev/docs/mcp/configuration/
- MCP usage: https://kiro.dev/docs/mcp/usage/

## Notes
- Keep secrets out of steering files and hooks.
- Prefer workspace steering for project-specific rules.
