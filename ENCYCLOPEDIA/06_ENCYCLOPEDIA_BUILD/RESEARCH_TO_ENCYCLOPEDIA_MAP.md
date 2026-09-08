# RESEARCH TO ENCYCLOPEDIA MAP

**Фаза:** C1  
**Дата:** 2026-09-08  
**Назначение:** карта «какой исследовательский документ чем становится в рабочей энциклопедии».  
**Не делает:** интеграцию статей. Это план слияния для фазы C2.

Легенда колонки **Действие C2:**

| Действие | Смысл |
|---|---|
| **NEW** | создать player-статью; в `04` канона нет |
| **UPDATE** | обновить существующую статью `04` player-блоками и статусом |
| **SPLIT** | одна обзорная `04` → несколько player-статей |
| **LINK** | оставить `04` как симуляционный якорь, не копировать |
| **ARCHIVE_ONLY** | не тащить в рабочую энциклопедию |

Статусы фактов при сборке: **CONFIRMED** · **REQUIRES_LIVE_VALIDATION** · **MOD_ONLY** · **INTERNAL**.

---

# 1. КОРПУСА

| Корпус | Путь | Что брать |
|---|---|---|
| Unified Encyclopedia | `04_UNIFIED_ENCYCLOPEDIA/` | CLOSED симуляция: классы, пайплайны, negative canon |
| Player Research | `05_PLAYER_RESEARCH/` | доступ игрока, границы контроля, ваниль vs моды vs debug |
| Legacy / Research | `02_`, `03_` | только если unique depth уже не в `04` (ономастика, city/social depth) |
| Extracts | `05_PLAYER_RESEARCH/_extract/` | справочник кнопок/окон; не статьи |

---

# 2. КАРТА `05_PLAYER_RESEARCH` → РАБОЧИЕ РАЗДЕЛЫ

Целевые разделы — `PROPOSED_ENCYCLOPEDIA_ARCHITECTURE.md`.

## Раздел 1. PLAYER INTERFACE AND CONTROL

| Источник | Канон `04` сейчас | Рабочая статья (план) | Действие C2 |
|---|---|---|---|
| `PLAYER_INTERFACE_ACCESS_MAP.md` | UI = MAP_ONLY | `interface-tabs-windows.md` | **NEW** |
| `PLAYER_ACTION_TRACE.md` | короткий вход в powers | `player-click-to-simulation.md` | **NEW** |
| `PLAYER_PREFAB_EVENT_COMPLETION.md` | нет | влить в interface + windows | **UPDATE** в NEW-статьи |
| `DEBUG_AND_DEVELOPER_TOOLS.md` | нет | `debug-menu-and-developer-tools.md` | **NEW** |
| `PLAYER_RESEARCH_SOURCE_MAP.md` | — | не статья игрока | **ARCHIVE_ONLY** / ссылка для AI |

Покрывает: вкладки сил, окна inspect, выбор объектов, редакторы, debug unlock, граница «кнопка есть ≠ ванильный доступ».

## Раздел 2. PLAYER POWERS AND TOOLS

| Источник | Канон `04` | Рабочая статья | Действие C2 |
|---|---|---|---|
| `GOD_POWERS_TRAIT_ACCESS.md` | `god-powers-drops-terraform.md` CLOSED architecture | `god-powers-player-guide.md` + обновить powers | **UPDATE** + **NEW** player-guide |
| `TRAIT_EDITOR_SIMULATION_EFFECTS.md` | `actor-traits-modifiers-subspecies.md` | `trait-editor.md` | **NEW** |
| `TRAIT_CALLBACK_DIRECT_EFFECTS.md` | traits CLOSED | секция traits / callbacks | **UPDATE** traits |
| `world-laws.md` (04) | CLOSED execution | `world-laws-player-toggles.md` | **UPDATE** player-блоками |
| buildings + watch towers `05` | `buildings.md` | кисти стен / drops башен | см. раздел 7 |

Отделить явно: God Power · Drop · spawn · terraform brush · UI overlay · diplomacy power · **MOD_ONLY** PowerBox.

## Раздел 3. NPC

