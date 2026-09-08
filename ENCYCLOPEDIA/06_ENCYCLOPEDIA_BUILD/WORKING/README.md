# WorldBox Working Encyclopedia v1

**Назначение:** отвечать, что игрок **реально может и не может** сделать, где это в интерфейсе, что вызовется в симуляции и как ответит AI.

Это не замена симуляционного канона. Это рабочий слой для вопросов игрока.

| Слой | Путь | Когда читать |
|---|---|---|
| **Эта энциклопедия** | `06_ENCYCLOPEDIA_BUILD/WORKING/` | «можно ли / где кнопка / что будет» |
| Симуляция | `04_UNIFIED_ENCYCLOPEDIA/` | классы, пайплайны, CLOSED architecture |
| Исследования игрока | `05_PLAYER_RESEARCH/` | первоисточник фактов доступа |
| План сборки | `06_ENCYCLOPEDIA_BUILD/` | аудит C1, не статьи игрока |

**Сборка:** 2026-09-08, фаза C2. LIVE-прогон игры не выполнялся: где код есть, а клик в билде не смотрели — **REQUIRES LIVE VALIDATION**.

---

## С чего начать

1. [Как пользоваться](00_HOW_TO_USE.md) — уровни доступа и метки фактов
2. Вопрос игрока → раздел ниже
3. Карточка эксперимента, если вопрос вида «можно ли…» → [10_PLAYER_EXPERIMENTS](10_PLAYER_EXPERIMENTS/README.md)

---

## Разделы

| # | Раздел | Главный вопрос |
|---|---|---|
| 01 | [Interface and Control](01_INTERFACE_AND_CONTROL/README.md) | Где взаимодействовать и что там можно сделать |
| 02 | [Powers and Tools](02_POWERS_AND_TOOLS/README.md) | Какие силы реально меняют мир и NPC |
| 03 | [NPC and AI](03_NPC_AND_AI/README.md) | Что такое NPC, что игрок меняет, что решает AI |
| 04 | [Species and Population](04_SPECIES_AND_POPULATION/README.md) | Вид ≠ подвид ≠ один NPC; рождение и смерть |
| 05 | [Debug](05_DEBUG_AND_DEVELOPER_TOOLS/README.md) | Скрытое меню: смотреть vs читы |
| 06 | [Civilizations](06_CIVILIZATIONS/README.md) | Город, работы, король, лояльность |
| 07 | [Meta Systems](07_META_SYSTEMS/README.md) | Культура, язык, религия, клан, семья, книги |
| 08 | [Politics and Conflict](08_POLITICS_AND_CONFLICT/README.md) | Война, союзы, армии, захват |
| 09 | [World Simulation](09_WORLD_SIMULATION/README.md) | Законы, эры, долгосрочные следствия |
| 10 | [Player Experiments](10_PLAYER_EXPERIMENTS/README.md) | Практические «можно ли» |

---

## Модель ответа

```
НАМЕРЕНИЕ ИГРОКА
  → ИНТЕРФЕЙС / СИЛА
  → ДЕЙСТВИЕ
  → ЦЕЛЬ
  → ВНУТРЕННЯЯ СИСТЕМА
  → ОТВЕТ AI / СИМУЛЯЦИИ
  → РЕЗУЛЬТАТ + ОГРАНИЧЕНИЯ
```

Уровни доступа **никогда не смешивать:** VANILLA · DEBUG · INTERNAL · MOD_ONLY.
