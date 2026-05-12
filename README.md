# coree for Kiro

Persistent memory and code intelligence for AI agents in [Kiro](https://kiro.dev).

## Install

### Workspace scope (recommended)

Copy `.kiro/settings/mcp.json` from this repo into your project root:

```sh
mkdir -p .kiro/settings
curl -fsSL https://raw.githubusercontent.com/coree-ai/kiro/main/.kiro/settings/mcp.json \
  -o .kiro/settings/mcp.json
```

Kiro picks up workspace settings automatically. Restart Kiro after copying.

### Global scope

To enable coree for all projects, copy the config to `~/.kiro/settings/mcp.json`:

```sh
mkdir -p ~/.kiro/settings
curl -fsSL https://raw.githubusercontent.com/coree-ai/kiro/main/.kiro/settings/mcp.json \
  -o ~/.kiro/settings/mcp.json
```

Workspace settings take precedence over global settings.

### Via Kiro UI

Open Kiro settings and navigate to **MCP Servers** to add the server via the UI.
Use the following values:

- **Command**: `npx`
- **Args**: `--yes @coree-ai/coree@0.13.0 serve`

## Config Reference

The `.kiro/settings/mcp.json` in this repo includes Kiro-specific fields:

| Field | Value | Description |
|-------|-------|-------------|
| `disabled` | `false` | Enables the server at startup |
| `autoApprove` | (list) | Tool names that don't need user confirmation |
| `disabledTools` | `[]` | No tools excluded |

The `autoApprove` list covers all coree tools so the agent can read and store
memories without prompting you on every call:

```
search, search_code, search_memory, store_memories, get_memories,
list_memories, capture_note, get_symbol, session_context,
list_stale_memories, evict_stale_memories, pin_memories, delete_memories
```

## Environment Variables

Set these in your shell profile:

| Variable | Description |
|----------|-------------|
| `COREE__MEMORY__REMOTE_AUTH_TOKEN` | Auth token for remote memory sync |
| `COREE__MEMORY__REMOTE_URL` | Remote memory database URL |
| `COREE__INDEX__REMOTE_AUTH_TOKEN` | Auth token for remote index sync |
| `COREE__INDEX__REMOTE_URL` | Remote index database URL |

Kiro inherits env vars from the shell that launched it. Variable substitution
`${VAR}` in the config file uses values from the environment at startup.

## Verify

Open Kiro and start an agent session. Ask: `What coree tools are available?`

The agent should list tools like `search`, `store_memories`, `capture_note`, etc.

## Requirements

- [Node.js](https://nodejs.org) 18+ with `npx` on `PATH`
- Kiro with MCP server support

## Version Bumping

```sh
node scripts/bump-version.mjs 0.14.0
```

Updates version references in `.kiro/settings/mcp.json` and `README.md`.