| Источник | Канон `04` | Рабочая статья | Действие C2 |
|---|---|---|---|
| `NPC_CORE_STATE_AND_AI_ARCHITECTURE.md` | architecture, lifecycle, actor-ai-decisions, mind | `npc-what-it-is.md`, `npc-stats-and-abilities.md`, `npc-ai-decisions-tasks.md`, `possession-and-player-control.md` | **NEW** player + **UPDATE** AI/architecture статусами |
| `TRAIT_EDITOR` + `TRAIT_CALLBACK` + traits `04` | traits CLOSED | `npc-traits.md` | **UPDATE** + player overlay |
| `actor-events-status-lifecycle.md` | CLOSED | `npc-statuses.md` | **LINK** + короткий player |
| `actor-magic-spells.md` | CLOSED | `npc-magic.md` | **LINK** |
| `actor-items-equipment.md` | CLOSED | `npc-equipment.md` | **LINK** |
| inspect / debug `05` | нет | `npc-inspect-windows.md` | **NEW** |

Ключ интеграции: слой `updateStats` (subspecies, clan, language, culture, **не religion base_stats**), Possession пропускает Decision + `ai.update`.

## Раздел 4. SPECIES AND POPULATION

| Источник | Канон `04` | Рабочая статья | Действие C2 |
|---|---|---|---|
| `SPECIES_SUBSPECIES_BIRTH_GENETICS_PLAYER_ACCESS.md` | sapience + traits subspecies | `species.md`, `subspecies.md`, `genetics.md`, `birth-traits.md` | **NEW** |
| `SUBSPECIES_LIVE_VALIDATION_AND_POPULATION_CONTROL.md` | нет | `subspecies-player-control.md` | **NEW** (пометка LIVE) |
| `REPRODUCTION_AND_POPULATION_GROWTH_PLAYER_ACCESS.md` | lifecycle PARTIAL overlap | `reproduction.md`, `population-growth.md` | **NEW** |
| `MORTALITY_SURVIVAL_AND_POPULATION_BALANCE.md` | status/aging CLOSED | `mortality.md` | **NEW** + **LINK** status |
| `catalog.md` / `classification.md` | CLOSED | справочник id видов | **LINK** |

## Раздел 5. CIVILIZATIONS

| Источник | Канон `04` | Рабочая статья | Действие C2 |
|---|---|---|---|
| `CITIZEN_JOBS_AND_CITY_ECONOMY.md` | actor-jobs, production, supply, resources | `citizen-jobs.md`, `city-economy.md` | **UPDATE** jobs/production + **NEW** player |
| `buildings.md` | CLOSED | `buildings-what-player-can-place.md` | **UPDATE** |
| `city-kingdom-governance.md` | PARTIAL | якорь City/Kingdom AI | **LINK** |
| `KINGDOM_SUCCESSION_ROYAL_CLAN_PLAYER_ACCESS.md` | governance | `succession.md` | **NEW** |
| `CITY_LEADERSHIP_LOYALTY_REBELLION_PLAYER_ACCESS.md` | governance | `city-leaders.md`, `loyalty.md` | **NEW** (rebellion — также раздел 7) |
| `kingdoms-and-civilization.md` | PARTIAL | `kingdoms.md` | **UPDATE** player |
| zones/borders/territory/expansion | CLOSED | `city-space.md` | **LINK** |
| city life + legacy depth | PARTIAL | только если нужен быт | **LINK** |

## Раздел 6. META SYSTEMS

| Источник | Канон `04` | Рабочая статья | Действие C2 |
|---|---|---|---|
| `CULTURE_PLAYER_ACCESS_AND_SIMULATION.md` | нет («NOT_CLOSED») | `culture.md` | **NEW** |
| `LANGUAGE_PLAYER_ACCESS_AND_SIMULATION.md` | нет | `language.md` | **NEW** |
| `RELIGION_PLAYER_ACCESS_AND_SIMULATION.md` | нет | `religion.md` | **NEW** |
| `BOOKS_META_SYSTEM_TRANSMISSION.md` | нет | `books.md` | **NEW** |
| `CLAN_BLOODLINE_PLAYER_ACCESS_AND_SIMULATION.md` | social якоря | `clan.md` | **NEW** |
| `FAMILY_PLAYER_ACCESS_AND_SIMULATION.md` | social-brain PARTIAL | `family.md` | **NEW** + **LINK** social |
| `PLOTS_RITES_PLAYER_ACCESS.md` | plots.md CLOSED | `plots-and-rites.md` | **UPDATE** plots + **NEW** player rites |
| onomastics `09` | LEGACY_UNIQUE | не приоритет v1 | **LINK** later |

