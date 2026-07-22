# Send Nodes

Веб-редактор нод в стиле Blender. Vite + React 19 + Zustand + Zod.

## Возможности

- **Граф нод**: добавить, удалить, дублировать, выбрать, переместить, box-select, multi-select
- **Соединения**: body-drag из выхода → вход, циклинг сокетов (колесо / Tab), hover-валидация по data type
- **11 стилей проводов**: bezier, straight, step, wave, zigzag, arc, double, ribbon, glow, tapered, dot-flow
- **Анимация проводов**: синхронизированный dash flow через `performance.now()`, композиторный слой SVG
- **Bundle Mode** (`H`): свёрнутые ноды с сегментированными шарами-коннекторами, объединённые провода
- **Focus Mode** (`F`): затемнение несвязанных нод
- **Color Picker**: Oklch, HS круг, RGB/HSV, hex, плавная lerp-анимация
- **AddNode Menu** (`Shift+A`): карусель из 2 уровней + поиск по Space с fuzzy-фильтром
- **Вьюпорт**: зумирование к курсору, pan (MMB), авто-pan при drag, сетка

## Шорткаты

| Клавиша | Действие |
|---------|----------|
| `A` | Выделить всё / снять выделение |
| `Shift+A` | Меню добавления ноды |
| `X` | Удалить выбранные |
| `Shift+D` | Дублировать |
| `G` | Переместить |
| `F` | Вкл/выкл Focus Mode |
| `H` | Вкл/выкл Bundle Mode |
| `Tab` / `Shift+Tab` | Переключить сокет (режим соединения) |
| `Esc` | Отменить соединение / закрыть меню |

## Стек

- **Vite 8** + `vite-plugin-singlefile` → один `index.html` (~385 кБ)
- **React 19**, Zustand, Zod, CSS-in-JS
- **Blender addon**: раздаёт `dist/` на `:8888`, открывается через `webbrowser.open()`
- Нет роутера, нет UI-библиотеки, нет Tailwind

## Ченджлог

Полная история версий — [`CHANGELOG.md`](CHANGELOG.md).
