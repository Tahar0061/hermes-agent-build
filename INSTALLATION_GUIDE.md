# Hermes Agent Installation Guide

## One-Line Installation

### Linux, macOS, WSL2, Termux
```bash
curl -fsSL https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.sh | bash
```

### Windows (PowerShell)
```powershell
iex (irm https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.ps1)
```

## After Installation

```bash
source ~/.bashrc    # Linux/macOS/WSL2 (or: source ~/.zshrc)
hermes              # Start the agent
```

## What Gets Installed

✅ **Python 3.11+** (if not present)  
✅ **uv** (Python package manager)  
✅ **Node.js** (for some tools)  
✅ **ripgrep** (fast file search)  
✅ **ffmpeg** (media handling)  
✅ **Git Bash** (Windows only, MinGit)  

**Installation Location:**
- **Linux/macOS/WSL2:** `~/.hermes/`
- **Windows:** `%LOCALAPPDATA%\hermes\`
- **Disk Space:** ~2GB

## System Requirements

| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| **Python** | 3.11 | 3.13 |
| **RAM** | 4GB | 8GB+ |
| **Disk** | 2GB | 5GB+ |
| **OS** | Windows, macOS, Linux | Any |
| **Internet** | Required for setup | Recommended |

## Platform-Specific Details

### Windows (Native)

**Pros:**
- No WSL2 setup needed
- All features work natively
- Git Bash bundled automatically

**What's installed:**
- Portable Python in `%LOCALAPPDATA%\hermes\python`
- Git Bash (MinGit) in `%LOCALAPPDATA%\hermes\git`
- uv in `%LOCALAPPDATA%\hermes\bin\uv.exe`

**Firewall:**
If prompted, allow:
- Python in `%LOCALAPPDATA%\hermes\python`
- uv in `%LOCALAPPDATA%\hermes\bin`

### macOS

**Requirements:**
- Xcode Command Line Tools
  ```bash
  xcode-select --install
  ```
- Or install via Homebrew:
  ```bash
  brew install hermes-agent  # If formula available
  ```

**Apple Silicon (M1/M2/M3):**
Fully supported! Native arm64 wheels included.

### Linux

**Debian/Ubuntu:**
```bash
sudo apt update
sudo apt install curl git -y
curl -fsSL https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.sh | bash
```

**Fedora/RHEL:**
```bash
sudo dnf install curl git -y
curl -fsSL https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.sh | bash
```

**Arch:**
```bash
sudo pacman -S curl git
curl -fsSL https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.sh | bash
```

### WSL2 (Windows Subsystem for Linux)

1. **Enable WSL2:**
   ```powershell
   wsl --install
   # Restart your computer
   ```

2. **In WSL2 terminal:**
   ```bash
   curl -fsSL https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.sh | bash
   ```

**Advantages:**
- Full Linux environment on Windows
- Better performance than Docker
- SSH works natively

### Termux (Android)

```bash
pkg install curl
curl -fsSL https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.sh | bash
```

See full guide: [Termux Setup](https://hermes-agent.nousresearch.com/docs/getting-started/termux)

## Troubleshooting Installation

### "Permission denied" on Linux/macOS

```bash
# Make installer executable
chmod +x install.sh
./install.sh
```

### "curl: command not found"

**Linux:**
```bash
sudo apt install curl  # or: yum, dnf, pacman
```

**macOS:**
```bash
brew install curl
```

**Windows:**
Use PowerShell instead:
```powershell
iex (irm https://raw.githubusercontent.com/Tahar0061/hermes-agent-build/main/scripts/install.ps1)
```

### "hermes: command not found" after install

**Reload your shell:**
```bash
source ~/.bashrc    # or: ~/.zshrc, ~/.profile
```

**Check installation:**
```bash
which hermes
hermes --version
```

### "Python 3.11+ required"

The installer handles Python installation. If you have an issue:

```bash
# Check Python version
python3 --version

# Install newer Python
# Linux: sudo apt install python3.11
# macOS: brew install python@3.11
# Windows: Installer includes Python
```

### Windows Defender quarantines uv.exe

This is a **false positive**. uv is from Astral.

**Whitelist the folder (Admin):**
```powershell
Add-MpPreference -ExclusionPath "$env:LOCALAPPDATA\hermes\bin"
```

**Verify authenticity:**
See [Verification Instructions](README.md#windows-defender-or-antivirus-flags-uv-as-malware)

### "state.db" corruption on first launch

```bash
hermes doctor --fix
hermes sessions recover
```

### Still having issues?

1. **Check logs:**
   ```bash
   tail -f ~/.hermes/logs/agent.log
   ```

2. **Run diagnostics:**
   ```bash
   hermes doctor
   ```

3. **Get help:**
   - Discord: [Nous Research](https://discord.gg/NousResearch)
   - GitHub Issues: [hermes-agent/issues](https://github.com/NousResearch/hermes-agent/issues)

## Uninstallation

### Linux/macOS/WSL2
```bash
rm -rf ~/.hermes
# Remove from PATH (edit ~/.bashrc or ~/.zshrc)
```

### Windows
```powershell
Rmdir -Recurse -Force $env:LOCALAPPDATA\hermes
# Also remove from PATH in Environment Variables
```

### Termux
```bash
rm -rf ~/.hermes
```

## Updating

```bash
# Check for updates
hermes update --check

# Update to latest
hermes update

# Update to specific version
hermes update --version v0.21.1

# Rollback
hermes update --version v0.21.0
```

## First-Time Setup

After installation, run:

```bash
hermes setup
```

This wizard will guide you through:
1. **Model Provider** - Choose OpenAI, Anthropic, Nous Portal, local, etc.
2. **Text-to-Speech** - Optional TTS configuration
3. **Terminal Backend** - Local, SSH, Docker, etc.
4. **Messaging Platforms** - Telegram, Discord, Slack, etc. (optional)
5. **Tools** - Configure available tools
6. **Telemetry** - Anonymous metrics (optional)
7. **Agent Settings** - Iterations, display mode, compression

**Skip wizard:**
```bash
hermes setup --non-interactive
```

**Quick setup (existing install):**
```bash
hermes setup --quick
```

## Next Steps

✅ **Installation complete!**

1. **Start chatting:**
   ```bash
   hermes
   ```

2. **Configure providers:**
   ```bash
   hermes model  # Choose LLM provider
   hermes tools  # Enable/configure tools
   ```

3. **Read documentation:**
   - [Quick Start](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart)
   - [CLI Guide](https://hermes-agent.nousresearch.com/docs/user-guide/cli)
   - [Configuration](https://hermes-agent.nousresearch.com/docs/user-guide/configuration)

4. **Join community:**
   - Discord: [Nous Research](https://discord.gg/NousResearch)
   - Skills Hub: [agentskills.io](https://agentskills.io)

## Getting Help

- **Docs:** https://hermes-agent.nousresearch.com/docs
- **Discord:** https://discord.gg/NousResearch
- **GitHub:** https://github.com/NousResearch/hermes-agent
- **Issues:** https://github.com/NousResearch/hermes-agent/issues

---

**Version:** 0.21.2  
**Built by:** Nous Research  
**License:** MIT
