# Hermes Agent v0.21.2 (v2026.9.11) - Build Edition

**The Self-Improving AI Agent by Nous Research**

This is the complete, production-ready build of Hermes Agent v0.21.2 with critical stability fixes for `state.db`, multi-profile isolation hardening, and enhanced credential management.

## 🚀 Quick Start

### Installation

**Linux, macOS, WSL2:**
```bash
curl -fsSL https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.sh | bash
```

**Windows (PowerShell):**
```powershell
iex (irm https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.ps1)
```

**After Installation:**
```bash
source ~/.bashrc    # reload shell (or: source ~/.zshrc)
hermes              # start chatting!
```

## ✨ What's New in v0.21.2

### State Database Reliability (44 issues closed)
- ✅ No more corrupt `state.db` from second writers
- ✅ Healthy WAL databases stop wedging
- ✅ FTS damage no longer kills conversations
- ✅ One corrupt row no longer kills `sessions list`
- ✅ Sessions never bind to another profile's database
- ✅ Opening `state.db` no longer locks when nothing needs writing

### Multi-Profile Isolation
- ✅ Secondary profiles don't inherit default profile allow-lists
- ✅ Adapters don't send credentials to default profile
- ✅ Stdio MCP servers don't receive vault secrets from other profiles
- ✅ MEDIA delivery can't attach another profile's files

### Desktop Backend Improvements
- ✅ No more spawn storms
- ✅ Profile switches don't create duplicates
- ✅ Stable bot mode with proper lifecycle

### New Features
- 🔐 **Password-blind credential vault** - Sign in and fill forms from 1Password/Bitwarden without seeing secrets
- 🔌 **Plugin Catalog** - Curated, SHA-pinned plugins with one Plugins page
- 🎯 **Nous Free Tier** - Free inference + connectors with one command
- 🌐 **Guided First Launch** - Easy onboarding for new users

## 📋 System Requirements

- **Python:** 3.11 - 3.13
- **OS:** Linux, macOS, Windows (native or WSL2), or Termux
- **Disk:** ~2GB for base install + models
- **RAM:** 4GB minimum (8GB+ recommended for complex tasks)

## 🎯 Key Features

| Feature | Description |
|---------|-------------|
| **Real Terminal Interface** | Full TUI with multiline editing, slash-commands, history, streaming output |
| **Lives Where You Do** | Telegram, Discord, Slack, WhatsApp, Signal, CLI — all from one gateway |
| **Closed Learning Loop** | Creates and improves skills from experience automatically |
| **Scheduled Automations** | Cron scheduler with natural language configuration |
| **Parallel Execution** | Spawn subagents for multi-task workflows |
| **Universal Deployment** | Local, Docker, SSH, Singularity, Modal, Daytona, Vercel Sandbox |
| **Research-Ready** | Batch trajectory generation for model training |

## 🔑 Quick Commands

```bash
hermes                      # Start interactive chat
hermes model                # Change inference provider/model
hermes tools                # Configure tools and permissions
hermes config set           # Set individual config values
hermes gateway              # Start messaging gateway
hermes setup                # Run full setup wizard
hermes update               # Update to latest version
hermes doctor               # Diagnose issues
```

## 📚 Documentation

Full documentation at: [hermes-agent.nousresearch.com/docs](https://hermes-agent.nousresearch.com/docs/)

### Key Sections:
- [Quickstart](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart)
- [CLI Usage](https://hermes-agent.nousresearch.com/docs/user-guide/cli)
- [Configuration](https://hermes-agent.nousresearch.com/docs/user-guide/configuration)
- [Messaging Gateway](https://hermes-agent.nousresearch.com/docs/user-guide/messaging)
- [Tools & Toolsets](https://hermes-agent.nousresearch.com/docs/user-guide/features/tools)
- [Skills System](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills)

## 🔐 Security & Privacy

- **Local-First:** Data stays on your machine
- **Permission Model:** Approve dangerous operations before execution
- **Isolated Containers:** Run untrusted code safely
- **Credential Vault:** Secure storage with password-less access

## 🎨 Providers & Models

Connect to any provider:
- **Nous Portal** - Free models + tool gateway
- **OpenRouter** - 300+ models, unified API
- **OpenAI** - GPT-4, GPT-4 Turbo, Vision
- **Anthropic** - Claude 3 family
- **Azure, Bedrock, Vertex** - Enterprise options
- **Local Inference** - Run Hermes offline

## 📊 947 Commits, 312 PRs, 140 Contributors

Since v0.21.1, this release contains:
- **182,504 lines added** | **15,564 lines removed**
- **1,869 files changed**
- **44 state.db issues closed**

## 🐛 Bug Fixes Summary

- Gateway & platforms: Fixed bare `display:` crashes, WebSocket stalls, first-turn delays
- Providers & routing: Auto-switch improvements, Bedrock stability, OAuth refresh fixes
- Agent loop: Compression timeouts fixed, context overflow handling, prompt cache preservation
- CLI/TUI/Desktop: Session resume fixed, terminal keybindings, update checks optimized, 60+ Desktop fixes
- Cron & Kanban: Manual runs, cloning, review workflows
- Tools & memory: MCP robustness, memory truncation fixes, tool search accuracy
- Housekeeping: Config backups, archive cleanup, sharing retention

## 🤝 Community

- 💬 [Discord](https://discord.gg/NousResearch)
- 📚 [Skills Hub](https://agentskills.io)
- 🐛 [Issues](https://github.com/NousResearch/hermes-agent/issues)
- 🔌 [MCP Servers](https://github.com/avifenesh/computer-use-linux)

## 📄 License

MIT — See [LICENSE](LICENSE) for details.

Built by [Nous Research](https://nousresearch.com).

---

**Version:** 0.21.2 (v2026.9.11)  
**Release Date:** September 11, 2026  
**Repository:** [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)  
**Build Origin:** [Tahar0061/hermes-agent-build](https://github.com/Tahar0061/hermes-agent-build)
