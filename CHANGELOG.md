# Ченджлог

## 0.1.17 — 2026-07-24
- **Alt/Shift fix** — `e.preventDefault()` для Alt предотвращает перехват фокуса браузером. Alt и Shift+Alt работают стабильно
- **Socket-click card completion** — клик по карточке целевой ноды завершает socket-click соединение; колёсико циклит совместимые сокеты
- **commitSocketConnection** — общая функция создания соединения, убрана дупликация из handleSocketClick и handleNodeSelect
- **Bundle: donut hover fix** — названия сокетов и подсветка сегментов работают для input и output сторон при connection drag
- **Bundle: socket labels 1.5×** — лейблы увеличены с 11px до 16px, font-weight 500

## 0.1.16 — 2026-07-23
- **Import Default** — кнопка «Import Default» + Ctrl+Shift+I для сброса к заводским настройкам (очистка localStorage + reload)

## 0.1.15 — 2026-07-23
- **Архитектурный рефакторинг:** appStore → 3 Zustand слайса (graph/ui/config), Wires → wireStyles.ts, Canvas → useConnections.ts. 44 теста (+22 graphSlice). Исправлен баг fontFamily.

## 0.1.14 — 2026-07-23
- **Красная точка на connected сокетах при Alt** — зажал Alt → все подключенные сокеты заливаются `#ff1c1cfa` (не кольцо, а полностью заполненный круг). Работает и на Alt-один (сигнал «кликни для дисконнекта»), и на Alt+Shift (sweep-режим)
- **`altActive` state для реактивной подсветки** — refs не триггерят ререндер; теперь `setAltActive(altHeldRef.current)` в keydown/keyup → Canvas → Node → Sockets реагируют мгновенно
- **Рефакторинг RAF-блоков** — `detectHoverTarget(source)` в `useConnectionDrag` заменил 2 идентичных блока (body-drag и socket-click) на один вызов с shared логикой
- **`disconnectMode` пропс** — заменил `sweepActive` в Sockets/Node для визуальной подсветки; `sweepActive` остался только для курсора (crosshair) и handleSocketEnter
- **Очистка мёртвого кода** — убран `sweepActive` из SocketsProps и Node (не использовался после замены на disconnectMode)
- **Bundle:** 404.15 kB (gzip 115.36 kB)

## 0.1.13 — 2026-07-23
- **Alt + hover = disconnect (Blender-style wire cut)** — зажал Alt, провёл курсором по сокетам/сегментам бублика → все отключаются. Не нужно кликать. Браузерное меню и выделение текста заблокированы (`e.preventDefault()` + `user-select: none` + `selectstart` listener)
- **Box Select отключён при Alt** — Alt+hover не вызывает случайный box select
- **Unification connection logic** — `resolveCanConnect(dragSide, src, tgt)` и `resolveConnEndpoints(drag, target)` в `graph/index.ts`. Убрано 8 повторов if/else в Canvas и useConnectionDrag (~40 строк → 10)
- **Bundle: donut-сегменты вместо пиццы** — кольцо с отверстием в центре (rInner=8, R=14), зазор 3° между сегментами, точка соединения в центре с отступом. `overflow: visible` убирает обрезку обводки
- **Bundle: reverse connection + провода от центров** — bidirectional подсветка сегментов, `previewWire` от центров шаров в Bundle mode (`getBundleCenter`)
- **Bundle: лейблы и колёсико при клике на сегмент** — клик по сегменту показывает имя сокета, колёсико переключает сегменты, target-сегменты подсвечиваются при наведении на чужой бублик
- **Sweep-отключение в Bundle** — сегменты бублика теперь React SVG (не innerHTML), кликабельны для Alt+disconnect
- **Toast undo/redo** — полупрозрачная плашка «Undo»/«Redo» при Ctrl+Z/Y
- **Space-search на wire drag** — пробел во время body-drag открывает AddNodeMenu с фильтром по совместимым типам нод, авто-коннект после выбора
- **ShortcutsPanel обновлён** — все новые шорткаты (Mute, Undo/Redo, Alt+hover disconnect, Space-search, Alt-flip, cycle target)

## 0.1.12 — 2026-07-23
- **Bidirectional connection drag** — можно вести провод от input-сокета к output другой ноды (обратное направление). Клик на input-сокет стартует drag вместо удаления connection
- **Alt + клик = disconnect** — зажал Alt и кликнул на input или output сокет → существующий connection удаляется
- **Alt во время body drag = flip output↔input** — double-click по карточке, затем нажатие Alt переключает направление drag с output на input и обратно. Не нужно заново стартовать
- **Input socket labels при body drag** — при Alt-flip на input-сокеты: source input подсвечивается, label с названием появляется (scale 1.4, цвет заполнения)
- **Target label fix при reverse drag** — `activeInput` ищет target и в inputs, и в outputs — label цели корректно показывается независимо от направления
- **Убран ALT+double-click** — неудобный, заменён на Alt во время drag
- **Убран Alt+hover disconnect** — слишком агрессивно, оставлен только Alt+click