## Раздел 7. POLITICS AND CONFLICT

| Источник | Канон `04` | Рабочая статья | Действие C2 |
|---|---|---|---|
| `WARS_PLAYER_ACCESS_AND_SIMULATION.md` | `war-diplomacy.md` NOT_CLOSED | `wars.md` | **SPLIT** / **NEW** + сменить статус `04` |
| `DIPLOMACY_PLAYER_ACCESS_AND_SIMULATION.md` | тот же файл | `diplomacy.md` | **NEW** |
| `POLITICAL_CONTROL_AND_ALLIANCE_CONSEQUENCES.md` | Alliance абзац | `alliances.md` | **NEW** |
| `CITY_LEADERSHIP_...` rebellion | governance | `rebellions.md` | **NEW** |
| `ARMIES_MILITARY_MOBILIZATION_AND_CITY_ATTACK.md` | VQ-03 NOT_CLOSED | `armies.md` | **NEW** |
| `UNIT_COMBAT_TARGETING_AND_BATTLE_CONSEQUENCES.md` | combat PARTIAL | `unit-combat.md` | **UPDATE** combat |
| `CITY_CAPTURE_AND_TERRITORIAL_CONTROL.md` | нет capture-статьи | `city-capture.md` | **NEW** |
| `WATCH_TOWERS_AND_DEFENSIVE_BUILDINGS.md` | buildings | `defense-watch-towers-walls.md` | **NEW** |
| `plots.md` startWar стык | CLOSED plots | related в wars | **LINK** |

PowerBox army create / convert city / EditResources → только **MOD_ONLY** врезки, не ванильные статьи.

## Раздел 8. WORLD SIMULATION

| Источник | Канон `04` | Рабочая статья | Действие C2 |
|---|---|---|---|
| `world-laws.md` | CLOSED | `world-laws.md` player | **UPDATE** |
| `world-ages.md` | CLOSED | `world-ages.md` | **LINK** + короткий player |
| disasters | CLOSED architecture | `disasters-and-environment.md` | **LINK** |
| NPC_CORE + population `05` | — | `ai-global-and-long-term.md` | **NEW** (сводка последствий) |
| Expeditions | NEGATIVE_CANON | `expeditions-do-not-exist.md` | **LINK** сохранить |
| biomes | MAP_ONLY | не выдумывать полноту | см. OPEN_RESEARCH_GAPS |
| boats/docks | NOT_CLOSED standalone | не блокировать v1 | gap |

## Раздел 9. PLAYER EXPERIMENTS

Источники: **все** `05` документы + player-статьи разделов 1–8.

Это не новое исследование. Это **индекс сценариев**, собранный из уже подтверждённых ограничений.

Планируемые карточки v1 (только из готовых фактов):

| Сценарий | Опирается на |
|---|---|
| Как начать войну между двумя королевствами | WARS, Whisper |
| Можно ли выбрать короля | SUCCESSION |
| Как назначить работу жителю | CITIZEN_JOBS → нельзя ванилью |
| Как заставить армию атаковать выбранный город | ARMIES → нельзя |
| Что будет, если поставить trait X | TRAIT_EDITOR, CALLBACKS |
| Как открыть Debug Menu | DEBUG |
| Почему NPC не размножается / город не растёт | REPRODUCTION, MORTALITY, JOBS |
| Можно ли поставить городскую сторожевую башню | WATCH_TOWERS |
| Что делает золотая пыль | CITIZEN_JOBS (`dust_gold`) |
| Как захватить город | CAPTURE, ARMIES, COMBAT, TOWERS |
| Possession: что игрок контролирует | NPC_CORE |
| Как создать / изменить подвид | SPECIES, SUBSPECIES |
| Unity / Discord | ALLIANCES |
| Почему нет Expeditions | expeditions NEGATIVE_CANON |

---

# 3. КАРТА `04_UNIFIED_ENCYCLOPEDIA` → НУЖНО ЛИ ТРОГАТЬ В C2

