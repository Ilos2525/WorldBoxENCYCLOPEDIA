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
2. Вкладки фильтруют кнопки debug-опций (каталог ниже — LIVE)
3. В коде также есть путь **New Debug Window → DebugTool** (Actor AI, Unit Info…); во вкладках окна debug этих кнопок **нет** (LIVE NEGATIVE). Как открыть New Debug Window в билде игрока — OPEN
4. Overlay `DebugLayer` только пока bug-кнопка active

### Вкладки окна debug — LIVE CONFIRMED (игрок)

| # | Вкладка |
|---|---|
| 1 | **Абсолютно всё** |
| 2 | **Отладочные стрелки** |
| 3 | **Карта** |
| 4 | **Курсор** |
| 5 | **Читы** |
| 6 | **Система** |

---

## Каталог кнопок — LIVE dump игрока

Источник: перечисление с экрана. Игрок отметил: **не полный dump**, но раскладка по вкладкам в большинстве верная.

Легенда эффекта:
- **CONFIRMED** — эффект закрыт исследованиями энциклопедии
- **по имени** — перевод/смысл по названию; глубокий эффект не разобран
- **осторожно** — ломает сейв/премиум/«честное» время

Имена кнопок — **как в игре** (английские id).

### 1. Абсолютно всё

#### General

| Кнопка | Перевод | Что делает |
|---|---|---|
| FastSpawn | быстрый спавн | **CONFIRMED:** убирает обычную задержку спавна |
| Graphy | Graphy (оверлей FPS) | **по имени:** включает оверлей производительности Graphy |
| SonicSpeed | сверхскорость | **CONFIRMED:** мир ×40; ломает «честное» время |
| ShowAmountNearArmy | число у армии | **по имени:** показывает численность рядом с армией |
| ShowOrsicText | текст Orsic (?) | **по имени:** отладочный текст на экране; точный смысл id не закрыт |
| ShowCityWeapons | оружие города | **по имени:** показывает оружие/вооружение города |
| ShowFoodCityText | еда города текстом | **по имени:** текст еды у города |
| RendBigItems | большие предметы | **по имени:** рендер крупных предметов (имя похоже на Render) |
| RenderFavoritePods | поды избранных | **по имени:** рисует маркеры/поды избранных юнитов |
| RenderHoldingResources | ресурсы в руках | **по имени:** показывает ресурсы, которые несёт юнит |
| BenchAiEnabled | бенч AI | **по имени:** включает бенчмарк/замер AI |

#### Overlay Debug Text

| Кнопка | Перевод | Что делает |
|---|---|---|
| OverlayCity | оверлей города | **по имени:** debug-текст поверх городов |
| OverlayKingdom | оверлей королевства | **по имени:** debug-текст поверх королевств |
| OverlayActorCivs | оверлей civ-юнитов | **по имени:** debug-текст на цивилизованных юнитах |
| OverlayActorMobs | оверлей мобов | **по имени:** debug-текст на мобах |
| OverlayActorGroupLeaderOnly | только лидеры групп | **по имени:** оверлей только у лидеров групп |
| OverlayCursorActor | оверлей юнита под курсором | **по имени:** debug-текст на актёре под курсором |

### 2. Отладочные стрелки

| Кнопка | Перевод | Что делает |
|---|---|---|
| KingdomDrawAttackTarget | цель атаки королевства | **по имени:** стрелка к цели атаки королевства |
| CivDrawSettleTarget | цель поселения | **по имени:** куда civ хочет селиться |
| ArrowsOnlyForCursorCities | стрелки только у городов под курсором | **по имени:** фильтр — стрелки лишь для городов у курсора |
| ArrowsUnitsAttackTargets | цели атаки юнитов | **CONFIRMED по смыслу боя:** стрелки к `attack_target` |
| ArrowUnitsBehActorTarget | цель поведения юнита | **по имени:** стрелка к цели текущего behaviour |
| ArrowUnitsNavigationTargets | цели навигации | **по имени:** куда юнит навигирует |
| ArrowsUnitsPaths | пути юнитов | **по имени:** рисует path юнитов |
| ArrowsUnitsFavoritesOnly | только избранные | **по имени:** стрелки лишь у favorite |
| ArrowsUnitsNextStepPosition | позиция следующего шага | **по имени:** точка следующего шага |
| ArrowsUnitsNextStepTile | тайл следующего шага | **по имени:** клетка следующего шага |
| ArrowsUnitsCurrentPosition | текущая позиция | **по имени:** маркер текущей позиции |
| BoatPassengerLines | линии пассажиров лодки | **по имени:** связи лодка ↔ пассажиры |
| BuildingResidents | жители здания | **по имени:** линии/связи жителей со зданием |
| Lovers | пары / любовники | **по имени:** линии между парами |
| CivDrawCityClaimZone | зона клейма города | **по имени:** рисует claim-зону города |

