# PROPOSED ENCYCLOPEDIA ARCHITECTURE

**Фаза:** C1  
**Дата:** 2026-09-08  
**Статус:** предложение. Сборка статей — фаза C2, не этот документ.

---

# ЗАЧЕМ НОВАЯ АРХИТЕКТУРА

Текущий `04_UNIFIED_ENCYCLOPEDIA` отвечает на вопрос:

> Как устроена система в коде?

Рабочая энциклопедия должна отвечать на вопрос:

> Что игрок может сделать, где это найти, что изменится, как ответит симуляция, какие ограничения и долгосрочные следствия?

Это **другой вход**, не отмена симуляционного канона.

---

# ГЛАВНАЯ МОДЕЛЬ ЗНАНИЙ

Каждая важная статья по возможности держит цепочку:

```
PLAYER INTENT
  → INTERFACE / TOOL
  → GAME ACTION
  → TARGET
  → INTERNAL SYSTEM
  → SIMULATION RESPONSE
  → RESULT
```

Обязательные блоки (для механик с участием игрока):

1. **WHAT PLAYER CAN DO**
2. **WHERE TO FIND IT**
3. **WHAT HAPPENS AFTER THE ACTION**
4. **WHAT AI / SIMULATION DECIDES**
5. **LIMITATIONS**
6. **LONG-TERM EFFECTS**
7. **RELATED SYSTEMS**

Метка каждого факта:

- **CONFIRMED** — код / уже закрытое исследование
- **REQUIRES_LIVE_VALIDATION** — код есть, живой прогон не делался

Отдельные ярлыки, не смешивать с ванилью:

- **MOD_ONLY** — PowerBox / NML / ModernBox / RulerBox / TPI и т.п.
- **INTERNAL** — есть в коде, нет ванильного игрового входа
- **DEBUG** — встроенное debug-меню после unlock, не мод и не обычный HUD
- **NEGATIVE_CANON** — системы нет (пример: Expeditions)

---

# ГДЕ БУДЕТ ЖИТЬ РАБОЧАЯ ЭНЦИКЛОПЕДИЯ

## Решение (предложение C2)

Не ломать `04` переездом папок в первый же день сборки.

| Слой | Путь | Роль |
|---|---|---|
| **Рабочая энциклопедия игрока (v1)** | `WorldBox Research/06_ENCYCLOPEDIA_BUILD/WORKING/` | повседневный вход для вопросов игрока |
| **Симуляционный канон** | `04_UNIFIED_ENCYCLOPEDIA/` | классы, пайплайны, CLOSED architecture |
| **Исследования игрока** | `05_PLAYER_RESEARCH/` | первоисточник доступа; после интеграции — ссылочный архив |
| **Аудит / план** | `06_ENCYCLOPEDIA_BUILD/*.md` (этот набор) | C1 артефакты |

Когда v1 стабилизируется, рабочее дерево можно повысить в `07_WORKING_ENCYCLOPEDIA/` или сделать главным входом `04`. **Сейчас не переименовывать `04`.**

Навигация `04` в C2 должна начать указывать: «вопрос игрока → WORKING; устройство кода → эта папка».

---

# ДЕРЕВО WORKING (v1)

```
06_ENCYCLOPEDIA_BUILD/WORKING/
  README.md                          ← вход игрока
  00_HOW_TO_USE.md
  01_PLAYER_INTERFACE_AND_CONTROL/
  02_PLAYER_POWERS_AND_TOOLS/
  03_NPC/
  04_SPECIES_AND_POPULATION/
  05_CIVILIZATIONS/
  06_META_SYSTEMS/
  07_POLITICS_AND_CONFLICT/
  08_WORLD_SIMULATION/
  09_PLAYER_EXPERIMENTS/
```

Имена файлов — латиница, стабильные якоря. Текст статей — русский, в плотности фаз 22–27.

---

# РАЗДЕЛ 1. PLAYER INTERFACE AND CONTROL

**Приоритет v1: высокий.**

| Статья | Вопрос игрока | Источник |
|---|---|---|
| `vanilla-vs-debug-vs-mods.md` | Это ваниль, debug или мод? | Interface map, Debug |
| `hud-tabs-and-power-buttons.md` | Где вкладки и кнопки сил? | Interface map |
| `windows-and-inspect.md` | Какие окна открываются кликом по миру/юниту? | Interface, prefabs, NPC inspect |
| `selecting-objects.md` | Как выбрать юнита, город, королевство, мета-объект? | Interface, Action trace |
| `editors.md` | Какие редакторы есть в ванили (traits, subspecies, …)? | Trait editor, Species |
| `debug-menu.md` | Как открыть debug, что там есть, что не сохраняется? | DEBUG |
| `limits-of-direct-control.md` | Чего игрок не приказывает напрямую? | NPC_CORE, Armies, Jobs, Succession |

