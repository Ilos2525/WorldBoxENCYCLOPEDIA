# 03 — NPC and AI

**Главный вопрос:** что такое живой персонаж, что игрок меняет напрямую, и почему дальше NPC действует сам.

```
Игрок меняет состояние NPC
  → AI читает состояние
  → выбирает Decision / Job / Task
  → NPC действует
```

Исключение кадра: **Possession** — Decision и `ai.update` выключены.

| Статья | Содержание |
|---|---|
| [Что такое NPC](what-is-an-npc.md) | Actor + данные vs вид/город |
| [Статы, черты, экип](stats-traits-equipment.md) | updateStats, editor, holders |
| [Конвейер AI](ai-pipeline.md) | Decision → Job → Task → Action |
| [Что можно и нельзя](player-can-cannot.md) | прямые vs автономные решения |
| [Боевой таргет](combat-targeting.md) | attack_target ≠ цель армии |

**Источники:** `NPC_CORE_STATE_AND_AI_ARCHITECTURE.md`, traits phases 4–6, combat 25, jobs 27.
