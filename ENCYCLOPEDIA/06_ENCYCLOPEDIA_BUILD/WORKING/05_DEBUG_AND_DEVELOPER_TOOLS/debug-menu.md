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

Два разных UI (не путать):

| | Первое окно | Второе меню |
|---|---|---|
| Что | окно `debug` / `UiDebugWindow` | плавающая панель `DebugTool` |
| Как | bug-кнопка HUD | кнопка **рамки** первого окна: `NewDebugWindow` |
| Содержимое | 6 вкладок тумблеров (`UiDebugButton` = DebugOption) | dropdown инструментов: Actor AI, Unit Info… |
| Prefab | ScrollWindow id `debug` | `PrefabLibrary.debugTool` на `DebugConfig` |

1. Bug HUD → окно `debug` (`is_testable = false`)
2. Вкладки фильтруют DebugOption (каталог ниже — LIVE)
3. **New Debug Window** → `DebugTool` — **CONFIRMED** в player build (см. ниже)
4. Overlay `DebugLayer` только пока bug-кнопка active (рисует зоны/чанки по опциям вкладок)

### Как открыть New Debug Window — CONFIRMED (код + LIVE игрок)

```
Settings → GraphyCaller ×11 → bug HUD
  → открыть окно debug (6 вкладок)
  → наверху / на РАМКЕ окна (не внутри списков вкладок) клик NewDebugWindow
  → DebugConfig.createTool("Game Info")
  → Instantiate(debugTool) → dropdown DebugToolAsset type == Default
```

**LIVE (игрок):** сверху в debug-окне есть кнопки → открываются плавающие панельки с информацией; в списке режимов есть Actor AI и остальные DebugTool.

Вторая кнопка рамки: `NewDebugWindow (1)` → сразу `Benchmark All` (dropdown type == Benchmarks).

- Хоткея на DebugTool в релизе **нет**
- `createTool` **не** завязан на `Config.isEditor` / `TRAILER_MODE`
- `debug_enabled` = bug-кнопка active; на createTool не влияет
- Панель закрыть: `DebugTool.clickClose()`; можно duplicate → ещё одна панель
- Автоспавн панелей по `show_on_start` в релизе **мёртв**

### Dropdown Default (примеры панелей)

Game Info, Basic Info, **Unit Info**, **Actor Stats**, **Actor AI**, **Actor Decisions**, Decisions Globals Use, Selected Unit, City Info, **City Capture**, **City Loyalty**, city_jobs, City Tasks, City Professions, city_storage, Cities, **World Laws**, Kingdoms Civ, Kingdoms Wild, Armies, Cultures, Religions, Languages, Families, Subspecies, Population, Building Info, Boat AI, City AI, Kingdom AI, …

UnlockAll / IgnoreDamage / ShowHiddenStats в этом dropdown **нет** — это не DebugTool.

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

## Где НЕ искать / DEAD UI / DebugTool

**LIVE NEGATIVE во вкладках:** `UnlockAll*`, `IgnoreDamage`, `UltraFastSpawn`, `TestAds`, `Actor AI`, `Unit Info` — не `UiDebugButton`.

| Имя | Статус в этом билде | Где |
|---|---|---|
| Actor AI / Unit Info / Actor Decisions / Actor Stats / City Capture / City Loyalty / city_jobs / World Laws | **VANILLA DEBUG** | NewDebugWindow → dropdown DebugTool |
| UnlockAllTraits / Equipment / Genes / Actors / Plots | **DEAD UI** | enum/код есть (lock ассетов), GO кнопки в ассетах **нет** |
| IgnoreDamage | **DEAD UI** | код в `getHit`, кнопки нет |
| UltraFastSpawn | **DEAD UI** | код спавна есть, кнопки нет (есть только FastSpawn) |
| TestAds | **DEAD UI** | код ads/persist, кнопки нет (есть DisablePremium) |
| ShowHiddenStats | **DEAD UI** | только флаги `editor_maxim` / `editor_nikon` |
| DebugTooltipActorAI | **DEAD UI** | если флаг ON — дописывает task/job в обычный tooltip; GO кнопки нет → из вкладок не включить |
| debugUnlockAll | **INTERNAL / DEAD UI** | `ButtonEvent` → прогресс/ачивки, не UnlockAllTraits; без OnClick на prefab |
| F7/F8 FastSpawn/Sonic | **INTERNAL** | только `TRAILER_MODE` (= false) |
| initDebugHotkeys | **INTERNAL / DEAD** | не вызывается |
| CitizenJob* / DrawCitizenJobIcons | не в LIVE-dump вкладок | статус UI OPEN |

### Чем смотреть AI

| Цель | Инструмент |
|---|---|
| job / task / action под курсором | DebugTool → **Actor AI** / **Unit Info** |
| веса Decision | DebugTool → **Actor Decisions** |
| last Decision | **ванильный Mind** (debug не нужен) |
| стрелки на карте | вкладки Отладочные стрелки (дополнительно) |

Не скроллить 6 вкладок в поисках «Actor AI». Клик по кнопкам **рамки** окна debug.

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
**New Debug Window → DebugTool** — CONFIRMED (рамка окна debug, не вкладки).  
UnlockAll* / IgnoreDamage / UltraFastSpawn / TestAds / ShowHiddenStats / DebugTooltipActorAI как кнопки — **DEAD UI** в этом билде.  
Где эффект только «по имени» — не выдавать за закрытое исследование.  
Цикл clearDebugOnStart vs premiumDisabled — PARTIALLY CONFIRMED.  
**LIVE CONFIRMED:** кнопки сверху debug-окна открывают DebugTool-панели (Actor AI и др.).

## RELATED SYSTEMS

[AI просмотр](../03_NPC_AND_AI/ai-pipeline.md) · [Уровни UI](../01_INTERFACE_AND_CONTROL/access-levels.md)