### 3. Карта

#### Paths

| Кнопка | Перевод | Что делает |
|---|---|---|
| PathRegions | регионы пути | **по имени:** регионы pathfinding |
| ActivePaths | активные пути | **по имени:** текущие живые пути |
| LastPath | последний путь | **по имени:** последний посчитанный путь |

#### Display Map Overlay

| Кнопка | Перевод | Что делает |
|---|---|---|
| Chunks | чанки | **по имени:** сетка чанков карты |
| CityZones | зоны городов | **по имени:** границы/зоны городов |
| Buildings | здания | **по имени:** оверлей зданий |
| CityPlaces | места города | **по имени:** слоты/места планировки города |
| CitySettleCalc | расчёт поселения | **по имени:** отладка расчёта «куда селиться» |
| DisplayUnitTiles | тайлы юнитов | **по имени:** какие тайлы заняты юнитами |
| RenderCityDangerZones | опасные зоны города | **по имени:** зоны опасности города |
| RenderCityCenterZones | центральные зоны | **по имени:** центр города |
| RenderCityFarmPlaces | места ферм | **по имени:** фермерские клетки |
| RenderVisibleZones | видимые зоны | **по имени:** какие зоны считаются видимыми |

#### Dirty

| Кнопка | Перевод | Что делает |
|---|---|---|
| ChunksDirty | грязные чанки | **по имени:** чанки, помеченные dirty на перерисовку/пересчёт |

### 4. Курсор

| Кнопка | Перевод | Что делает |
|---|---|---|
| UnitIsInside | юнит внутри | **по имени:** показывает, внутри ли юнит (здание/зона и т.п.) |
| TargetedBy | кем целятся | **по имени:** кто целится в юнита под курсором |
| UnitKingdoms | королевства юнита | **по имени:** info о kingdom-связях юнита под курсором |

### 5. Читы

| Кнопка | Перевод | Что делает |
|---|---|---|
| FastCultures | быстрые культуры | **по имени:** ускоряет культуру/meta-культуру |
| CityInfiniteResources | бесконечные ресурсы города | **CONFIRMED:** склад не кончается |
| CityFastConstruction | быстрая стройка | **CONFIRMED:** ускоряет строительство |
| CityFastPopGrowth | быстрый рост населения | **CONFIRMED:** ускоряет рост |
| CityFastZonesGrowth | быстрый рост зон | **по имени:** ускоряет расширение зон города |
| CityFastUpgrades | быстрые апгрейды | **CONFIRMED:** ускоряет улучшения |
| CityUnlimitedHouses | без лимита домов | **CONFIRMED:** снимает лимит домов |
| CityUnlimitedZoneRange | без лимита зоны | **CONFIRMED:** снимает лимит зоны |
| UnitsAlwaysFast | юниты всегда быстрые | **по имени:** юниты двигаются/действуют ускоренно |

Обычные пауза/скорость часов — **ваниль**, не эта вкладка.

### 6. Система

#### Greg

| Кнопка | Перевод | Что делает |
|---|---|---|
| Greg | Greg | **по имени:** debug-флаг/сущность Greg; глубокий эффект в базе не разобран |

#### Mobile

| Кнопка | Перевод | Что делает |
|---|---|---|
| DisablePremium | отключить премиум | **CONFIRMED / осторожно:** ломает премиум; часть может persist |

#### System

