# Plugins (Skills Marketplaces)

Claude Code supports plugins from community marketplaces. This directory contains the configuration and installation guide for recommended plugins.

## Installed Plugins

### Marketplaces

| Marketplace | GitHub Repo | Description |
|-------------|-------------|-------------|
| **anthropic-agent-skills** | [anthropics/skills](https://github.com/anthropics/skills) | Official Anthropic skills (document handling, design) |
| **superpowers-marketplace** | [obra/superpowers-marketplace](https://github.com/obra/superpowers-marketplace) | Brainstorming, debugging, code review, TDD workflows |
| **everything-claude-code** | [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) | Comprehensive dev toolkit (TDD, security, database, patterns) |
| **ai-research-skills** | [zechenzhangAGI/AI-research-SKILLs](https://github.com/zechenzhangAGI/AI-research-SKILLs) | ML/AI research tools (fine-tuning, serving, distributed training) |
| **claude-plugins-official** | [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official) | Official Claude plugins |

### Individual Plugins

| Plugin | Marketplace | What It Does |
|--------|-------------|--------------|
| **superpowers** | superpowers-marketplace | Brainstorming, systematic debugging, code review, git worktrees, plan writing |
| **everything-claude-code** | everything-claude-code | TDD guide, security review, database patterns, Go/Python/Spring Boot patterns |
| **document-skills** | anthropic-agent-skills | PDF, DOCX, PPTX, XLSX creation and manipulation |
| **example-skills** | anthropic-agent-skills | Frontend design, MCP builder, canvas design, algorithmic art |
| **fine-tuning** | ai-research-skills | Axolotl, LLaMA-Factory, PEFT, Unsloth fine-tuning guides |
| **post-training** | ai-research-skills | GRPO, RLHF, DPO, SimPO post-training guides |
| **inference-serving** | ai-research-skills | vLLM, SGLang, TensorRT-LLM, llama.cpp serving guides |
| **distributed-training** | ai-research-skills | DeepSpeed, FSDP, Megatron-Core, Ray Train guides |
| **optimization** | ai-research-skills | AWQ, GPTQ, GGUF, Flash Attention, bitsandbytes quantization |

## Installation

### Quick (via install script)

```bash
./install.sh --plugins
```

### Manual

```bash
# Step 1: Add marketplaces
claude plugin marketplace add https://github.com/anthropics/skills
claude plugin marketplace add https://github.com/obra/superpowers-marketplace
claude plugin marketplace add https://github.com/affaan-m/everything-claude-code
claude plugin marketplace add https://github.com/zechenzhangAGI/AI-research-SKILLs
claude plugin marketplace add https://github.com/anthropics/claude-plugins-official

# Step 2: Install plugins from each marketplace
# Anthropic skills
claude plugin install document-skills --marketplace anthropic-agent-skills
claude plugin install example-skills --marketplace anthropic-agent-skills

# Superpowers
claude plugin install superpowers --marketplace superpowers-marketplace

# Everything Claude Code
claude plugin install everything-claude-code --marketplace everything-claude-code

# AI Research (multiple plugins from same marketplace)
claude plugin install fine-tuning --marketplace ai-research-skills
claude plugin install post-training --marketplace ai-research-skills
claude plugin install inference-serving --marketplace ai-research-skills
claude plugin install distributed-training --marketplace ai-research-skills
claude plugin install optimization --marketplace ai-research-skills
```

### Enable in settings.json

After installing, ensure plugins are enabled in `~/.claude/settings.json`:

```json
{
  "enabledPlugins": {
    "document-skills@anthropic-agent-skills": true,
    "example-skills@anthropic-agent-skills": true,
    "superpowers@superpowers-marketplace": true,
    "fine-tuning@ai-research-skills": true,
    "post-training@ai-research-skills": true,
    "inference-serving@ai-research-skills": true,
    "distributed-training@ai-research-skills": true,
    "optimization@ai-research-skills": true,
    "everything-claude-code@everything-claude-code": true
  }
}
```

## Which Plugins Should I Install?

| Your Focus | Recommended Plugins |
|------------|-------------------|
| **General development** | superpowers, everything-claude-code |
| **Document creation** | document-skills, example-skills |
| **ML/AI research** | fine-tuning, post-training, inference-serving, optimization |
| **Large-scale ML** | distributed-training, optimization |
| **All-in-one** | All of the above |
