# Global Instructions

## Thinking Mode

- Use ultrathink extended thinking mode by default

## Language Preferences

- All responses and explanations in the user's preferred language
- Code comments may use English
- Keep standard English for technical terms (API, Git, Docker, etc.)

## Shell Environment

- Default Shell: **Zsh**
- Config file: `~/.zshrc`

## Conda Environment Usage

**Important**: Before running any Python script, activate the conda environment:

```bash
# Conda path
CONDA_PATH="$HOME/anaconda3"

# List available environments
$HOME/anaconda3/bin/conda env list

# Activate environment (in Zsh)
source $HOME/anaconda3/etc/profile.d/conda.sh && conda activate <env_name>

# Or use the environment's Python directly
$HOME/anaconda3/envs/<env_name>/bin/python script.py
```

## Proxy & Network Configuration

- Remote server proxies are typically configured via SSH reverse port forwarding
- Do not modify `.bashrc`, `.profile`, or VSCode settings to configure proxies unless explicitly asked
- Standard approach: `ssh -R <remote_port>:127.0.0.1:<local_port>`, then set `http_proxy`/`https_proxy` to `http://127.0.0.1:<remote_port>`
- When no `sudo` access, prefer user-space installation methods

## Communication Preferences

- When the user explicitly says a cause is **not** the problem, **immediately stop** exploring that direction and pivot to other possibilities
- Prefer providing concrete code implementations over asking repeated questions. If the user has made the same request multiple times, just write the code with reasonable assumptions noted in comments

## Date Awareness

- At the start of each conversation, check the current date
- All web searches must use the current date as context to ensure up-to-date results
- When searching for documentation, news, or recent developments, include the current year in search queries

## Self-Improvement Loop

### What counts as a "correction" (low threshold)
- User directly points out an error
- User says "remember", "don't do ... again", "last time you ..."
- User's tone conveys frustration or repeats the same request
- Same operation fails 2+ times (e.g., connection, push, build)
- **When in doubt whether it's a correction, treat it as one**

### Mandatory post-correction flow
1. **First action**: write to global `memory/lessons.md` (date, context, mistake, rule) — before doing anything else
2. The "rule" must be a concrete instruction to prevent recurrence, not vague reflection
3. Only after writing lessons.md, continue handling the user's request

### Memory hierarchy
- `memory/lessons.md`: first landing point for all lessons, write anytime (global only, never project-level)
- `memory/MEMORY.md`: at each new session start, summarize recurring items from lessons.md into this file
- `CLAUDE.md`: only modify when the user **explicitly asks** — never self-promote rules

## Workflow Guidelines

- **Plan Mode First**: Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- **Re-plan on Deviation**: If implementation drifts from the plan, stop and re-plan — don't keep pushing
- **Subagent Strategy**: Use subagents for research, exploration, and parallel analysis to keep main context clean; one task per subagent
- **Verification Before Done**: Never mark a task complete without proving it works. Run tests, check logs, demonstrate correctness
- **Autonomous Bug Fixing**: When given a bug report, just fix it. Point at logs, errors, failing tests — then resolve them. Zero context switching required from the user

## Paper Reading Standards

When asked to read/summarize research papers:
1. Prefer HTML version from `ar5iv.labs.arxiv.org` (replace `arxiv.org/abs/` with `ar5iv.labs.arxiv.org/html/`); use PDF as fallback when ar5iv is unavailable
2. Use Playwright to screenshot important figures (architecture diagrams, experiment results, etc.), save to `images/` subdirectory and embed in the summary markdown
3. Provide structured summary: problem definition, method, key contributions, architecture, experimental results
4. Include concrete examples and equations, not just abstract descriptions
5. If full content cannot be retrieved, say so immediately — don't repeatedly try failed approaches
