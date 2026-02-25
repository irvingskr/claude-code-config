# MCP Servers

Recommended MCP (Model Context Protocol) servers for Claude Code.

## Included Servers

| Server | Transport | Purpose |
|--------|-----------|---------|
| **Context7** | stdio | Injects up-to-date, version-specific library documentation into context |
| **GitHub** | http | Manage PRs, issues, code reviews, and CI/CD directly from Claude Code |
| **Playwright** | stdio | Browser automation, E2E testing, screenshots, form filling |

## Installation

### Quick (via install script)

```bash
./install.sh --mcp
```

### Manual

```bash
# Context7 — Up-to-date library docs
claude mcp add --scope user --transport stdio context7 -- npx -y @upstash/context7-mcp@latest

# GitHub — PR/Issue management (requires OAuth: run /mcp in Claude Code after install)
claude mcp add --scope user --transport http github https://api.githubcopilot.com/mcp/

# Playwright — Browser automation & E2E testing
claude mcp add --scope user --transport stdio playwright -- npx -y @playwright/mcp@latest
```

### From JSON config

```bash
# Import all servers at once using the provided config
python3 -c "
import json
with open('mcp-servers.json') as f:
    servers = json.load(f)
for name, config in servers.items():
    print(f'Server: {name} ({config[\"type\"]})')
"
```

## Post-Install

1. **Restart Claude Code** for MCP servers to take effect
2. **GitHub OAuth**: Run `/mcp` inside Claude Code, select GitHub, and authenticate in browser
3. **Verify**: Run `/mcp` to check all servers are connected

## Adding More Servers

Edit `mcp-servers.json` or use the CLI:

```bash
# Example: Add Sentry for error monitoring
claude mcp add --scope user --transport http sentry https://mcp.sentry.dev/mcp

# Example: Add a database server
claude mcp add --scope user --transport stdio db -- npx -y @bytebase/dbhub \
  --dsn "postgresql://user:pass@host:5432/dbname"
```

## Scope Options

| Scope | Flag | Stored In | Visibility |
|-------|------|-----------|------------|
| Local (default) | `--scope local` | `~/.claude.json` (per-project) | You only, current project |
| User | `--scope user` | `~/.claude.json` (global) | You only, all projects |
| Project | `--scope project` | `.mcp.json` (repo root) | All team members |
