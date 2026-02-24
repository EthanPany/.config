# Ethan's Config

> Forked from [theniceboy/.config](https://github.com/theniceboy/.config) — adapted for **QWERTY keyboard** on **macOS (Ghostty) + Linux**.

## What's inside

| Tool | Purpose |
|---|---|
| **ghostty** | Terminal emulator (macOS client) |
| **tmux** | Terminal multiplexer |
| **zsh** | Shell |
| **starship** | Pane titles inside tmux |
| **yazi** | File manager |
| **lazygit / lazynpm** | Git & npm TUI |
| **neofetch** | System info |
| **agent-tracker** | Claude Code agent task tracker |
| **codex / opencode** | AI coding tools |

## Key changes from upstream

### QWERTY keyboard remapping
The original config is built for **Colemak** layout. All positional bindings are remapped so the same finger positions work on a standard QWERTY keyboard:

| Colemak | QWERTY | Direction |
|---|---|---|
| `n` | `j` | Left |
| `e` | `k` | Down |
| `u` | `i` | Up |
| `i` | `l` | Right |

### tmux — prefix is `Ctrl+s`

**Panes (no prefix needed):**
| Key | Action |
|---|---|
| `⌥j / ⌥k / ⌥i / ⌥l` | Move between panes (left/down/up/right) |
| `⌥J / ⌥K / ⌥I / ⌥L` | Resize panes |
| `⌥f` | Toggle fullscreen zoom |

**Windows (no prefix needed):**
| Key | Action |
|---|---|
| `⌥;` | New window |
| `⌥Q` | Kill pane |
| `⌥1`–`⌥9` | Jump to window |
| `⌥u / ⌥o` | Swap window left / right |

**Sessions (no prefix needed):**
| Key | Action |
|---|---|
| `⌥D` | New session |
| `⌥d` | Toggle scratchpad |
| `Ctrl+1`–`Ctrl+9` | Switch session by index |

**With prefix `Ctrl+s`:**
| Key | Action |
|---|---|
| `i / k / j / l` | Split pane up/down/left/right |
| `r` | Reload config |
| `u / o` | Move window to session left/right |

### Ghostty
`macos-option-as-alt = true` — makes `Option` send ESC-prefix sequences so tmux `M-` bindings work on macOS. Without this, `Option+key` prints garbage (`<ffffffff>`) instead of triggering shortcuts.

> **After syncing to your Mac:** fully quit and reopen Ghostty (`Cmd+Q`) for this setting to take effect.

### tmux 3.6+
Requires tmux 3.6+ for `pane-scrollbars`. Build from source if your distro ships an older version:
```bash
sudo apt-get install -y libevent-dev libncurses-dev build-essential
curl -sL https://github.com/tmux/tmux/releases/download/3.6/tmux-3.6.tar.gz | tar xz -C /tmp
cd /tmp/tmux-3.6 && ./configure --prefix=/usr/local && make -j$(nproc) && sudo make install
sudo ln -sf /usr/local/bin/tmux /usr/bin/tmux
```

## Setup on a new machine

```bash
# 1. Clone into ~/.config
git clone https://github.com/EthanPany/.config.git ~/.config

# 2. Run the setup script (installs tools + creates symlinks)
~/.config/bin/upgrade-all

# 3. Linux only: set zsh as default shell
sudo chsh -s /usr/bin/zsh $USER
```

## Syncing changes

```bash
# Push changes from this machine
cd ~/.config && git add -A && git commit -m "message" && git push

# Pull on another machine
cd ~/.config && git pull

# Pull updates from the original author (optional)
git fetch upstream && git merge upstream/main
```

## First-time Mac setup

```bash
# 1. Clone the repo
git clone https://github.com/EthanPany/.config.git ~/.config

# 2. Run setup
~/.config/bin/upgrade-all

# 3. Fully quit and reopen Ghostty (Cmd+Q)
#    Required for macos-option-as-alt to take effect —
#    without this Option+key prints <ffffffff> instead of triggering tmux shortcuts
```
