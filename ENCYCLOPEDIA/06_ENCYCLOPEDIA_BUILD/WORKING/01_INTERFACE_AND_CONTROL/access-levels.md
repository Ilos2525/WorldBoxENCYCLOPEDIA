# Уровни доступа интерфейса

**Статус фактов:** CONFIRMED по сцене `level1` и коду, если не помечено иначе.

## WHAT PLAYER CAN DO

Отличать четыре слоя, которые в этой копии игры видны одновременно.

## VANILLA

Поставляемый HUD: объект `CanvasMain` / `canvas_ui` в сцене `level1`.

- Главные вкладки сил (`tab_type_main`)
- Вкладки после выбора объекта (`selected_unit`, `selected_city`, …)
- Окна `ScrollWindow` по кнопкам Window и по inspect
- Хоткеи паузы, скрытия UI, переключения вкладок, possession (`control_unit`)

Моды в `level1` **не входят**. Toolbar из сцены = ваниль, даже если рядом установлены PowerBox/NML.

Premium: поля `requires_premium` / `PowerRank` есть в коде. Какие кнопки скрыты на конкретном аккаунте — **REQUIRES LIVE VALIDATION**.

## DEBUG

Окно `debug` и bug-кнопка HUD после 11 кликов `GraphyCaller`. Консоль `~` работает **без** этого unlock (лог).

Mind tab юнита (последнее Decision) — **ваниль**, не debug.

Подробно: [05 Debug](../05_DEBUG_AND_DEVELOPER_TOOLS/debug-menu.md).

## INTERNAL

Классы окон и `ButtonEvent.debug*` существуют. Методы `initDebugHotkeys()` в релизе **не вызываются**. Флаги `Config.editor_*` по умолчанию false.

Игрок не получает их из обычного или debug-меню, пока нет кнопки в prefab / вызова.

## MOD_ONLY

| Мод | Что добавляет (не ваниль) |
|---|---|
| NeoModLoader | загрузчик |
| PowerBox 1.5.1 | вкладка PowerBox, EditResources, FindAllCreatures, extra GodPowers (армия, convert city, duplicate culture…) |
| ModernBox, RulerBox, TPI | DLL; UI в `05` не разбирался по кнопкам |

Если кнопка видна только после загрузки модов — это не ответ «ванильный WorldBox умеет».

## WHERE TO FIND IT

Слои на экране:

```
canvas_ui        — вкладки сил
canvas_windows   — окна (Resources.Load "windows/"+id)
canvas_tooltip
canvas_map_names
```

Типы кнопок `PowerButton`: Active = GodPower; Special = overlay/toggle; Window = открыть окно; Options = не GodPower (inspect-вкладки); BrushSize / TimeScale; Shop.

## WHAT HAPPENS AFTER THE ACTION

Клик Active → выбор силы → клик по миру → `PlayerControl.clickedFinal` → делегат GodPower.  
Клик Window → `ScrollWindow.showWindow`.  
Клик Options на selected-вкладке → `ButtonEvent` / `SelectedMeta.open*` → то же окно + внутренняя вкладка.

## LIMITATIONS

- Наличие `GodPower` в `PowerLibrary` ≠ кнопка на HUD.
- Наличие окна в `WindowLibrary` (99 id) ≠ ванильный вход. Доказаны кнопки на canvas, inspect/`MetaTypeLibrary`, `select_button_action`.
- `follow_unit` есть хоткеем, кнопки на toolbar нет.
- `mush_unit` есть в библиотеке сил, кнопки на вкладке units нет.
- TradeRoutes на noosphere → окно `under_development`.

## RELATED SYSTEMS

[Вкладки](hud-tabs.md) · [Окна](windows-inspect-select.md) · [Силы](../02_POWERS_AND_TOOLS/how-powers-work.md) · [Debug](../05_DEBUG_AND_DEVELOPER_TOOLS/debug-menu.md)
