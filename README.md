# Codex Configuration

Production-ready configuration for Codex: global instructions, lessons-based self-improvement, layered coding standards via skills, MCP integration, and one-command bootstrap.

## Directory Structure

```
.
├── AGENTS.md              # Global instructions
├── config.toml            # Codex settings (model, permissions, MCP, lesson injection)
├── lessons.md             # Self-correction log template
└── install.sh             # One-command installer
```

## Quick Start

```bash
git clone -b codex https://github.com/Mizoreww/claude-code-config.git
cd claude-code-config
bash install.sh
```

Then restart Codex.

## Key Features

### Self-Improvement Loop

1. User correction is recorded into `~/.codex/lessons.md`
2. Next session loads lessons automatically
3. Stable patterns are promoted into `AGENTS.md`

### Auto Lesson Injection

`config.toml` sets:

```toml
model_instructions_file = "~/.codex/lessons.md"
```

This keeps correction memory active without extra startup hooks.

### Layered Rules

Rules are provided through skills (for example `claude-rules`, `python-patterns`, `golang-patterns`, `frontend-patterns`) so common principles and language-specific practices stay consistent.

### MCP Integration

The default setup includes:
- Lark MCP
- Context7 MCP
- GitHub MCP
- Playwright MCP

### Skill Bundle Bootstrap

`install.sh` installs a practical baseline from open-source ecosystems:
- superpowers
- everything-claude-code
- anthropic skills packs (document + examples)
- claude-mem
- AI research skill packs

## Notes

1. Fill your own credentials:
   - `YOUR_APP_ID` / `YOUR_APP_SECRET` (Lark)
   - `YOUR_GITHUB_PAT` (GitHub MCP)
2. Uses current Codex config style (`web_search = "live"`, top-level)
3. If `~/.codex/config.toml` already exists, merge manually

## License

MIT