## 0.1.11 — 2026-07-23
- **Починена белая страница Vite dev server** — 4 корневые причины: (1) Vite Fast Refresh ломался на смешанных экспортах в `Controls.tsx` → разделён на `Controls.tsx` + `renderControl.tsx`; (2) Zustand v4 — отсутствовали каррированные скобки `create<AppState>()(...)`, generic игнорировался; (3) Zod schema — пропущен variant `"file"` в `controlDefSchema`; (4) Битый импорт `StartupData` в `storage/index.ts`
- **Убран двойной рендер preview-проводов** — Wires.tsx больше не рисует свои preview, только `useConnectionDrag.previewWire` с корректным zoom/pan
- **Dead code cleanup** — 6 неиспользуемых пропсов из WiresProps, мёртвая функция `renderWire` (11 стилей), неиспользуемые импорты, `NodePreview.tsx`
- **Bundle:** 395.06 kB (gzip 113.37 kB)

## 0.1.10 — 2026-07-23
- **Default startup для GitHub Pages** — `src/defaultStartup.ts` с графом пользователя (3 Mix Shader + Image Texture) вшит в билд. При первом открытии GitHub Pages грузится твой граф
- **Кнопка «Export Default»** — скачивает текущий стартап как JSON, который можно положить в `defaultStartup.ts`
- **Box Selection** — починен RAF-цикл: линия выделения снова видна

## 0.1.9 — 2026-07-23
- **Рефакторинг:** Canvas.tsx (975→370 строк, −21%) и Node/index.tsx (612→230, −47%) разбиты на хуки и компоненты
- **Новые файлы:** `useCanvasShortcuts`, `useConnectionDrag`, `useBoxSelect`, `ShortcutsPanel`, `CanvasToolbar`, `Sockets`, `Header`, расширен `Controls`
- **Исправлены 4 скрытые ошибки tsc** (ControlCard без `"file"`, PropertiesPanel без `case "file"`, сужение типа в appStore, `unknown` → boolean в Node)
- **Починены баги:** preview wire без учёта zoom/pan, findNodeAt с хардкодом `pan={x:0,y:0}`, мёртвый проп `sockColor`
- **Удалён мёртвый код:** деад пропсы, неиспользуемые импорты, `NodePreview.tsx`
- **Bundle Mode** (`H`) — ноды сворачиваются в заголовок, сегментированные шары-коннекторы, объединённые провода
- **Image Texture** — нода с загрузчиком файлов и превью под карточкой
- **Tab** / **Shift+Tab** — циклинг сокетов в режиме соединения
- **Убран иконка формата** перед именем файла в контроле file
- **Исправлен баг:** RAF-цикл в `useBoxSelect` останавливался на первом тике — box selection не показывал линию выделения

## 0.1.8 — 2026-07-22
- **Поиск в AddNode Menu** — Space переключает в режим поиска, fuzzy-фильтр по всем типам нод, подсветка совпадения
- **Подсказки** — `↑↓` навигация, `↵` добавить, `Esc` назад, счётчик результатов, кнопка очистки

## 0.1.7 — 2026-07-22
- **Save as Startup сохраняет весь граф** — после перезагрузки восстанавливаются все ноды, соединения, редактирования, удаления. Legacy-сохранения (v0.1.6) загружаются с одной нодой по умолчанию

## 0.1.6 — 2026-07-22
- **Исправлена порча данных в Save as Startup** — значения разных нод больше не перезаписывают друг друга
- **Toast** подтверждения при сохранении

## 0.1.5 — 2026-07-22
- **Стабильная анимация проводов** — дёрганье при любом взаимодействии (слайдер, ховер, переключение режимов) устранено. Слайдер Dash теперь реально меняет анимацию

## 0.1.4 — 2026-07-22
- **Wire Animation Fix** — провода больше не дёргаются в начале анимации при перетаскивании нод

## 0.1.3 — 2026-07-22
- **Оптимизация производительности** — viewport culling, wire culling, innerHTML-провода, React.memo на нодах и проводах
- **Color Picker** — Oklch, HS круг, RGB/HSV, hex, плавная анимация
- **FPS счётчик**, **кнопки зума**

## 0.1.2 — 2026-07-19
- **AddNode Menu** (`Shift+A`) — 2 уровня (категория → нода), 11 категорий Blender 5.2, спавн в позиции мыши

## 0.1.1 — 2026-07-21
- **Multi-select** — Shift+клик, Box selection, `X` удаляет все выбранные
- **Shift+D** дублирует выбранные ноды, **G** работает с группой

## 0.1.0 — 2026-07-21
- Первый релиз: граф нод, body-drag соединения, вьюпорт, Color Picker, Focus Mode, 11 стилей проводов, локальное сохранение, Blender addon
