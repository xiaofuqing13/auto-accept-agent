# Auto Accept Agent

**English** | [中文](README.md)

A VS Code / Antigravity / Cursor extension that auto-accepts AI agent actions, so you don't have to click approve every few seconds.

---

## Features

- Auto-accept 14 action types: file edits, terminal commands, retries, etc.
- Configurable — pick which actions to auto-accept in the settings panel
- Background mode for managing multiple conversation tabs at once
- Built-in dangerous command blocking (e.g. `rm -rf /`)
- Status bar indicator for real-time state
- Auto-detects CDP debugging port
- English and Simplified Chinese support

## Installation

1. Download the `.vsix` file
2. Open your IDE, press `Ctrl+Shift+P`, type `Install from VSIX`
3. Select the file and restart

## Usage

Click `Auto Accept: OFF` in the status bar to enable. On first use, allow the shortcut update (adds `--remote-debugging-port=9000`). After that it runs on its own.

## Configuration

| Setting | Description | Default |
|---------|-------------|---------|
| CDP Port | Debug protocol port | Auto-detect |
| Auto Accept File Edits | Auto-apply file changes | Enabled |
| Language Override | Force UI language | Auto |
| Overlay Mode | Background mode display | Disabled |
| Action Types | Which actions to auto-accept | Run only |

## Compatibility

Works with VS Code, Antigravity, and Cursor on Windows, macOS, and Linux. Supports multiple windows, multiple instances, and works fine when minimized or unfocused.

## License

[MIT](LICENSE.md)