## Обновлять статус и ссылки (обязательно, иначе энциклопедия врёт)

| Файл | Почему |
|---|---|
| `README.md` | NOT_CLOSED / MAP_ONLY список устарел |
| `00_NAVIGATION/system-status.md` | то же |
| `00_NAVIGATION/knowledge-map.md` | нет маршрутов Culture/UI/War player |
| `00_NAVIGATION/how-to-use-this-encyclopedia.md` | должен указать рабочий слой игрока |
| `11_OPEN_RESEARCH/open-questions.md` | VQ-01/03 и UI/Culture как «нет прохода» — устарели *как системный статус*; тонкие VQ оставить |
| `03_ACTORS/connections.md` | player MAP_ONLY, meta NOT_CLOSED |
| `05_CIVILIZATIONS/war-diplomacy.md` | статус NOT_CLOSED |
| `10_REGISTRIES` OBJ-0016/0028/0029 / PlayerOptionData | Army/War/Player «нет канона» |

## Обновлять содержание player-блоками (приоритет v1)

| Файл | Влить из |
|---|---|
| `god-powers-drops-terraform.md` | GOD_POWERS, dust_gold clarification |
| `actor-ai-decisions.md` / mind | NPC_CORE (Possession, religion stats, mind tab) |
| `actor-jobs.md` | CITIZEN_JOBS |
| `actor-traits-modifiers-subspecies.md` | TRAIT_EDITOR, CALLBACKS, genetics player |
| `actor-combat-warfare.md` | UNIT_COMBAT |
| `buildings.md` | WATCH_TOWERS player limits |
| `plots.md` | PLOTS_RITES player |
| `production.md` / `supply.md` / resources | CITIZEN_JOBS (axe, pickaxe, stockpile, recipes without baker) |
| `city-kingdom-governance.md` | SUCCESSION, LEADERSHIP (не раздувать CityBeh dump) |
| `world-laws.md` | interface «где закон» |

## Можно оставить как SIM-якорь без переписывания v1

architecture, lifecycle, catalog, classification, items, magic, status (кроме player death tools), zones/borders/territory/expansion, disasters architecture, ages, sapience tags, onomastics, system-connections, architecture-map, build-and-config, object passports, expeditions negative, research-report.

## Не копировать в рабочую энциклопедию

- `02_ENCYCLOPEDIA_LEGACY` ART/MEC целиком
- `03_ENCYCLOPEDIA_RESEARCH` целиком
- `_extract` JSON как статьи
- `PLAYER_RESEARCH_SOURCE_MAP.md` как статью игрока
- Master V2

---

# 4. СЧЁТЧИК ИНТЕГРАЦИИ (C1)

| Метрика | Число |
|---|---|
| Предметных документов `05` | 27 |
| Служебных `05` | 3 |
| Статей/файлов `04` (md) | 65 |
| Документов `05`, уже влитых в `04` | **0** |
| Областей `04` CLOSED как симуляция | ~22 |
| Областей, помеченных NOT_CLOSED/MAP_ONLY, но закрытых в `05` для игрока | UI/Player, Debug, War, Diplomacy, Alliance, Army, Capture, Culture, Language, Religion, Books, Clan, Family, Succession, Loyalty, Rebellion |
| Приоритетных областей v1 (из ТЗ) | 8 (интерфейс, powers, NPC, AI, traits, статы/способности, species, debug) |

---

# 5. ПРАВИЛО СЛИЯНИЯ (чтобы не плодить каноны)

1. Если `04` CLOSED и факты верны — **не переписывать симуляцию**; добавить блоки игрока или отдельную player-статью со ссылкой.
2. Если `04` NOT_CLOSED, а `05` закрыл доступ игрока — **player-статья становится рабочим ответом**; `04` либо обновляет статус, либо остаётся техническим приложением.
3. Если факт есть только в `05` — **NEW**.
4. Моды этой копии (PowerBox, NML, ModernBox, RulerBox, TPI) никогда не смешивать с ванилью.
5. LIVE не выдумывать: в статьях писать REQUIRES_LIVE_VALIDATION там, где `05` так пометил.

Следующий шаг после утверждения архитектуры: сборка v1 по приоритету 1–8, не новое исследование.
