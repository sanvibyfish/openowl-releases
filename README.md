<p align="center">
  <img src="resources/icon.png" width="128" height="128" alt="openowl">
</p>

<h1 align="center">openowl</h1>

<p align="center">
  Git GUI + Terminal desktop app. No built-in AI — your terminal, your tools.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/platform-macOS-blue" alt="macOS">
  <img src="https://img.shields.io/badge/electron-33-47848f" alt="Electron">
  <img src="https://img.shields.io/badge/license-MIT-green" alt="License">
</p>

---

## Why openowl?

Most Git GUIs either lock you into their workflow or bolt on AI features you didn't ask for. openowl takes a different approach: **the terminal is the core**. Open any project, get a full-featured terminal with split panes and tabs, and manage Git visually — all in one window. Want AI? Run Claude Code, GitHub Copilot, or whatever you prefer directly in the terminal.

## Features

**Terminal (ghostty-web)**
- Native-quality terminal rendering via WebAssembly
- Multi-tab support (Cmd+T, Cmd+1-9)
- Split panes — horizontal (Cmd+D), vertical (Cmd+Shift+D)
- Focus navigation between splits (Cmd+Arrow)
- Readline shortcuts mapped through (Cmd+K/L/U/E)

**Git**
- Changes panel with staged / unstaged / untracked groups
- Stage/unstage individual files or batch
- Inline diff view with syntax highlighting
- Commit with optional AI-generated messages
- Git graph with SVG lane visualization
- Branch management and remote operations

**Projects & Worktrees**
- Multi-project sidebar with accordion navigation
- Create/archive Git worktrees with one click
- Per-project terminal sessions that persist across switches
- Branch tracking per worktree

**File Explorer**
- Tree view with lazy-loaded directories
- Git status color coding (green/yellow/red)
- .gitignore-aware filtering
- Right-click context menu (open in terminal/Finder)

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Electron 33 + electron-vite 5 |
| UI | React 19 + TypeScript + Tailwind CSS 4 |
| Terminal | ghostty-web (WASM) + node-pty |
| Git | simple-git |
| Editor | Monaco Editor + Shiki |
| Components | shadcn/ui + Radix UI + Lucide icons |

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Cmd+T | New terminal tab |
| Cmd+1-9 | Switch to tab N |
| Cmd+D | Split horizontal |
| Cmd+Shift+D | Split vertical |
| Cmd+W | Close split/tab |
| Cmd+Arrow | Move focus between splits |
| Cmd+K | Clear to end of line |
| Cmd+L | Clear screen |
| Cmd+U | Clear line |
| Cmd+E | Move to end of line |
| Cmd+Enter | Submit commit |
| Cmd+Option+I | Toggle DevTools |

## Getting Started

```bash
# Clone
git clone https://github.com/sanvibyfish/openowl-releases.git
cd openowl

# Install
npm install

# Dev
npm run dev

# Build
npm run build && npx electron-builder --mac
```

Requires Node.js 20+ and macOS (for now).

## Project Structure

```
src/
├── main/                   # Electron main process
│   ├── index.ts            # Window creation, shortcuts
│   ├── ipc/                # IPC handlers (git, pty, fs, project)
│   └── services/           # Git, PTY, file watcher, store
├── preload/                # contextBridge API
└── renderer/src/           # React app
    ├── app/layout/         # MainLayout, Sidebar, RightPanel
    ├── features/
    │   ├── terminal/       # ghostty-web + store + splits
    │   ├── git/            # Changes, Graph, Diff, Commit
    │   ├── projects/       # Project list, worktrees
    │   └── files/          # File tree explorer
    ├── stores/             # useSyncExternalStore state
    └── components/ui/      # shadcn components
```

App data is stored at `~/.openowl/`. Worktrees are created under `~/.openowl/workspace/`.

## License

MIT
