# Auto Accept Agent

**English** | [中文](README.md)

A VS Code / Antigravity / Cursor extension that communicates with the IDE frontend via Chrome DevTools Protocol, automatically detecting and clicking AI agent action buttons (run, accept, retry, etc.) to reduce manual intervention.

---

## How It Works

On activation, the extension walks the process tree upward to detect the `--remote-debugging-port` argument from the parent process. Once a CDP port is found, it establishes a WebSocket connection and injects a JavaScript script into the target page that periodically scans the DOM for buttons matching predefined patterns and triggers clicks.

Core flow:

```
Extension activates → Detect CDP port → WebSocket connect → Inject script → Poll & click
```

### State Management

A three-layer state model separates user intent from system capability:

| State | Meaning | Persisted |
|-------|---------|-----------|
| `userWantsEnabled` | Whether the user wants auto-accept on | globalState |
| `cdpAvailable` | Whether CDP connection is available | Runtime |
| `isRunning` | Whether polling is active | Runtime |

When the user has enabled but CDP is unavailable, the extension enters a BLOCKED state — clicking the toggle again triggers the setup wizard instead of toggling off.

### Port Detection

Tried in priority order:

1. VS Code setting `autoAccept.cdpPort`
2. Parent process command line (Windows via WMI process tree traversal, macOS via `ps`, Linux via `/proc/[pid]/cmdline`)
3. `--remote-debugging-port` in `process.argv`
4. `ELECTRON_REMOTE_DEBUGGING_PORT` environment variable

### Button Matching

The injected script decides whether to click a button through these steps:

1. Text matching against configurable `acceptPatterns` (e.g. `run`, `accept`, `retry`)
2. Exclusion of negative patterns (`skip`, `cancel`, `discard`, `deny`)
3. Visibility check (`display`, `visibility`, `opacity`, `getBoundingClientRect`)
4. Interactivity check (`pointer-events`, `disabled` attribute)

### Safety

Built-in command blocklist that intercepts destructive patterns by default:

```
rm -rf /    rm -rf ~    rm -rf *    format c:    del /f /s /q
rmdir /s /q    :(){:|:&};:    dd if=    mkfs.    > /dev/sda    chmod -R 777 /
```

Pro users can customize the blocklist through the settings panel.

---

## Features

- 14 configurable auto-accept action types (run, accept, retry, apply, execute, resume, confirm, etc.)
- Background mode: manages WebSocket connections across multiple tabs via CDP
- Instance mutex: coordinates across windows using `globalState` to ensure only one instance controls CDP
- Window state awareness: listens to `onDidChangeWindowState` and checks action stats when focus returns
- ROI tracking: weekly stats on clicks saved, time saved, and blocked commands with notification summaries
- Automatic shortcut configuration: modifies `.lnk` files and registry context menus on Windows, creates launchers via `osacompile` on macOS, patches `.desktop` files on Linux
- i18n: built on VS Code L10n API, supports English and Simplified Chinese with configurable override

---

## Installation

1. Download the `.vsix` file
2. Open IDE → `Ctrl+Shift+P` → `Install from VSIX`
3. Select the file and restart

### First-time Setup

The extension requires the IDE to be launched with `--remote-debugging-port=9000`. On first enable, it attempts to automatically modify system shortcuts to add this argument. Manual setup is also available:

**Windows** — Right-click shortcut → Properties → append `--remote-debugging-port=9000` to Target

**macOS** — Run `open -a "Antigravity.app" --args --remote-debugging-port=9000` from terminal

**Linux** — Edit the `Exec=` line in the `.desktop` file and append the argument

---

## Configuration

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `autoAccept.cdpPort` | `integer \| null` | `null` | CDP port, `null` for auto-detection |
| `autoAccept.autoAcceptFileEdits` | `boolean` | `true` | Auto-accept file edits |
| `autoAccept.languageOverride` | `string` | `auto` | UI language (`auto` / `en` / `zh-cn`) |
| `autoAccept.overlayMode` | `string` | `none` | Background overlay (`none` / `panel` / `minimal`) |
| `autoAccept.localVipOverride` | `boolean` | `false` | Force local Pro mode (debug) |

Action type selection is done through the settings panel's multi-select UI. Preferences are stored in `globalState`.

---

## Project Structure

```
├── extension.js           # Entry point, state management, command registration
├── settings-panel.js      # WebView settings panel
├── config.js              # Stripe payment link config
├── main_scripts/
│   ├── cdp-handler.js     # CDP connection management, WebSocket communication
│   ├── full_cdp_script.js # Full script injected into browser pages
│   ├── auto_accept.js     # Button detection and click logic
│   ├── relauncher.js      # Cross-platform shortcut modification
│   ├── overlay.js         # Background mode overlay UI
│   ├── selector_finder.js # CSS selector finder
│   └── utils.js           # Utility functions
├── utils/
│   └── localization.js    # i18n localization manager
├── l10n/                  # Language bundle files
└── test_scripts/          # Test scripts
```

---

## Compatibility

| Platform | IDE Support | Port Detection |
|----------|-------------|----------------|
| Windows | VS Code, Antigravity, Cursor | WMI process tree traversal |
| macOS | VS Code, Antigravity, Cursor | `ps` command traversal |
| Linux | VS Code, Antigravity, Cursor | `/proc` filesystem |

Supports multiple windows, multiple instances (coordinated via globalState instance lock), minimized and unfocused states.

---

## License

[MIT](LICENSE.md)
