# ENCYCLOPEDIA AUDIT

**Фаза:** C1  
**Дата:** 2026-09-08  
**Статус:** аудит завершён. Массовое переписывание энциклопедии **не начато**.  
**Канон симуляции (текущий повседневный вход):** `WorldBox Research/04_UNIFIED_ENCYCLOPEDIA/`  
**Исследования игрока (не интегрированы):** `WorldBox Research/05_PLAYER_RESEARCH/`

Словарь этого аудита:

| Метка | Значение |
|---|---|
| **CANON_04** | статья в `04_UNIFIED_ENCYCLOPEDIA` |
| **PLAYER_05** | документ в `05_PLAYER_RESEARCH` |
| **ARCHIVE** | `02_ENCYCLOPEDIA_LEGACY` / `03_ENCYCLOPEDIA_RESEARCH` — не повседневная навигация |
| **STALE_STATUS** | статус в `04` не отражает уже подтверждённое исследование `05` |
| **SIM_ONLY** | статья описывает код/симуляцию, но не цепочку игрока |

---

# CURRENT ENCYCLOPEDIA STRUCTURE

## Где находится основная энциклопедия

**Единственная повседневная энциклопедия:**  
`E:\worldboxGAME\WorldBox Research\04_UNIFIED_ENCYCLOPEDIA\`

Это прямо зафиксировано в её `README.md` и `00_NAVIGATION/how-to-use-this-encyclopedia.md`: новые правки — только сюда; `02_` и `03_` — исходники сборки / архив.

**Исследования ванильного игрока (не энциклопедия):**  
`E:\worldboxGAME\WorldBox Research\05_PLAYER_RESEARCH\`

**Этот этап сборки:**  
`E:\worldboxGAME\WorldBox Research\06_ENCYCLOPEDIA_BUILD\`

## Слои корпуса (не путать)

| Слой | Путь | Роль сейчас | Для рабочей энциклопедии игрока |
|---|---|---|---|
| Unified Encyclopedia | `04_UNIFIED_ENCYCLOPEDIA/` | канон **симуляции** (классы → механика) | исходник фактов; структура **не** отвечает на «что может игрок» |
| Player Research | `05_PLAYER_RESEARCH/` | подтверждённый доступ игрока | главный источник цепочки PLAYER → TOOL → RESULT |
| Encyclopedia Research | `03_ENCYCLOPEDIA_RESEARCH/` | зеркало проходов A–D | ARCHIVE; не читать как канон |
| Legacy Encyclopedia | `02_ENCYCLOPEDIA_LEGACY/` | ART/MEC/OBJ/QUE | ARCHIVE; unique depth уже частично в `04` |
| Game analysis dumps | `09_GAME_ANALYSIS` (если есть) | сырьё | не канон |

## Дерево `04_UNIFIED_ENCYCLOPEDIA` (65 `.md`)

Организация — **по внутренним системам кода**, не по намерению игрока.

| Папка | Назначение | Кол-во статей |
|---|---|---|
| `00_NAVIGATION/` | вход, статусы, карта, методология | 4 |
| `01_CORE_ARCHITECTURE/` | карта Assembly-CSharp, Config, связи | 4 |
| `02_WORLD_AND_EVENTS/` | Laws, Ages, Powers, Disasters | 5 |
| `03_ACTORS/` | Actor, AI, Jobs, экономика, бой, traits, magic | ~20 |
| `04_CITIES_AND_ECONOMY/` | Buildings, Production, Supply, city life | 6 |
| `05_CIVILIZATIONS/` | Plots, пространство, governance, War overview, Expeditions | 10 |
| `07_GENETICS_AND_TRAITS/` | только sapience | 2 |
| `09_NAMES_AND_ONOMASTICS/` | имена | 6 |
| `10_REGISTRIES_AND_INDEXES/` | ID, OBJ-паспорта | 4+ |
| `11_OPEN_RESEARCH/` | VQ/RQ | 3 |
| `99_ARCHIVE_REFERENCES/` | куда смотреть в `02_`/`03_` | 1 |

Номера `06` и `08` в дереве `04` намеренно пустые (kingdoms живут в `05_`, законы в `02_`).

## Модель статей `04`

Типичная статья:

1. Status (CLOSED / PARTIALLY / NOT_CLOSED / …)
2. Классы, поля, методы
3. Подтверждённые факты симуляции
4. Связи с другими системами
5. Чего нет / открытые хвосты

**Нет обязательных блоков:** WHAT PLAYER CAN DO / WHERE TO FIND IT / WHAT HAPPENS AFTER THE ACTION / WHAT AI DECIDES / LIMITATIONS / LONG-TERM EFFECTS.

Исключение: `god-powers-drops-terraform.md` уже содержит короткий UI-вход (`PlayerControl.clickedFinal`), но это архитектура сил, не путеводитель игрока.

## Как энциклопедия сама себя описывает (важно)

Из `04` README / `system-status.md` / `knowledge-map.md` (на момент аудита):

- **CLOSED:** Plots, Decisions, Jobs, Resources, Buildings, Items, Production, Supply, Zones, Borders, Territory, Expansion, World Laws (исполнение), Ages, Powers/Disasters architecture, Actor core, Traits, Status, Magic.
- **NEGATIVE_CANON:** Expeditions (системы нет).
- **PARTIALLY_RESEARCHED:** combat, governance, Kingdom archive, City life, Social, economic behavior, architecture map.
- **NOT_CLOSED:** War, Diplomacy, Army, Culture, Language, Religion, Clan, biomes, UI, player, modding, standalone Boats/Docks.
- **MAP_ONLY:** UI / Player / Modding; Biomes.

Это **устарело относительно `05_PLAYER_RESEARCH`**. Исследование игрока уже закрыло доступ и симуляцию по большинству этих «NOT_CLOSED / MAP_ONLY» доменов. В `04` это **не отражено**.

---

# EXISTING KNOWLEDGE AREAS

## A. Канон симуляции в `04` (есть статьи)

| Область | Главные статьи | Статус в `04` | Пригодно для игрока? |
|---|---|---|---|
| Архитектура кода | `architecture-map.md`, `build-and-config.md`, `system-connections.md` | PARTIAL | нет как вход; да как якоря классов |
| World Laws | `world-laws.md` | CLOSED (execution) | частично: законы есть, нет «какой закон нажать чтобы…» |
| World Ages | `world-ages.md` | CLOSED | частично |
| God Powers / Drops / Terraform | `god-powers-drops-terraform.md` | CLOSED architecture | сильный симуляционный канон; слабый player intent |
| Disasters / fire / heat | `disasters-world-behaviours-environment.md` | CLOSED architecture | SIM_ONLY |
| Actor architecture / lifecycle / catalog | `architecture.md`, `lifecycle.md`, `catalog.md`, `classification.md` | CLOSED | SIM_ONLY |
| Actor AI / Decisions | `actor-ai-decisions.md`, `actor-ai-and-mind.md` | CLOSED | симуляция pipeline; нет Possession / границ игрока |
| Jobs | `actor-jobs.md` | CLOSED | CitizenJob как биржа; нет «игрок не назначает работу» как главный ответ |
| Resources / Items | `actor-economic-resources.md`, `actor-items-equipment.md` | CLOSED | факты склада/предметов есть |
| Buildings / Production / Supply | `buildings.md`, `production.md`, `supply.md` | CLOSED | SIM_ONLY + один якорь топора |
| City life | `city-and-civilization-life.md` + legacy depth | PARTIAL | обзор, не player chain |
| Zones / Borders / Territory / Expansion | 4 статьи в `05_CIVILIZATIONS` | CLOSED | пространство мира, не «как захватить город» |
| Plots | `plots.md` | CLOSED | сильный канон 28 id; обряды/rites игрока — в `05` |
| Governance | `city-kingdom-governance.md` | PARTIAL | City/Kingdom AI jobs; нет succession/loyalty player |
| Kingdoms | `kingdoms-and-civilization.md` | PARTIAL | два пула Kingdom |
| War / Diplomacy | `war-diplomacy.md` | **NOT_CLOSED** (обзор) | устаревший статус; факты частично верны |
| Combat | `actor-combat-warfare.md` | PARTIAL | Actor fight; Army/capture не закрыты в `04` |
| Traits / Status / Magic | 3 статьи в `03_ACTORS` | CLOSED | симуляция; нет Trait Editor / player apply |
| Sapience | `subspecies-sapience.md` | CLOSED tags | не полный genetics/birth |
| Social | `actor-social-brain.md` + legacy | PARTIAL | якоря love/family; не Clan/Culture/Religion |
| Onomastics | `09_NAMES_AND_ONOMASTICS/` | LEGACY_UNIQUE | не приоритет игрока |
| Expeditions | `expeditions.md` | NEGATIVE_CANON | сохранить: системы нет |
| Open questions | `11_OPEN_RESEARCH/` | ACTIVE VQ/RQ | **устарел:** VQ-01/03 и Culture/UI помечены открытыми |

## B. Исследования игрока в `05` (есть документы, нет статей энциклопедии)

30 markdown-файлов. Из них **27** — предметные исследования; **3** — карта источников / трасса действий / prefab completion.

### Приоритетные для первой рабочей версии

| Документ | Область |
|---|---|
| `PLAYER_INTERFACE_ACCESS_MAP.md` | вкладки, окна, кнопки, ваниль vs моды |
| `PLAYER_ACTION_TRACE.md` | клик → PowerButton → симуляция |
| `PLAYER_PREFAB_EVENT_COMPLETION.md` | события prefab окон |
| `GOD_POWERS_TRAIT_ACCESS.md` | силы, trait access |
| `TRAIT_EDITOR_SIMULATION_EFFECTS.md` | редактор черт |
| `TRAIT_CALLBACK_DIRECT_EFFECTS.md` | прямые эффекты trait callbacks |
| `NPC_CORE_STATE_AND_AI_ARCHITECTURE.md` | Actor+Data, updateStats, Decision→Job→Task, Possession |
| `DEBUG_AND_DEVELOPER_TOOLS.md` | GraphyCaller, debug windows, console |
| `SPECIES_SUBSPECIES_BIRTH_GENETICS_PLAYER_ACCESS.md` | вид / подвид / рождение / генетика |
| `SUBSPECIES_LIVE_VALIDATION_AND_POPULATION_CONTROL.md` | контроль популяции подвида |

### Цивилизации / политика / конфликт

| Документ | Область |
|---|---|
| `PLOTS_RITES_PLAYER_ACCESS.md` | Plots + Rites с точки зрения игрока |
| `KINGDOM_SUCCESSION_ROYAL_CLAN_PLAYER_ACCESS.md` | престолонаследие |
| `CITY_LEADERSHIP_LOYALTY_REBELLION_PLAYER_ACCESS.md` | лидер, лояльность, мятеж |
| `WARS_PLAYER_ACCESS_AND_SIMULATION.md` | война |
| `DIPLOMACY_PLAYER_ACCESS_AND_SIMULATION.md` | дипломатия |
| `POLITICAL_CONTROL_AND_ALLIANCE_CONSEQUENCES.md` | Unity / Discord / альянсы |
| `CITY_CAPTURE_AND_TERRITORIAL_CONTROL.md` | захват города |
| `ARMIES_MILITARY_MOBILIZATION_AND_CITY_ATTACK.md` | армии |
| `UNIT_COMBAT_TARGETING_AND_BATTLE_CONSEQUENCES.md` | бой юнита |
| `WATCH_TOWERS_AND_DEFENSIVE_BUILDINGS.md` | башни / стены |
| `CITIZEN_JOBS_AND_CITY_ECONOMY.md` | работы и склад |

### Популяция и мета-системы

| Документ | Область |
|---|---|
| `REPRODUCTION_AND_POPULATION_GROWTH_PLAYER_ACCESS.md` | размножение / рост |
| `MORTALITY_SURVIVAL_AND_POPULATION_BALANCE.md` | смертность |
| `CULTURE_PLAYER_ACCESS_AND_SIMULATION.md` | культура |
| `LANGUAGE_PLAYER_ACCESS_AND_SIMULATION.md` | язык |
| `RELIGION_PLAYER_ACCESS_AND_SIMULATION.md` | религия |
| `BOOKS_META_SYSTEM_TRANSMISSION.md` | книги |
| `CLAN_BLOODLINE_PLAYER_ACCESS_AND_SIMULATION.md` | клан |
| `FAMILY_PLAYER_ACCESS_AND_SIMULATION.md` | семья |

### Служебные

| Документ | Область |
|---|---|
| `PLAYER_RESEARCH_SOURCE_MAP.md` | где лежат исходники; **не** энциклопедия |

Сырьё извлечения UI: `05_PLAYER_RESEARCH/_extract/` (JSON/Python). Не канон.

## C. Архив (не интегрировать слепо)

- `02_ENCYCLOPEDIA_LEGACY` — ~162 md; ART/MEC/OBJ. Unique depth уже перенесён в `04` (ономастика, city/social depth, OBJ-0015). Combat/War overlay помечен VERIFY.
- `03_ENCYCLOPEDIA_RESEARCH` — ~43 md; исходники проходов, почти все уже скопированы в `04`.

---

# RESEARCH NOT YET INTEGRATED

**Ни один документ `05_PLAYER_RESEARCH` не влит в `04_UNIFIED_ENCYCLOPEDIA`.**  
`04` не ссылается на `05`. `knowledge-map.md` прямо говорит: статей-канона по Culture / Language / Religion / Clan / UI / player **нет**.

Это главный разрыв корпуса.

| Исследование `05` | Есть ли статья `04` на ту же тему | Интеграция |
|---|---|---|
| Interface / Action Trace / Prefabs | нет (UI = MAP_ONLY) | **0%** |
| Debug / Developer Tools | нет | **0%** |
| NPC Core State / AI Architecture | `actor-ai-decisions.md` (pipeline) | **~20%** — AI есть как симуляция, нет Possession, updateStats-слоёв, границы игрока |
| God Powers trait access | `god-powers-drops-terraform.md` | **~40%** — архитектура есть; player trait/spawn/mass tools — нет |
| Trait Editor / Callbacks | `actor-traits-modifiers-subspecies.md` | **~30%** — traits как данные; редактор и callbacks игрока — нет |
| Species / Subspecies / Genetics / Birth | `subspecies-sapience.md` + traits | **~15%** |
| Reproduction / Mortality / Population | `lifecycle.md`, status | **~15%** |
| Plots / Rites player | `plots.md` | **~50%** — runtime Plot закрыт; player rites/access — нет |
| Culture / Language / Religion / Books | нет канона | **0%** |
| Clan / Family | social brain якоря | **~10%** |
| Succession / Leadership / Loyalty / Rebellion | governance PARTIAL | **~15%** |
| Wars / Diplomacy / Alliances | `war-diplomacy.md` NOT_CLOSED | **~25%** — обзор есть; player chain и уточнения `05` — нет |
| City Capture | territory/expansion CLOSED, capture нет | **0%** как отдельная механика игрока |
| Armies | NOT_CLOSED, VQ-03 | **~10%** якоря |
| Unit Combat targeting | combat PARTIAL | **~30%** |
| Watch Towers / walls | buildings CLOSED | **~20%** — здания есть; player cannot place civ tower / wall tiles — нет |
| Citizen Jobs / City Economy player | jobs+production CLOSED | **~40%** — биржа есть; «игрок не назначает», axe vs pickaxe, `dust_gold`, `hasEnoughFoodForArmy` — нет |

**Итог:** симуляционный канон закрыт по многим внутренним системам; **рабочая энциклопедия игрока отсутствует.** Знания игрока лежат рядом и не подключены.

---

# OUTDATED OR CONTRADICTORY INFORMATION

Не «ошибки кода `05` против кода», а **навигация и статусы `04` против уже подтверждённого исследования**.

## 1. Статусы систем (критично)

`system-status.md`, `README.md`, `knowledge-map.md`, `open-questions.md` утверждают:

- UI / Player = **MAP_ONLY**
- War / Diplomacy / Army = **NOT_CLOSED**
- Culture / Language / Religion / Clan = **NOT_CLOSED**, «нет статьи-канона»
- VQ-01 DiplomacyHelpers, VQ-03 Army full model — ACTIVE

`05` уже содержит закрывающие (для доступа игрока и симуляционного ответа) документы по всем этим областям. Пока статусы не обновлены, **энциклопедия врёт читателю о пробелах**.

Это не значит, что каждая внутренняя формула VQ закрыта (VQ-02 `clash`, VQ-04 CursedSacrifice, VQ-06 stats formulas остаются). Значит: помечая целые системы NOT_CLOSED, `04` скрывает готовые ответы игрока.

## 2. `dust_gold`

`god-powers-drops-terraform.md` перечисляет `dust_gold` в одном ряду с красками/пылью (`paint`, `dust_white`, …).

`CITIZEN_JOBS_AND_CITY_ECONOMY.md`: `dust_gold` = забыть kingdom/city, **не** выдача золота.

**Конфликт интерпретации для игрока.** Архитектурный список Drop id не ложен; отсутствующий эффект вводит в заблуждение.

## 3. Army / food

`04` / VQ-03: «порог 0.7 send, follow leader» — согласуется с `05`.  
`05` дополнительно: `hasEnoughFoodForArmy()` всегда `true`; 1 Army на город; нет ванильных команд армии.

Энциклопедия не противоречит прямо, но **неполна** и помечена NOT_CLOSED, как будто модели нет.

## 4. Religion stats

`NPC_CORE_STATE_AND_AI_ARCHITECTURE.md`: religion `base_stats` **не мержатся** в `updateStats`; религия может добавлять decisions.

`04` traits/connections этого слоя не канонизируют. Риск: статья про «всё meta даёт статы» будет неверной.

## 5. Friendship / мир

`war-diplomacy.md`: Friendship power → leaveWar / Peace.

`05` дипломатия: нет ванильного «выбрать две стороны и заключить мир» как парного инструмента (в отличие от Whisper A+B). Friendship — drop на цель, не pair-picker.

Не обязательно ложь; **разные уровни описания**. Для игрока нужна формулировка `05`.

## 6. Watch towers vs walls

`buildings.md` описывает здания.  
`05`: цивилизационная watch tower строится городом; игрок **не** ставит `watch_tower_*`; Flame/ice/angle towers — God Power drops, не городская оборона; `wall_*` — terraform-тайлы игрока, не city wall building.

Без этой границы статья Buildings отвечает «есть башни», но не «игрок не может поставить городскую башню».

## 7. Jobs CLOSED vs player control

`actor-jobs.md` CLOSED как биржа CitizenJob.  
`05`: игрок **не назначает** citizen job; CitizenJob ≠ UnitProfession; без stockpile собиратели не открывают работу.

Статус CLOSED корректен для симуляции и **опасен** как ответ «как назначить работу жителю».

## 8. Combat targeting

`actor-combat-warfare.md` PARTIAL.  
`05`: `Actor.attack_target` ≠ `City.target_attack_city`; `peaceful` пропускает поиск, `pacifist` — нет; нет ванильного «приказ атаковать».

Частичное описание в `04` не должно оставаться единственным входом.

## 9. Open questions, которые уже не блокируют игрока

| ID в `04` | Почему устарел как «система не исследована» |
|---|---|
| VQ-01 DiplomacyHelpers | `05` закрыл player start-war / isEnemy ⇔ War |
| VQ-03 Army full model | `05` закрыл 1 army/city, march, target city, нет команд |
| RQ-06 UI/player/modding как MAP_ONLY | interface map + debug + mods отделены |
| Culture/Language/Religion/Clan без ID | отдельные документы `05` |
| CQ-05 baby vs newCreature | покрыто species/birth `05` на уровне доступа игрока |

Оставить открытыми (не закрывать статусом из `05`): VQ-02 clash, VQ-04 law readers, VQ-06 формулы статов, VQ-07 ономастика, RQ-03 полный ID biomes, Boats/Docks standalone, LIVE-проверки.

## 10. Путь декомпила

`04` часто пишет runtime truth: `E:\worldboxAssembly-CSharp`.  
Фактический workspace: `E:\worldboxGAME\worldboxAssembly-CSharp`.  
Это навигационная устарелость, не механика.

---

# DUPLICATES

Дубликаты здесь — **параллельные корпуса**, не две одинаковые статьи в `04`.

## Внутри `04` (умеренно)

| Пара | Оценка |
|---|---|
| `actor-ai-decisions.md` ↔ `actor-ai-and-mind.md` | намеренный split (канон + supporting) |
| `actor-social-brain.md` ↔ `actor-social-legacy-depth.md` | канон + Legacy depth |
| `city-and-civilization-life.md` ↔ `city-life-legacy-depth.md` | то же |
| `03` Research ↔ `04` Unified | исторический дубль; `03` = ARCHIVE |
| `02` ART ↔ `04` статьи | ARCHIVE; не повседневность |
| `world-laws` указатель в `03/world/` | архивный дубль |

**Не плодить третий слой** тех же SIM-статей при сборке рабочей энциклопедии.

## Между `04` и `05` (главный риск сборки)

Если просто скопировать `05` в `04` без слияния, появятся двойные каноны:

| Тема | `04` | `05` | Правило сборки |
|---|---|---|---|
| AI | actor-ai-decisions | NPC_CORE | обновить `04` AI + новая player-статья NPC |
| Jobs | actor-jobs | CITIZEN_JOBS | обновить jobs player-блоками; не вторая jobs-статья симуляции |
| Combat | actor-combat-warfare | UNIT_COMBAT | обновить combat; army/capture — отдельные player-статьи |
| Powers | god-powers-drops | GOD_POWERS_TRAIT_ACCESS | обновить powers player-входом; не дублировать каталог Drop |
| Traits | actor-traits | TRAIT_EDITOR + CALLBACKS | обновить traits + player editor статья |
| Plots | plots.md | PLOTS_RITES | обновить plots player-доступом |
| War | war-diplomacy.md | WARS + DIPLOMACY + ALLIANCES | **разделить** player-статьи; `war-diplomacy.md` повысить из NOT_CLOSED или заменить ссылками |
| Buildings | buildings.md | WATCH_TOWERS | доп. секция / отдельная player defense |
| Social | social-brain | FAMILY + CLAN | новые meta-статьи, social-brain оставить якорем love/talk |
| Governance | city-kingdom-governance | SUCCESSION + LEADERSHIP | не дублировать CityBeh list; добавить player succession/loyalty |

## Внутри `05`

Предметного дубля почти нет. Пересечения намеренные:

- Interface map ↔ Action trace ↔ Prefab completion (разные слои одного UI)
- GOD_POWERS ↔ TRAIT_EDITOR (разные входы на traits)
- WARS ↔ DIPLOMACY ↔ ALLIANCES ↔ CAPTURE ↔ ARMIES ↔ COMBAT (конвейер конфликта)

---

# MISSING CONNECTIONS BETWEEN ARTICLES

1. **`04` не знает о `05`.** Ни knowledge-map, ни system-status не ведут к player research.
2. **Нет цепочки PLAYER INTENT.** Нет маршрута «хочу начать войну» → Whisper → isEnemy → army march → capture.
3. **Powers не связаны с Trait Editor, Debug, Possession.**
4. **Jobs не связаны с «игрок не назначает» и stockpile-гейтом.**
5. **Plots CLOSED не связан с player rites и с тем, что Spite/Whisper минуют Plot** (в `plots.md` это есть; в player-навигации нет).
6. **Territory/Expansion CLOSED не связаны с capture ticks / watch tower +10.**
7. **Religion/Culture/Language отсутствуют**, поэтому Actor.connections обрывается на «NOT_CLOSED».
8. **Debug отсутствует**, поэтому Mind tab / Actor AI tooltip не объяснены как ванильный inspect vs debug unlock.
9. **Моды.** `04` почти не отделяет PowerBox (army create, convert city, EditResources). `05` отделяет. Энциклопедия игрока без этого будет смешивать ваниль и моды этой копии.
10. **Эксперименты игрока.** Раздела «Как создать / Можно ли / Почему NPC не делает» нет ни в `04`, ни как индекс в `05`.

---

# CRITICAL KNOWLEDGE GAPS

Пробелы **для рабочей энциклопедии**, не приглашение к новому исследованию кода.

## Блокируют первую рабочую версию, если не интегрировать уже найденное

Это не «нет знаний» — это «знания не в энциклопедии»:

1. Интерфейс и границы прямого контроля
2. God Powers / Drops / spawn / mass tools как действия игрока
3. NPC: статы, traits, AI, Possession
4. Debug Menu vs Internal vs Mods
5. Species / Subspecies / genetics / birth
6. «Что игрок не может» (назначить короля, работу, цель армии, поставить city watch tower, парный мир)

## Реальные пробелы знания (не закрывать новым исследованием сейчас)

Зафиксированы в `OPEN_RESEARCH_GAPS.md`. Кратко:

| Пробел | Блокирует |
|---|---|
| LIVE-прогон UI (11 кликов GraphyCaller, точный layout debug window) | формулировки REQUIRES_LIVE_VALIDATION в статьях Debug / Interface |
| Полный каталог Decision id как справочник игрока | «почему NPC выбрал X» на уровне имени решения |
| Housing / happiness / food consumption как отдельный player-контур | сценарии «почему город не растёт» сверх reproduction/mortality |
| Boats / Docks standalone | морские сценарии |
| Biomes player access | «как сменить биом / что даёт биом юниту» полно |
| Формулы VQ-06 (mass/stamina/XP) | точные числа в статье характеристик |
| Onomastics algorithm VQ-07 | «как игра выбирает имя» |
| War type `clash` (не init) | ничего для игрока; INTERNAL curiosity |

**Не пробел:** отсутствие Expeditions (NEGATIVE_CANON).  
**Не пробел:** «нет исследования War» — исследование есть в `05`.

## Чего энциклопедия не умеет сейчас как продукт

- Ответить «что реально может сделать игрок» первым абзацем
- Отделить VANILLA / DEBUG / INTERNAL / MOD_ONLY на каждой карточке
- Дать цепочку PLAYER → INTERFACE → ACTION → TARGET → SYSTEM → RESPONSE → RESULT
- Провести практический сценарий без чтения 3–6 технических файлов

---

# PROPOSED WORKING STRUCTURE

Полная архитектура: `PROPOSED_ENCYCLOPEDIA_ARCHITECTURE.md`.

Кратко:

Рабочая энциклопедия игрока **не заменяет** симуляционный канон `04` в C1.  
В C2 она собирается как **player-first слой** с девятью разделами:

1. PLAYER INTERFACE AND CONTROL  
2. PLAYER POWERS AND TOOLS  
3. NPC  
4. SPECIES AND POPULATION  
5. CIVILIZATIONS  
6. META SYSTEMS  
7. POLITICS AND CONFLICT  
8. WORLD SIMULATION  
9. PLAYER EXPERIMENTS  

Правило факта в статьях: **CONFIRMED** или **REQUIRES_LIVE_VALIDATION**.  
**MOD_ONLY** и **INTERNAL** отделяются от ванили.

Карта источников: `RESEARCH_TO_ENCYCLOPEDIA_MAP.md`.  
Пробелы, которые нельзя закрывать новым исследованием автоматически: `OPEN_RESEARCH_GAPS.md`.
