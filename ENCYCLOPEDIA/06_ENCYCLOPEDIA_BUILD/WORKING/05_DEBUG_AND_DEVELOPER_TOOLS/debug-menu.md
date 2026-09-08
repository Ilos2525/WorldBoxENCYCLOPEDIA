# Debug Menu

## Как открыть

**VANILLA DEBUG (код):**

```
клик по объекту с GraphyCaller.click()
  → счётчик; на 11-м клике (clicked > 10)
  → DebugOption.DebugButton toggle
  → bug-кнопка HUD
```

Привязка UI: код не содержит слово burger. Публичные гайды: **Settings → иконка burger сверху слева, 11 раз**, затем bug **сверху справа**. **REQUIRES LIVE VALIDATION** конкретного GameObject; механика счётчика CONFIRMED.

Unlock **не пишется в save** (кроме цикла DisablePremium/TestAds — PARTIALLY CONFIRMED, ломает premium). Обычные 11 кликов = **сессия**.

Unity Editor: `Config.isEditor` сразу показывает кнопку. В релизе false.

Консоль: клавиша `~` **всегда** в хоткеях — лог, **не** командный чит, debug unlock не нужен. `clickConsole()` тем же счётчиком (гайд: дракон в settings) — REQUIRES LIVE для иконки.

Achievement `god_mode` при открытии окна debug.

## Что доступно после unlock

1. Bug HUD → окно `debug` (`UiDebugWindow`, `is_testable = false`)
2. Вкладки фильтруют кнопки debug-опций
3. New Debug Window → `DebugTool` панели
4. Overlay `DebugLayer` только пока bug-кнопка active

### Вкладки окна debug — LIVE CONFIRMED (игрок)

В живой игре у окна debug **6 вкладок**:

| # | Вкладка | Зачем (по смыслу) | Полный список кнопок |
|---|---|---|---|
| 1 | **Абсолютно все** | все debug-кнопки сразу | ещё не разобран |
| 2 | **Отладочные стрелки** | визуальные стрелки/линии на карте (пути, цели и т.п.) | ещё не разобран |
| 3 | **Карта** | оверлеи и отладка карты | ещё не разобран |
| 4 | **Курсор** | что связано с курсором / подсветкой под мышью | ещё не разобран |
| 5 | **Читы** | опции, которые ломают или ускоряют симуляцию | частично (см. ниже) |
| 6 | **Система** | включить/выключить куски симуляции | частично (см. ниже) |

Имена вкладок — с экрана игрока. Полный dump каждой кнопки по вкладкам — **OPEN**: нужен скрин или список названий.

## Что только наблюдать (полезно для AI)

| Инструмент | Показывает | Не показывает |
|---|---|---|
| `DebugTooltipActorAI` | wait, **task, action, job, citizen_job**, profession | текущий Decision id |
| Unit Info | job, task, HP, city, attack_target, path | — |
| Actor AI | job, next task, task, action у юнита под курсором | — |
| Actor Decisions | веса возможных Decision, `pGameplay: false` | не ставит task в игру |
| Actor Stats | полный `actor.stats` | — |
| City Capture / Loyalty / city_jobs | город | — |
| Last Decision | **ванильный Mind**, не debug | — |

Гены конкретного NPC в debug нет — смотреть Subspecies editor.

## Что реально меняет симуляцию (читы)

| Опция | Эффект |
|---|---|
| SonicSpeed | мир ×40; слот в clock если debug_enabled |
| FastSpawn / UltraFastSpawn | спавн без обычной задержки |
| UnlockAllTraits/Equipment/Genes/Actors/Plots | снимает lock **ассетов**, не addTrait выбранному |
| CityInfiniteResources, FastConstruction/Upgrades/PopGrowth, UnlimitedHouses/ZoneRange | ломает экономику/рост |
| IgnoreDamage | `getHit` early return |
| SystemCityTasks / SystemUpdateUnits / … off | останавливает тики (вкладка **Система**) |
| CitizenJob* toggle | фильтр слотов работ |
| MakeUnitsFollowCursor | чит поведения (скорее **Курсор** / **Читы**) |
| DisablePremium / TestAds | ломает премиум, частично persist |

Обычные пауза/скорость clock — VANILLA, не debug. Trailer F7/F8 sonic — INTERNAL (`TRAILER_MODE=false`).

### Вкладка «Система» — что известно

Выключатели вида **System…** останавливают отдельные тики симуляции (пример: городские задачи, обновление юнитов).  
Полный список кнопок вкладки в базе **ещё нет** — нужен список с экрана.

### Вкладки «Отладочные стрелки» / «Карта» / «Курсор»

По коду известны инструменты наблюдения (Actor AI под курсором, Unit Info, City Capture/Loyalty и т.д.), но **какая кнопка на какой вкладке** — не разложено. Не выдумывать раскладку.

## Что НЕ является ванильной игрой

Весь этот раздел после unlock. Не отвечать «игрок может SonicSpeed» без пометки DEBUG.

Консоль ≠ Lua. `initDebugHotkeys` (Ctrl+V budding, N kill, PageUp maps) **нигде не вызывается** — INTERNAL.

`Config.editor_maxim` и подобные — false, не игрок.

## MOD_ONLY

Вкладка PowerBox, EditResources, army create — **не** окно `debug`.

## LIMITATIONS

Нет кнопки debug «выдать trait этому NPC».  
Состав **6 вкладок** — LIVE CONFIRMED. Полные списки кнопок по вкладкам — ещё OPEN.  
Цикл clearDebugOnStart vs premiumDisabled — PARTIALLY CONFIRMED.

## RELATED SYSTEMS

[AI просмотр](../03_NPC_AND_AI/ai-pipeline.md) · [Уровни UI](../01_INTERFACE_AND_CONTROL/access-levels.md)
