# Hermes Agent v0.21.2 - Build Edition

## Build Information

**Release:** v0.21.2 (v2026.9.11)  
**Build Date:** 2026-09-13  
**Base Repository:** NousResearch/hermes-agent  
**Commit:** 939e45c91d751fadd94dcd1b873ac3cb44846213  

## Installation Methods

### Method 1: Shell Installer (Recommended)

**Linux, macOS, WSL2, Termux:**
```bash
curl -fsSL https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.sh | bash
source ~/.bashrc
hermes
```

**Windows (Native, PowerShell):**
```powershell
iex (irm https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.ps1)
```

### Method 2: Manual Installation from Source

```bash
# Clone the repository
git clone https://github.com/Tahar0061/hermes-agent-build.git
cd hermes-agent-build

# Install uv (universal Python package manager)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Create virtual environment and install
uv venv ~/.hermes/venvs/hermes-dev --python 3.11
source ~/.hermes/venvs/hermes-dev/bin/activate
uv pip install -e ".[all,dev]"

# Run
hermes
```

### Method 3: Docker

```bash
# Build Docker image
docker build -t hermes-agent:v0.21.2 .

# Run container
docker run -it --rm \
  -v ~/.hermes:/root/.hermes \
  hermes-agent:v0.21.2 hermes
```

## Troubleshooting

### Windows Defender/Antivirus Issues

If `uv.exe` is quarantined as malware:

1. **Whitelist via PowerShell (Admin):**
   ```powershell
   Add-MpPreference -ExclusionPath "$env:LOCALAPPDATA\hermes\bin"
   ```

2. **Verify Authenticity:**
   ```powershell
   winget install --id GitHub.cli
   gh auth login
   
   $uv = "$env:LOCALAPPDATA\hermes\bin\uv.exe"
   $ver = (& $uv --version).Split(' ')[1]
   [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
   $zip = "$env:TEMP\uv.zip"
   Invoke-WebRequest "https://github.com/astral-sh/uv/releases/download/$ver/uv-x86_64-pc-windows-msvc.zip" -OutFile $zip -UseBasicParsing
   gh attestation verify $zip --repo astral-sh/uv
   Expand-Archive $zip "$env:TEMP\uv_x" -Force
   (Get-FileHash "$env:TEMP\uv_x\uv.exe").Hash -eq (Get-FileHash $uv).Hash
   ```

### Common Issues

#### "Command not found: hermes"
Reload your shell: `source ~/.bashrc` or `source ~/.zshrc`

#### "Python 3.11+ required"
Install Python 3.11-3.13. The installer handles this automatically.

#### "state.db corrupted"
Run the recovery tool:
```bash
hermes doctor
hermes sessions recover --inspect-only
```

## Key Dependencies

**Core (Always Installed):**
- Python 3.11-3.13
- OpenAI SDK 2.24.0
- Pydantic 2.13.4
- Rich 14.3.3
- Prompt Toolkit 3.0.52
- FastAPI 0.104+
- Uvicorn 0.31+

**Optional (Lazy-Installed):**
- Anthropic SDK (for Claude)
- Firecrawl (web search)
- Edge-TTS (text-to-speech)
- Discord.py (Discord gateway)
- Mautrix (Matrix gateway)
- Faster-Whisper (voice input)

## Configuration

### First-Time Setup

```bash
hermes setup
```

Guided wizard covers:
1. **Model & Provider** — Choose inference provider (Nous Portal, OpenRouter, OpenAI, etc.)
2. **Text-to-Speech** — TTS provider selection
3. **Terminal Backend** — Local, SSH, Docker, Modal, etc.
4. **Messaging Platforms** — Telegram, Discord, Slack, WhatsApp, Signal
5. **Tools** — Enable/disable capabilities
6. **Telemetry** — Optional metrics and sending
7. **Agent Settings** — Iterations, compression, display mode

### Configuration Files

**Location:** `~/.hermes/` (UNIX) or `%LOCALAPPDATA%\hermes` (Windows)

- `config.yaml` — Agent configuration
- `.env` — API keys and secrets
- `state.db` — Sessions and memory (SQLite)
- `backups/` — Config backups
- `logs/` — Agent and tool call logs
- `skills/` — Custom and imported skills

### Quick Config Commands

