# Конвейер AI

**Уровень решений:** INTERNAL каждый кадр; игрок задаёт входы.  
**Полный каталог Decision id:** не собран (не блокирует эту статью).

## Слои (не путать имена)

| Слой | Что это | Кто выбирает |
|---|---|---|
| Decision | `UtilityBasedDecisionSystem` → обычно `setTask` | AI, веса |
| ActorJob | список задач (`miner`, `make_decision`, …) | AI / подстановка CitizenJob |
| Task | цепочка `Beh*` | текущий job |
| Action | один шаг | task |
| CitizenJob | спрос города miner/farmer/… | **город**, не игрок |
| UnitProfession | Unit/Warrior/King/Leader | город / succession |

Иконка «кузнец» в задаче ≠ CitizenJob в библиотеке.

Размножение — Decision/Task, **не** CitizenJob.

## Кадр Actor (упрощённо)

```
бой уже идёт → skip
поиск врага → task fighting, skip
движение / verifier → skip
иначе если не unconscious и не possessed:
  DecisionHelper.makeDecisionFor
  ai.update()   Job → Task → Action
```

Бой перебивает гражданский AI. Цель армии города при этом **не** сбрасывается.

`registerDecisions` при updateStats: traits + clan + culture + language + religion (если можно spells) + subspecies + profession + spells.

## WHERE TO FIND IT (смотреть, не приказывать)

| Что увидеть | Где | Уровень |
|---|---|---|
| Последнее Decision | окно unit → **Mind** | VANILLA |
| job / task / action / citizen_job | DebugTool → **Actor AI** (после NewDebugWindow на рамке debug) | DEBUG |
| веса Decision | DebugTool → **Actor Decisions** | DEBUG |
| job/task / attack_target у курсора | DebugTool → **Unit Info** / **Actor AI** | DEBUG |

Mind `runSimulationForMindTab` не ставит gameplay task.

## Possession

`_has_status_possessed` → нет decision и нет `ai.update`. См. [UI possession](../01_INTERFACE_AND_CONTROL/possession-and-plots-ui.md).

## LIMITATIONS

Игрок не выбирает Decision, Task или CitizenJob в ванили. Favorite влияет на сортировки, не на «стать королём».

## RELATED SYSTEMS

[Границы](player-can-cannot.md) · [Работы города](../06_CIVILIZATIONS/cities-jobs-economy.md) · [Debug](../05_DEBUG_AND_DEVELOPER_TOOLS/debug-menu.md)