| Кнопка | Перевод | Что делает |
|---|---|---|
| SystemUnitPathfinding | pathfinding юнитов | выкл → **по имени:** стоп поиска путей юнитов |
| SystemZoneGrowth | рост зон | выкл → **по имени:** зоны не растут |
| SystemBuildTick | тик строительства | выкл → **по имени:** стройка не тикает |
| SystemCityPlaceFinder | поиск мест города | выкл → **по имени:** город не ищет новые place |
| SystemWorldBehaviours | world behaviours | выкл → **по имени:** мировые поведения стоп |
| SystemProduceNewCitizens | производство граждан | выкл → **по имени:** новые граждане не появляются этим контуром |
| SystemCheckUnitAction | проверка действий юнита | выкл → **по имени:** проверки action стоп |
| SystemRedrawMap | перерисовка карты | выкл → **по имени:** карта не перерисовывается этим тиком |
| SystemUpdateUnits | обновление юнитов | **CONFIRMED:** выкл → юниты не обновляются |
| SystemUpdateBuildings | обновление зданий | выкл → **по имени:** здания не обновляются |
| SystemUpdateCities | обновление городов | выкл → **по имени:** города не обновляются |
| SystemCityTasks | задачи города | **CONFIRMED:** выкл → городские задачи стоп |
| SystemUpdateDirtyChunks | dirty-чанки | выкл → **по имени:** dirty-чанки не обновляются |
| UseGlobalPathLock | глобальный lock путей | **по имени:** включает/выключает глобальную блокировку path |
| SystemCheckGoodForBat | check good for bat | **по имени:** проверка пригодности (bat); детали OPEN |
| SystemSplitAStar | split A* | **по имени:** режет/дробит A* pathfinding |
| UseCacheForRegionPath | кэш region path | **по имени:** кэш путей по регионам |
| ParallelJobUpdater | параллельный job updater | **по имени:** параллельное обновление job |
| ParallelChunks | параллельные чанки | **по имени:** параллельная обработка чанков |
| ChunkBatches — 128 | батчи чанков 128 | **по имени:** размер батча чанков = 128 |
| ScaleEffectEnabled | scale-эффекты | **по имени:** вкл/выкл эффектов масштаба |
| UseCameraAspect | aspect камеры | **по имени:** учитывать соотношение сторон камеры |
| AddJobManagerSkips | пропуски job manager | **по имени:** добавляет skip’и в job manager |
| MakeUnitsFollowCursor | юниты за курсором | **CONFIRMED:** юниты бегут за мышкой (**вкладка Система**, не Курсор) |
| DrawBadLinksDiag | плохие связи (diag) | **по имени:** рисует диагностику битых связей |
| DebugIdleSounds | idle-звуки | **по имени:** отладка idle-звуков |
| PauseOnStart | пауза на старте | **по имени:** мир стартует на паузе |

---

## Где НЕ искать: опции из кода без кнопок во вкладках

**LIVE NEGATIVE (игрок):** по всем 6 вкладкам окна `debug` **нет** кнопок  
`UnlockAll*`, `IgnoreDamage`, `UltraFastSpawn`, `TestAds`, `Actor AI`, `Unit Info`.

Это не «недописанный dump». Игрок специально искал — их там нет.

| Имя | Что говорит старое исследование | Где реально искать / статус |
|---|---|---|
| UnlockAllTraits / Equipment / Genes / Actors / Plots | снимают lock ассетов | В коде есть `debugUnlockAll` / опции; **кнопок на главных вкладках нет** (`editors.md`). Во вкладках окна debug — **нет**. Не выдавать за доступную кнопку. |
| IgnoreDamage | урон не проходит | Упоминался как DEBUG-опция в коде; **кнопки во вкладках нет**. Статус доступа: OPEN / возможно мёртвый UI или Editor-only. |
| UltraFastSpawn | ещё быстрее FastSpawn | Рядом с FastSpawn в коде; в LIVE есть только **FastSpawn** (вкладка Абсолютно всё → General). Ultra — **кнопки нет**. |
| TestAds | тест рекламы, persist | В паре с DisablePremium в старых заметках; в LIVE есть только **DisablePremium** (Система → Mobile). TestAds — **кнопки нет**. |
| Actor AI / Unit Info / Actor Decisions / Actor Stats / ShowHiddenStats | инструменты наблюдения | Это не тумблеры вкладок. В архитектуре: **New Debug Window → DebugTool** панели + tooltip `DebugTooltipActorAI`. Как открыть New Debug Window с bug-HUD в этом билде — **OPEN / REQUIRES LIVE** (отдельная кнопка/окно, не вкладка). |
| City Capture / Loyalty / city_jobs / World Laws tool | наблюдение | Тоже скорее DebugTool / отдельные tools, не чекбоксы 6 вкладок. |
| CitizenJob* / DrawCitizenJobIcons | фильтры работ | В LIVE-dump вкладок **не найдены**. |

