# Persistent Memory Index

## File Index

- [lessons.md](lessons.md) - Lessons learned (global, shared across all sessions)

## User Environment

- System: Ubuntu Linux, Zsh
- Conda path: `$HOME/anaconda3`
- Main workspace: projects under `~/Desktop/`
- MCP installed: Context7, GitHub, Playwright (user scope)
- Permission mode: bypass permissions enabled

## GitHub

- Account: Mizoreww, gh CLI logged in
- Claude config repo: `Mizoreww/claude-code-config`, branches `main` (English) and `zh-CN` (Chinese)
- Git push: `GIT_SSH_COMMAND="ssh -o ConnectTimeout=10 -o ServerAliveInterval=5" git push`

## User Preferences

- Communicate in Chinese
- Give code directly, minimize questions
- Don't repeatedly suggest the same root cause

## Memory Structure

| Level | Path | Loaded when | Content |
|-------|------|-------------|---------|
| Global | `~/.claude/memory/` | Every conversation | Cross-project experience, preferences, lessons |
| Project | `~/.claude/projects/<path>/memory/` | Entering that directory | Project-specific context only |

- `lessons.md` exists only at global level, never at project level
- `CLAUDE.md` can only be modified when the user explicitly asks