Не тащить сюда полный dump каждого locale JSON.

---

# РАЗДЕЛ 2. PLAYER POWERS AND TOOLS

**Приоритет v1: высокий.**

| Статья | Вопрос игрока | Источник |
|---|---|---|
| `how-powers-work.md` | Что происходит после клика по силе? | Action trace, powers `04`+`05` |
| `god-powers.md` | Какие силы меняют мир / NPC? | GOD_POWERS, powers `04` |
| `drops.md` | Чем drop отличается от кисти и от spawn? | powers `04`+`05` |
| `spawn-and-mass-tools.md` | Как создать существ / здания / эффекты массово? | GOD_POWERS, interface |
| `terraform-and-brushes.md` | Кисти земли, стены-тайлы, биом-семена | powers, watch towers (walls) |
| `diplomacy-powers.md` | Whisper, Spite, Inspiration, Unity, Discord, Friendship | Wars, Diplomacy, Alliances |
| `trait-and-status-powers.md` | Силы, которые вешают trait/status | GOD_POWERS, traits |
| `powerbox-and-other-mods.md` | Что в этой копии не ваниль | все `05` MOD_ONLY |

Обязательно уточнить `dust_gold`: не золото королевства.

---

# РАЗДЕЛ 3. NPC

**Приоритет v1: высокий.**

| Статья | Вопрос игрока | Источник |
|---|---|---|
| `what-is-an-npc.md` | Actor vs ActorData, городской житель vs существо | NPC_CORE, architecture |
| `stats-and-abilities.md` | Откуда берутся характеристики | NPC_CORE updateStats |
| `traits.md` | Что делают черты, как игрок их ставит | traits `04`, editor, callbacks |
| `statuses.md` | Временные состояния | status `04` |
| `ai-decisions-jobs-tasks.md` | Почему NPC «сам» что-то делает | AI `04`, NPC_CORE |
| `possession.md` | Что даёт одержимость, что отключает | NPC_CORE |
| `inspect-and-mind-tab.md` | Что видно в карточке юнита / last decision | Interface, Debug, NPC_CORE |

Граница контроля — сквозная: игрок меняет условия и тело NPC, симуляция выбирает Decision/Job/Task, кроме Possession.

---

# РАЗДЕЛ 4. SPECIES AND POPULATION

**Приоритет v1: высокий (species/subspecies); остальное — интегрировать, не тормозить.**

| Статья | Вопрос игрока | Источник |
|---|---|---|
| `species.md` | Что такое вид | SPECIES `05`, catalog `04` |
| `subspecies.md` | Что такое подвид, что редактируется | SPECIES, SUBSPECIES |
| `genetics.md` | Гены на подвиде, не личный геном | SPECIES, NPC_CORE |
| `birth-traits.md` | Черты при рождении | SPECIES |
| `reproduction.md` | Как появляются дети | REPRODUCTION |
| `inheritance-and-evolution.md` | Что наследуется / как вид «плывёт» | SPECIES, REPRODUCTION |
| `population-growth.md` | Почему население растёт или нет | REPRODUCTION, JOBS |
| `mortality.md` | Как умирают | MORTALITY, status |

---

# РАЗДЕЛ 5. CIVILIZATIONS

**Приоритет v1: средний, не блокировать раздел 1–3.**

| Статья | Вопрос игрока | Источник |
|---|---|---|
| `cities.md` | Что такое город | city life, zones |
| `citizen-jobs.md` | Работы жителей; игрок не назначает | CITIZEN_JOBS, actor-jobs |
| `city-economy.md` | Склад, еда, топор/кирка, рецепты | CITIZEN_JOBS, production, supply |
| `buildings.md` | Что строит город vs что ставит игрок | buildings, watch towers |
| `kingdoms.md` | Королевство | kingdoms `04`, succession `05` |
| `kings-and-leaders.md` | Король и лидер города | SUCCESSION, LEADERSHIP |
| `succession.md` | Кто станет следующим королём | SUCCESSION |
| `loyalty.md` | Откуда лояльность | LEADERSHIP |

Rebellion — карточка здесь (ссылка) и полная статья в разделе 7.

---

# РАЗДЕЛ 6. META SYSTEMS

**Приоритет v1: средний.**

