# Окна, inspect, выбор объектов

**Статус:** VANILLA CONFIRMED для цепочек inspect и Window-кнопок. Часть внутренних вкладок prefab — PARTIALLY CONFIRMED.

## WHAT PLAYER CAN DO

1. Открыть справочные окна с главной вкладки (законы, эпохи, списки королевств…).
2. Inspect юнита / зоны / meta → окно карточки **и** вкладка `selected_*`.
3. В карточке смотреть данные; часть кнопок ведёт в **редакторы** (это уже действие, не просмотр).

## WHERE TO FIND IT

Инструмент **inspect** — вкладка `main`, GodPower `inspect`. Клик по юниту/зоне при соответствующем слое: `ActionLibrary.inspect*` + `MetaTypeLibrary`.

| Meta | Окно | Вкладка HUD после выбора |
|---|---|---|
| Unit | `unit` | `selected_unit` |
| City | `city` | `selected_city` |
| Kingdom | `kingdom` | `selected_kingdom` |
| Culture / Language / Religion / Subspecies / Clan / Family / Army / Alliance / War / Plot / Item | одноимённые id | `selected_*` |

Списки на **noosphere** (`list_cultures`, `list_wars`, …) открывают перечень; клик по строке → карточка / selected-вкладка.

### Кнопки на `selected_unit` (level1)

`main_info`, `favorite`, `unit_possession`, `unit_spectate`, `unit_trait_editor`, `unit_equipment_editor`, `unit_mind`, `unit_genealogy`, `unit_plots`.

Цепочки UnityEvent → `ButtonEvent.openUnitTab*` / `clickPossess` — CONFIRMED выгрузкой сцены (фаза 2).

### Город

`main_info`, favorite, inventory, books, families, interesting people, pyramid, statistics. Склад — **просмотр** количеств, клик не выдаёт ресурсы.

### Культура / подвид / язык / клан / королевство

Есть кнопки trait editor (и onomastics у культуры; genetics + birth traits у подвида).  
**Аномалия:** дети `selected_religion` названы как `clan_*`. Не утверждать, что редактор религии = редактор клана. PARTIALLY CONFIRMED + REQUIRES LIVE VALIDATION.

### Multiple units

Вкладка `multiple_units` есть. Детей `PowerButton` **0**. UI — `SelectedMultipleUnitsTab` (аватары, status, equipment). Набор массовых приказов с этой вкладки **не** инвентаризирован как GodPower.

Открытие окна юнита **сбрасывает** мультивыбор (`openUnitWindow`). Trait editor всегда пишет **одного** `SelectedUnit.unit`.

### Здание

`selected_building` в `PowerTabLibrary` — пустой stub. Отдельной вкладки здания на `level1` нет.

## WHAT HAPPENS AFTER THE ACTION

Inspect / favorite / spectate / Mind / Genealogy / списки войн — сами по себе **не** меняют симуляцию (кроме флага favorite и побочного `unlock()` ассета plot при открытии карточки).

Редакторы и possession — меняют. См. [editors](editors.md), [possession](possession-and-plots-ui.md).

## WHAT AI / SIMULATION DECIDES

Карточка показывает состояние, которое AI уже посчитал (работа, plot, last decision на Mind). Игрок не выбирает Decision кнопкой Mind: симуляция вкладки Mind с `pGameplay: false`.

## LIMITATIONS

- Просмотр ≠ действие.
- Customize-окна (`*_customize`) есть в библиотеке; кнопки внутри prefab не все сняты (PARTIALLY CONFIRMED).
- Окно `debug` не открывается с главных вкладок. См. раздел 05.

## RELATED SYSTEMS

[Редакторы](editors.md) · [NPC inspect](../03_NPC_AND_AI/what-is-an-npc.md) · [Debug AI](../05_DEBUG_AND_DEVELOPER_TOOLS/debug-menu.md)
