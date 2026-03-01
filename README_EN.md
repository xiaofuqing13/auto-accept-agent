# Auto Accept Agent

**English** | [中文](README.md)

> A VS Code / Antigravity / Cursor extension that automatically accepts AI agent actions, freeing you from constant manual approvals.

---

## ✨ Features

- **Auto Accept Actions** — Supports 14 action types including file edits, terminal commands, retries, etc.
- **Configurable Actions** — Select which actions to auto-accept via the settings panel
- **Background Mode** — Manage multiple AI conversation tabs simultaneously
- **Dangerous Command Blocking** — Built-in protection against destructive commands like `rm -rf /`
- **Real-time Status** — Status bar color indicators (purple = running, green = complete)
- **Smart Port Detection** — Auto-scans CDP debugging ports, no manual config needed
- **Multi-language** — Auto-detects IDE language, supports English and Simplified Chinese

## 📦 Installation

1. Download the latest `.vsix` file
2. Open VS Code / Antigravity / Cursor
3. `Ctrl+Shift+P` → type `Install from VSIX`
4. Select the `.vsix` file and restart IDE

## 🚀 Usage

1. Click `Auto Accept: OFF` in the status bar to enable
2. Allow the one-time shortcut update (adds `--remote-debugging-port=9000`)
3. Once enabled, it runs automatically — status bar shows `Auto Accept: ON`

## ⚙️ Configuration

| Setting | Description | Default |
|---------|-------------|---------|
| CDP Port | Debug protocol port | Auto-detect |
| Auto Accept File Edits | Auto-apply file changes | Enabled |
| Language Override | Force UI language | Auto |
| Overlay Mode | Background mode display | Disabled |
| Action Types | Select actions to auto-accept | Run only |

## 🖥️ Compatibility

- ✅ VS Code / Antigravity / Cursor
- ✅ Windows / macOS / Linux
- ✅ Multiple windows / instances
- ✅ Minimized / unfocused

## 📄 License

[MIT](LICENSE.md)
