# Changelog

## 0.1.9 — 2026-07-22
### Bundle Mode
- `H` toggle — collapsed nodes with header only
- Segmented connector balls (28×28px, r=14) — active/connected segments filled with socket color, inactive `#2a2a2a`
- White stroke highlight on active segment during connection drag
- Socket name label next to bundle ball when cycling
- Merged wires by node pair — single thick bezier (3× width, no animation)
- Connection drag preview snaps to bundle ball centers
- Slider remains visible below collapsed header

### Shortcuts
- `Tab` / `Shift+Tab` — cycle output/input sockets (works alongside mouse wheel)
- Shortcuts list split into **General** / **Connection** sections

### Docs
- `WEBARCCONTEXT.md` — WebView2 embedding path documented

## 0.1.8 — 2026-07-22
### AddNodeMenu
- Press **Space** inside menu to switch to search mode
- Fuzzy match ranking: exact → prefix → contains → chars-in-order
- Top 8 results, substring highlighting (`#FFD66B` bold)
- `↑↓` navigate, `↵` add, `Esc` back to carousel
- Match counter, clear (✕) button, soft pulse animation

## 0.1.7 — 2026-07-22
### Save as Startup
- Full graph persistence (nodes + connections + nodeDef + fontFamily)
- `startupDataSchema` extended with optional `nodes` / `connections`
- Legacy v0.1.6 saves backward-compatible (fallback to single default node)

## 0.1.6 — 2026-07-22
### Save as Startup Fix
- Fixed data corruption — `saveToDisk` no longer merges values across node instances
- Toast confirmation on successful save
- `syncDefaults` no longer strips keys from secondary nodes

## 0.1.5 — 2026-07-22
### Wire Animation Stability
- `effectiveWireOptions` stabilised via `useMemo` — prevents `pathHtml` recompute on every render
- `performance.now()` hoisted once per frame — all wires share same animation phase
- `ensureKeyframes` mutates `<style>` element — Dash slider actually works
- `-0` boundary glitch in `animation-delay` fixed

## 0.1.4 — 2026-07-22
### Wire Animation Fix
- Negative `animation-delay` synced via `performance.now()` — no jitter on node drag
- Defaults: `dashed: true, animated: true`
- SVG `translateZ(0)` compositor layer isolation
- 3 dead-code symbols removed from `Canvas.tsx`

## 0.1.3 — 2026-07-22
### Performance
- Viewport + wire culling (800px margin)
- `innerHTML` wires — SVG paths as string → `dangerouslySetInnerHTML`
- `React.memo` on Node + Wires
- `contain: layout style` + `will-change: transform` on node during drag
- RAF animation removed — sliders use `const anim = raw`
- `animationsEnabled` for conditional CSS transitions

### Slider
- CSS transition on thumb (`left .12s`), disabled during active drag
- ~~RAF idle-stop~~ (was added, then removed with RAF)

### Color Picker
- Two-column layout: HS circle + sliders/hex
- HSV math, 8-digit hex output
- Smooth lerp animation (factor 0.12)

## 0.1.2 — 2026-07-19
### AddNodeMenu
- 2-level carousel: category → node
- 11 Blender 5.2 categories
- Breadcrumb animation (`slideFromRight`, 0.15s)
- Spawn at mouse position
- Russian layout support (`e.code`)

## 0.1.1 — 2026-07-21
### Multi-select
- Shift+click toggle multi-select (white border)
- `X` deletes all selected nodes + connections
- Box selection — drag on empty canvas
- `Shift+D` duplicates all selected nodes
- `G` works with box-selected nodes
- RAF box rendering

## 0.1.0 — 2026-07-21
### Initial Release
- Body-drag connections
- Node CRUD (add, duplicate, delete)
- Viewport controls (zoom, pan, reset)
- Color picker (Oklch)
- Animations toggle
- Focus mode (F)
- Wire styles (bezier, straight, step, wave, etc.)
- Save/Load via localStorage
- Blender addon → `webbrowser.open()`
