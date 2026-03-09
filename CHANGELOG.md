# Changelog

## [1.3.0] - 2026-03-09

### Features
- Full uninstall now includes plugins and MCP by default (previously omitted)
- Install warning tracking: failed merges or plugin installs now skip version stamp and report warning count
- Uninstall backs up `settings.json` to `settings.json.bak` before removal
- `--all` flag now composes with other flags (e.g., `--all --mcp` installs everything plus MCP)
- Windows installer checks bash availability and warns if missing (required by statusline and hooks)
- Adversarial review skill no longer requires missing `brain/principles.md`; uses `reviewer-lenses.md` as self-contained source

### Bug Fixes
- VERSION environment variable sanitized to prevent command injection in remote install
- Repeated install no longer creates nested directories (e.g., `paper-reading/paper-reading/`)
- `stat` fallback order fixed: Linux `stat -c %Y` tried first, macOS `stat -f %m` as fallback
- Windows installer missing `tokenization` plugin in AI Research group (5/6 → 6/6)

### Documentation
- Self-improvement loop wording clarified: "auto-saved" → "Claude writes corrections driven by CLAUDE.md instructions"
- Uninstall examples annotated with "(incl. plugins & MCP)"
- Manual plugin install docs updated with all marketplace `add` commands and `name@marketplace` syntax

### Design Rationale
- Warning tracking prevents users from believing a partially-failed install is current
- Settings backup on uninstall prevents accidental loss of user-owned config merged by the installer
- VERSION sanitization closes a real attack vector in the remote install path (`bash -c` with untrusted input)

### Notes & Caveats
- `bypassPermissions` default unchanged (power-user config by design)
- Adversarial review still requires opposite CLI (`codex`/`claude`) — this is by design, not a bug

## [1.2.0] - 2026-03-07

### Features
- Windows support with PowerShell installer (`install.ps1`)
- Adversarial code review skill (cross-model review via opposite AI CLI)
- Tokenization plugin added to AI Research skill group (huggingface-tokenizers, sentencepiece)
- Cross-platform web search date instruction (system command with fallback)
- Codex branch link in README navigation

### Bug Fixes
- Statusline non-blocking for third-party API users
- Bash 3.2 compatibility (replace associative array with string matching)
- Retry logic (5 attempts) for network operations in installer
- Fallback to expired cache when usage API is rate-limited

### Design Rationale
- PowerShell installer mirrors bash installer logic for Windows parity
- Adversarial review replaces codex-cli MCP — cross-model challenge produces higher quality reviews than same-model delegation
- Web search date instruction ensures queries include current year by verifying system clock first

### Notes & Caveats
- PowerShell installer requires `winget` for `jq`/`gh` dependencies
- Adversarial review requires the opposite CLI installed (`codex` for Claude users, `claude` for Codex users)
- GitHub redirect from old repo name (`claude-code-config`) still works but canonical URL is now `awesome-claude-code-config`

## [1.1.0] - 2026-03-05

### Features
- Gradient statusline showing model, cost, and context usage
- Version changelog policy in CLAUDE.md
- Project renamed to `awesome-claude-code-config`
- Backup logic removed from installer (replaced by smart merge)

### Design Rationale
- Statusline provides at-a-glance session awareness without interrupting workflow
- Changelog policy ensures design decisions are traceable alongside code

### Notes & Caveats
- Statusline reads from OS keychain for API credentials — requires keychain access
- Rename may break existing bookmarks; GitHub redirect handles this transparently

## [1.0.0] - 2026-03-02

### Features
- Installer overhaul: remote install, smart merge, plugin groups, uninstall, version management
- Enhanced paper-reading skill with depth-first analysis and multi-perspective evaluation
- Code Review rule in CLAUDE.md
- Codex CLI MCP server integration

### Design Rationale
- Plugin-first architecture: skills installed from open-source ecosystems rather than bundled
- Smart merge preserves user customizations during upgrades
- Paper-reading skill uses Andrew Ng's three-perspective framework for balanced evaluation

### Notes & Caveats
- Plugin installer requires Python 3 and network access to GitHub
- MCP servers require separate credential configuration (Lark, GitHub PAT)

## [0.1.0] - 2026-02-25

### Features
- Initial release with CLAUDE.md global instructions
- Memory system with lessons-based self-correction loop
- Plugin marketplace with AI research, MCP servers, and paper-reading skill
- Feishu/Lark MCP and Context7 integration
- Installer with plugin group support

### Design Rationale
- Lessons-driven self-improvement: corrections recorded → auto-injected → stable patterns promoted to CLAUDE.md
- Plugin marketplace separates concern: CLAUDE.md manages behavior, plugins provide domain skills

### Notes & Caveats
- First public release — API and configuration format may change