### Чем заменить наблюдение AI без Actor AI / Unit Info

Пока DebugTool не найден на экране:

| Вместо | Живые кнопки из dump |
|---|---|
| кто кого бьёт / куда идёт | Отладочные стрелки: `ArrowsUnitsAttackTargets`, `ArrowsUnitsPaths`, `ArrowUnitsBehActorTarget` |
| текст на юните под курсором | `OverlayCursorActor` + вкладка Курсор (`TargetedBy`, `UnitIsInside`, `UnitKingdoms`) |
| last Decision | **ванильный** Mind у юнита (debug не нужен) |

---

## Что потыкать для масштабных наблюдений

Цель: увидеть **большие** сдвиги симуляции, не микро-чит одного юнита.

### A. Ускорить цивилизацию и смотреть рост — вкладка Читы

Включить вместе: `CityInfiniteResources` + `CityFastConstruction` + `CityFastPopGrowth` + `CityFastZonesGrowth` + `CityFastUpgrades` (+ по желанию `FastCultures`, `UnitsAlwaysFast`).  
Опционально сверху: `SonicSpeed` (Абсолютно всё).  
Смотреть: взрывной рост городов, зон, домов, апгрейдов.

### B. Выключить кусок мира и смотреть, что умрёт — вкладка Система

По одному (чтобы было ясно, что сломалось):

| Выключить | Ожидаемый масштабный эффект |
|---|---|
| `SystemProduceNewCitizens` | население перестаёт пополняться этим контуром |
| `SystemZoneGrowth` | города перестают расползаться |
| `SystemBuildTick` | стройка встаёт |
| `SystemCityTasks` | городские работы/задачи стоп |
| `SystemUpdateCities` | города «замирают» целиком |
| `SystemUpdateUnits` | юниты перестают обновляться |
| `SystemWorldBehaviours` | мировые поведения стоп |
| `SystemUnitPathfinding` | массовый хаос движения / топтание |

### C. Война и экспансия глазами стрелок — Отладочные стрелки + Карта

Война: `KingdomDrawAttackTarget` + `ArrowsUnitsAttackTargets` + `ArrowsUnitsPaths` (+ `ActivePaths` на Карте).  
Экспансия: `CivDrawSettleTarget` + `CivDrawCityClaimZone` + `CitySettleCalc` / `CityZones` / `RenderCityFarmPlaces`.  
Социум: `Lovers` + `BuildingResidents`.

### D. Не для «интересного мира»

`DisablePremium` — ломает премиум.  
`MakeUnitsFollowCursor` — ломает естественный AI.  
`Parallel*` / `ChunkBatches` / `SystemSplitAStar` — тюнинг движка, не зрелище.  
`Greg` — неизвестно; не первый кандидат.

Last Decision во вкладке Mind юнита — **ваниль**, не debug.  
Гены одного NPC в debug нет — смотри редактор подвида.

## Что НЕ является ванильной игрой

Весь этот раздел после unlock. Не отвечать «игрок может SonicSpeed» без пометки DEBUG.

Консоль ≠ Lua. `initDebugHotkeys` (Ctrl+V budding, N kill, PageUp maps) **нигде не вызывается** — INTERNAL.

`Config.editor_maxim` и подобные — false, не игрок.

## MOD_ONLY

Вкладка PowerBox, EditResources, army create — **не** окно `debug`.

## LIMITATIONS

Нет кнопки debug «выдать trait этому NPC».  
Состав **6 вкладок** + каталог — LIVE от игрока.  
**LIVE NEGATIVE:** UnlockAll*, IgnoreDamage, UltraFastSpawn, TestAds, Actor AI, Unit Info — **не** кнопки этих вкладок.  
Где эффект только «по имени» — не выдавать за закрытое исследование.  
Как открыть New Debug Window / DebugTool в этом билде — OPEN.  
Цикл clearDebugOnStart vs premiumDisabled — PARTIALLY CONFIRMED.

## RELATED SYSTEMS

[AI просмотр](../03_NPC_AND_AI/ai-pipeline.md) · [Уровни UI](../01_INTERFACE_AND_CONTROL/access-levels.md)