```bash
# View settings
hermes config get model.provider

# Set values
hermes config set model.provider openrouter
hermes config set model.default gpt-4-turbo

# Edit in editor
hermes config edit

# See all
hermes config show
```

## Updates

```bash
# Check for updates
hermes update --check

# Update to latest
hermes update

# Rollback if needed
hermes update --version v0.20.0
```

## Monitoring & Logs

```bash
# View agent logs
tail -f ~/.hermes/logs/agent.log

# View tool calls
cat ~/.hermes/logs/tool_calls.log

# See debug info
hermes doctor

# Export session for sharing
hermes debug share
```

## Platform-Specific Notes

### Windows
- Native Windows fully supported (no WSL2 required)
- Git Bash (MinGit) bundled if Git not installed
- `uv.exe` may trigger Windows Defender (see troubleshooting)
- Portable installation to `%LOCALAPPDATA%\hermes`

### macOS
- Both Intel and Apple Silicon supported
- Requires Xcode Command Line Tools
- SSH and remote execution work natively

### Linux
- All major distros supported (Ubuntu, Debian, Fedora, Arch, etc.)
- WSL2 on Windows works identically to native Linux
- SSH and container backends fully functional

### Termux (Android)
- Tested on Android 10+
- Use `install.sh` from WSL2/Linux guide
- See full guide: [Termux Documentation](https://hermes-agent.nousresearch.com/docs/getting-started/termux)

## Performance Optimization

### Speed Up First Run
```bash
# Skip optional components
hermes setup --non-interactive

# Or use quick setup
hermes setup --quick
```

### Reduce Memory Usage
```yaml
# In ~/.hermes/config.yaml
agent:
  max_turns: 50  # Lower max iterations
  memory_limit_mb: 1024
```

### Enable Hardware Acceleration
```yaml
model:
  provider: local  # Run models locally with GPU
  base_url: http://localhost:8000/v1
```

## Backup & Recovery

```bash
# Automatic backups (kept in ~/.hermes/backups/)
hermes backup

# Restore from backup
hermes backup --restore ~/.hermes/backups/config/config.yaml.bak

# Database recovery
hermes doctor --fix
hermes sessions recover --inspect-only
```

## Development

### Contributing

See [CONTRIBUTING.md](https://github.com/NousResearch/hermes-agent/blob/main/CONTRIBUTING.md)

### Running Tests

```bash
cd hermes-agent-build
uv pip install -e ".[all,dev]"
scripts/run_tests.sh
```

### Building From Source

```bash
# Full build
uv build

# Wheel only
python -m build --wheel

# Editable install
uv pip install -e "."
```

## Support & Community

- **GitHub Issues:** [NousResearch/hermes-agent/issues](https://github.com/NousResearch/hermes-agent/issues)
- **Discord:** [Nous Research Community](https://discord.gg/NousResearch)
- **Skills Hub:** [agentskills.io](https://agentskills.io)
- **Docs:** [hermes-agent.nousresearch.com/docs](https://hermes-agent.nousresearch.com/docs/)

## Release Notes

### v0.21.2 Highlights

**State Database Reliability** - 44 issues closed
- No more second-writer corruption
- Healthy WAL databases stable
- FTS errors don't kill conversations
- Corrupt rows handled gracefully
- Profile isolation enforced
- Instant database opens (0.01s vs 4-20s)

**New Capabilities**
- Password-blind credential vault (1Password, Bitwarden)
- Curated plugin catalog with SHA pinning
- Free Nous tier with guided onboarding
- Multi-profile isolation hardening

**Bug Fixes**
- Desktop backend spawn storms eliminated
- Provider credential routing fixed
- Bedrock model stability improved
- CLI session resume working
- Update checks optimized
- 60+ Desktop UI fixes

**Migration from v0.21.1**
```bash
hermes update
# Or
hermes claw migrate  # If coming from OpenClaw
```

## Version History

| Version | Date | Key Changes |
|---------|------|-------------|
| v0.21.2 | 2026-09-11 | State.db fixes, multi-profile isolation, plugin catalog |
| v0.21.1 | 2026-09-07 | Session stability improvements |
| v0.21.0 | 2026-09-04 | Major session store rewrite |
| v0.20.6 | 2026-08-29 | Desktop improvements, bug fixes |

## License

MIT License — See [LICENSE](LICENSE)

Built by [Nous Research](https://nousresearch.com)
