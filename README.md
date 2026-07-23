# Send Nodes

Веб-редактор нод в стиле Blender. Vite + React 19 + Zustand + Zod. **v0.1.14**

## Возможности

- **Граф нод**: добавить, удалить, дублировать, выбрать, переместить, box-select, multi-select
- **Соединения**: body-drag из выхода → вход, **обратное направление** (input→output), **Alt+click** отключение, **Alt+hover** sweep-отключение с красной точкой
- **Bidirectional drag**: double-click по карточке стартует drag, **Alt** переключает направление output↔input на лету
- **Space-search на drag**: во время body-drag Space открывает фильтр совместимых нод с авто-коннектом
- **11 стилей проводов**: bezier, straight, step, wave, zigzag, arc, double, ribbon, glow, tapered, dot-flow
- **Анимация проводов**: синхронизированный dash flow через `performance.now()`, композиторный слой SVG
- **Bundle Mode** (`H`): свёрнутые ноды с **donut-сегментами**, объединённые провода от центров
- **Типы нод**: Color Mix (микшер цвета), Image Texture (загрузка файлов + превью под карточкой)
- **Focus Mode** (`F`): затемнение несвязанных нод
- **Color Picker**: Oklch, HS круг, RGB/HSV, hex, плавная lerp-анимация
- **AddNode Menu** (`Shift+A`): карусель из 2 уровней + поиск по Space с fuzzy-фильтром
- **Undo/Redo** (`Ctrl+Z`/`Ctrl+Y`): с toast-уведомлением
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
| `M` | Mute/размутить выбранные ноды |
| `Tab` / `Shift+Tab` | Переключить сокет (режим соединения) |
| `Space` | Поиск (в меню) / фильтр нод (при drag) |
| `Alt` + клик | Отключить соединение |
| `Alt` + hover | Sweep-отключение всех соединений |
| `Alt` (при drag) | Переключить направление output↔input |
| `Ctrl+Z` / `Ctrl+Y` | Undo / Redo |
| `Esc` | Отменить соединение / закрыть меню |

## Ченджлог

Полная история версий — [`CHANGELOG.md`](CHANGELOG.md).
