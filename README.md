# Vexscan for Claude Code

Security scanner plugin for Claude Code that protects your environment from malicious plugins, skills, MCPs, and hooks.

## Features

- **Automatic Scanning**: Scans third-party plugins on session start
- **AI-Powered Analysis**: Uses your Claude session to analyze findings and filter false positives
- **Pre-Install Vetting**: Vet plugins before installing with `/vexscan:vet`
- **Smart Filtering**: Skips official plugins, focuses on untrusted code

## Installation

### From GitHub (Recommended)

```bash
# Add the marketplace
/plugin marketplace add edimuj/vexscan-claude-code

# Install the plugin
/plugin install vexscan
```

### Manual Installation

```bash
git clone https://github.com/edimuj/vexscan-claude-code.git ~/.claude/plugins/vexscan
```

## Usage

### Commands

- `/vexscan:scan` - Scan all installed plugins with AI analysis
- `/vexscan:scan ~/.claude/plugins/some-plugin` - Scan specific path
- `/vexscan:vet https://github.com/user/plugin` - Vet a plugin before installing

### Automatic Scanning

On session start, Vexscan automatically scans your plugins directory and alerts you to any findings:

```
[Vexscan] SECURITY ALERT: Found 2 critical, 5 high issues in plugins/skills.
Run /vexscan:scan for AI-powered analysis.
```

## What It Detects

| Category | Examples |
|----------|----------|
| Code Execution | `eval()`, `new Function()`, `exec()` |
| Shell Injection | `child_process.exec()`, subprocess calls |
| Data Exfiltration | Discord webhooks, external POST requests |
| Credential Access | SSH keys, AWS credentials, API tokens |
| Prompt Injection | Instruction override attempts |
| Obfuscation | Base64, hex, unicode encoding |

## Requirements

The plugin automatically installs the Vexscan CLI on first use. For manual installation:

```bash
# macOS/Linux
curl -fsSL https://raw.githubusercontent.com/edimuj/vexscan/main/install.sh | bash

# Or build from source
cargo install --git https://github.com/edimuj/vexscan
```

## Configuration

The plugin works out of the box with sensible defaults:

- Scans `~/.claude` directory
- Skips official Anthropic plugins (`--third-party-only`)
- Skips `node_modules` (`--skip-deps`)
- Reports medium severity and above
- 2 minute timeout for large scans

## Related Projects

- [Vexscan CLI](https://github.com/edimuj/vexscan) - The core security scanner
- [Vexscan for OpenClaw](https://www.npmjs.com/package/@exelerus/vexscan-openclaw) - OpenClaw plugin

## License

Apache 2.0
