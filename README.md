# Send Nodes

Web-based Blender-style node editor. Vite + React 19 + Zustand + Zod.

## Features

- **Node graph**: add, delete, duplicate, select, move, box-select, multi-select
- **Connections**: body-drag from output → input, socket cycling (wheel / Tab), hover validation by data type
- **11 wire styles**: bezier, straight, step, wave, zigzag, arc, double, ribbon, glow, tapered, dot-flow
- **Wire animation**: synced dash flow via `performance.now()`, compositor-isolated SVG
- **Bundle Mode** (`H`): collapsed nodes with segmented connector balls, merged wires by node pair
- **Focus Mode** (`F`): dims unconnected nodes
- **Color Picker**: Oklch, HS circle, RGB/HSV, hex, smooth lerp animation
- **AddNode Menu** (`Shift+A`): 2-level carousel + Space-to-search with fuzzy matching
- **Viewport**: zoom to cursor, pan (MMB), auto-pan during drag, grid background

## Shortcuts

| Key | Action |
|-----|--------|
| `A` | Select all / deselect all |
| `Shift+A` | Add Node menu |
| `X` | Delete selected |
| `Shift+D` | Duplicate |
| `G` | Grab / move |
| `F` | Toggle focus mode |
| `H` | Toggle bundle mode |
| `Tab` / `Shift+Tab` | Cycle socket (connection mode) |
| `Esc` | Cancel connection / close menu |

## Stack

- **Vite 8** + `vite-plugin-singlefile` → single `index.html` (~385 kB)
- **React 19**, Zustand, Zod, CSS-in-JS
- **Blender addon**: serves `dist/` on `:8888`, opens via `webbrowser.open()`
- No router, no UI library, no Tailwind

## Changelog

See [`CHANGELOG.md`](CHANGELOG.md) for full version history.
