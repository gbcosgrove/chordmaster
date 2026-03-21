# CHORDMASTER

> Learn keyboard shortcuts by doing — not by reading.

A keyboard shortcut trainer built around one insight: shortcuts only stick when your **fingers** learn them, not your eyes. The same principle that made touch-typing trainers effective, applied to chords.

## Quick Start

```
open index.html
```

No build step. No server needed. No accounts. Everything stores in localStorage.

## How It Works

Each session:
1. Pick a pack (Terminal, tmux, Vim — or import your own)
2. 20 shortcuts per session, ordered by spaced repetition (most overdue first)
3. Press the **actual key combination** — no multiple choice, no clicking
4. Instant feedback: correct/wrong, response time, visual
5. Summary with accuracy and streak stats

### Modes

| Mode | Behavior |
|------|----------|
| **LEARN** | Auto-show hint after 4 seconds of inactivity. Good for new packs. |
| **CHALLENGE** | No hints. Pure recall. Use once you've done a pack in learn mode. |

### Scoring

Response time determines your score (1–5), not just correctness:

| Score | Meaning | Interval effect |
|-------|---------|-----------------|
| 5 | < 40% of target time | Interval × ease factor |
| 4 | < 70% | Interval × ease factor |
| 3 | < 110% | Interval × ease factor |
| 2 | < 180% | Small interval increase |
| 1 | Slow / used hint | Interval resets to 1 day |

Shortcuts you know cold surface less often. Ones you fumble come back daily.

### Quit a Session

Press **ESC twice** to exit mid-session, or use the `[ QUIT ]` button.

## Keymaps

### Built-in Packs

| Pack | Shortcuts | Description |
|------|-----------|-------------|
| Terminal | 17 | bash/zsh readline shortcuts |
| tmux | 18 | Window, pane, and session management |
| Vim | 24 | Normal-mode motions, editing, search |

### Import a Custom Keymap

1. Click **↑ IMPORT KEYMAP** on the home screen
2. Select a `.json` file following the schema

Click **download keymap schema** in the footer to get the JSON Schema + example.

#### Key Format Reference

| Format | Meaning | Example |
|--------|---------|---------|
| `ctrl+a` | Hold Ctrl, press A | `ctrl+a` |
| `alt+f` | Hold Alt/Option, press F | `alt+f` |
| `G` | Shift+G (capital letter) | `G` |
| `$` | Shift+4 (dollar sign) | `$` |
| `escape` | Escape key | `escape` |
| `enter` | Enter/Return | `enter` |

#### Shortcut Types

| Type | Keys value | When to use |
|------|-----------|-------------|
| `chord` | `["ctrl+a"]` | All keys held simultaneously |
| `sequence` | `["ctrl+b", "c"]` | Keys pressed in order (like tmux prefix) |
| `key` | `["G"]` | Single keypress (like Vim normal-mode) |

#### Example Custom Keymap

See `keymaps/example-custom.json` for a complete VS Code keymap example.

Minimal example:

```json
{
  "meta": {
    "id": "my-app",
    "name": "My App",
    "subtitle": "shortcuts",
    "icon": "✦",
    "color": "#ff9500"
  },
  "shortcuts": [
    {
      "id": "my-save",
      "type": "chord",
      "keys": ["ctrl+s"],
      "description": "Save file",
      "category": "File",
      "difficulty": 1
    },
    {
      "id": "my-tmux-split",
      "type": "sequence",
      "keys": ["ctrl+b", "%"],
      "description": "Split pane vertically",
      "category": "Panes",
      "difficulty": 1
    }
  ]
}
```

## Known Limitations

- **OS-level shortcuts** (Cmd+Space, Cmd+Tab, Cmd+Q) can't be captured in a browser. Avoid including these in keymaps.
- **Mac Option key**: Alt+letter combos work correctly — the trainer uses `e.code` (physical key) rather than `e.key` to avoid macOS Option-character substitution (alt+f → "ƒ").
- **Vim command mode** (`:wq`, `:q!`) is not supported — these require line-input mode, which conflicts with key capture. Stick to Normal-mode shortcuts.
- **File protocol**: The app works at `file://` without a server. Custom keymap import uses the FileReader API, which is fully supported.

## Contributing

The keymap format is intentionally simple. Contributions welcome:
- Additional built-in packs (Git, fish shell, Neovim, Zellij, Helix, etc.)
- i18n key label support
- Stats export

## License

MIT