| Статья | Вопрос игрока | Источник |
|---|---|---|
| `culture.md` | Культура: доступ игрока и эффект | CULTURE `05` |
| `language.md` | Язык | LANGUAGE |
| `religion.md` | Религия; статы не мержатся | RELIGION, NPC_CORE |
| `books.md` | Книги как передача мета | BOOKS |
| `clan.md` | Клан / кровь / королевский клан | CLAN, SUCCESSION |
| `family.md` | Семья | FAMILY, social-brain |
| `plots-and-rites.md` | Заговоры и обряды NPC vs силы игрока | plots `04`, PLOTS_RITES `05` |

---

# РАЗДЕЛ 7. POLITICS AND CONFLICT

**Приоритет v1: средний; войны/армии уже исследованы — интегрировать без нового кода.**

| Статья | Вопрос игрока | Источник |
|---|---|---|
| `diplomacy.md` | Отношения, opinion, что может игрок | DIPLOMACY |
| `alliances.md` | Unity Forced, Discord leave | ALLIANCES |
| `wars.md` | Как начать войну; isEnemy ⇔ War | WARS |
| `rebellions.md` | Мятеж | LEADERSHIP |
| `armies.md` | 1 армия/город, марш, нет команд | ARMIES |
| `unit-combat.md` | Кого бьёт юнит; не приказ игрока | UNIT_COMBAT |
| `city-capture.md` | Тики до 100, кто получает город | CAPTURE |
| `defense.md` | Башни +10, стены-тайлы, drops-башни | WATCH_TOWERS |

Сквозной факт: захват ∥ бой; получатель захвата может быть **основная** сторона войны, не штурмующая армия.

---

# РАЗДЕЛ 8. WORLD SIMULATION

**Приоритет v1: низкий-средний, якоря уже в `04`.**

| Статья | Вопрос игрока | Источник |
|---|---|---|
| `world-laws.md` | Какие законы переключить и что это меняет | world-laws `04` |
| `world-ages.md` | Эры | world-ages `04` |
| `disasters-environment.md` | Катастрофы / огонь / тепло | disasters `04` |
| `global-ai.md` | City/Kingdom AI vs Actor AI | governance, NPC_CORE |
| `population-balance.md` | Длинный контур роста/смерти | population `05` |
| `long-term-consequences.md` | Что остаётся после войны/захвата/пыли | conflict + meta `05` |
| `expeditions.md` | Есть ли экспедиции? **Нет.** | NEGATIVE_CANON |

Biomes и Boats — не раздувать v1; см. gaps.

---

# РАЗДЕЛ 9. PLAYER EXPERIMENTS

**Приоритет v1: высокий как индекс**, низкий как объём новых фактов.

Формат карточки:

```
INTENT
→ TOOL / WHERE
→ STEPS (ваниль)
→ RESULT (CONFIRMED / REQUIRES_LIVE)
→ AI RESPONSE
→ LIMITATIONS
→ RELATED
```

Стартовый набор — из карты `RESEARCH_TO_ENCYCLOPEDIA_MAP.md` §9.  
Не писать сценарий, если цепочка не подтверждена.

---

# ПРИОРИТЕТ СБОРКИ v1

Делать в этом порядке. Не ждать полного покрытия разделов 5–8.

| Порядок | Раздел | Минимальный набор статей |
|---|---|---|
| 1 | Interface | vanilla/debug/mods, HUD, windows, debug, limits |
| 2 | Powers | how-powers-work, god-powers, drops, diplomacy-powers, trait powers |
| 3 | NPC | what-is-npc, stats, traits, AI, possession |
| 4 | Species | species, subspecies, genetics, birth-traits |
| 5 | Experiments | 8–12 карточек по уже закрытым ограничениям |
| 6 | Conflict | wars, armies, combat, capture, defense |
| 7 | Civilizations | jobs, economy, succession, leaders, loyalty |
| 8 | Meta | culture, language, religion, clan, family, plots |
| 9 | World | laws, ages, expeditions-negative |

---

# ЧЕГО НЕ ДЕЛАТЬ В АРХИТЕКТУРЕ

- Не создавать третью копию CLOSED симуляции из `04`.
- Не делать одну гигантскую статью «War+Diplomacy+Army+Capture».
- Не включать мод-кнопки в ванильные списки инструментов.
- Не объявлять LIVE_CONFIRMED без прогона.
- Не начинать исследование неизвестных классов, чтобы «дозаполнить» раздел.
- Не удалять `04` и `05` в C2.

---

# СВЯЗЬ С `04` ПОСЛЕ v1

Каждая WORKING-статья внизу:

```
SIMULATION CANON: ссылка на 04
PLAYER RESEARCH: ссылка на 05
```

`04/00_NAVIGATION` получает один абзац: вопросы игрока решаются в WORKING.

Это достаточно, чтобы C2 начала сборку без нового исследования игры.
