# Changelog

## v0.1.55 — Feature Registry Panel + B Badge (2026-08-02)

### 🗂️ Feature Registry Panel
- Новый `src/lib/featureRegistry.ts` — единый реестр функционала (11 General + 10 Connection + 7 Features)
- Панель под зумом: вкладки General/Connection/Features теперь рендерятся из реестра (были хардкод-строки)
- Вкладка **Features** — режимы тулбара (Expert/Focus/Animations/Bundle/Card/Collapse/Compact) с live-пилюлями ON/OFF
- Bundle помечен бейджем **B** (работа в режиме Bundle). Общий компонент `MenuTagBadge` (FINAL/WIP/OLD/B)
- Порядок строк: сначала хоткей, затем описание; кнопки-вкладки осветлены

### 📦 Default Startup (25)
- Свежий экспорт: 8 nodeDefs

### 🧪 Tests
- `featureRegistry.test.ts` (5) + `ShortcutsPanel.test.tsx` (6) — 181/181 green

---


## v0.1.52 — Expert Mode + Mix Shader (2026-07-31)

### ✨ Expert Mode
- Кнопка **Expert** в тулбаре (перед Focus)
- Все шапки нод → серый `#555` (не отвлекают)
- Названия нод, обводка Selection, точка активного Output — остаются в цвете Data Type
- Mode-switcher текст в Header → `#eee` (читаемый на сером)
- ColorPicker автоматически в Focus-режиме, кнопка Focus заблокирована

### 🔀 Mix Shader
- Новая нода `mix_shader` (зелёная, dt6 Shader)
- 2 Shader входа + Factor слайдер
- В дефолтном графе: RGB → Principled → Mix Shader → Material Output

### 📦 Default Startup (24)
- Свежий экспорт: 2 Principled BSDF, Mix Shader, обновлённый граф соединений
- Почищены stray values на нодах
- Исправлена опечатка: Shdaer → Shader

---

## v0.1.51 — Configurator Preview + useShallow (2026-07-30)

### 🖼️ Configurator
- Preview Block для File-контролов — настройка превью без хардкода через `previewToggle`
- `useNodeEditor` (23 useState) → вынесен из NodeConfiguratorPanel
- CollapsibleSection — общий компонент для сворачиваемых секций

### ⚡ Performance
- `useShallow` applied to `useCanvasRender` (14→1 Zustand subscription)
- `useShallow` applied to `PropertiesPanel` (26→1)
- `useShallow` applied to `useCanvasShortcuts` (12→1)

### 🧪 Tests
- `CollapsibleSection.test.ts` — 9 smoke-тестов
- `useNodeEditor.test.ts` — 26 тестов (loadType/startNew/save)

---

## v0.1.46 → v0.1.50 — Node Builder, Cleanup & React.memo (2026-07-26–29)

### 🏗️ Node Configurator
- NodeConfiguratorPanel — создание/редактирование нод через UI
- Node Types группируются по Data Types
- Global Settings: Card Style (padding, radius, dim, cross position)
- Sockets linked to controls (inputSocketId → dimming)

### 🧹 Code Cleanup
- NodeSelectorPanel удалён (заменён категориями)
- ControlCard.tsx удалён
- FormFields.tsx удалён
- ~100 строк мёртвых констант выпилено из menuConfig.ts

### ⚡ React.memo Fix (v0.1.49)
- `useNodeRender` bag без `zoom`/`isZoomedOut` (continuous primitive leak fix)
- `NodeWrapper` hash-based `connectedSockets` Set memo
- 33 inline пропа → единый объект `interactions` через `useMappedCallback`

### 🔧 QoL
- Mute: красный badge MUTED над нодой + batch mute через box-select
- Auto-cardless: zoom<100+bundle → cardless auto-on/off
- `useCanvasLayout`, `useCanvasHandlers`, `useCanvasMenu` вынесены из Canvas
