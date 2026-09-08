# Боевой таргет NPC

**Не путать с целью армии.** Захват города — отдельный счётчик на тайлах.

| | Армия / город | Бой юнита |
|---|---|---|
| Поле | `City.target_attack_city` | `Actor.attack_target` |
| Кто пишет | `CityBehCheckAttackZone` | поиск врага / ответ на удар |
| Смысл | куда идёт капитан | кого бить сейчас |

## VANILLA

Игрок **не** назначает attack_target. Молния бьёт тайл, не отдаёт приказ «атакуй этого».

## Как AI выбирает цель — CONFIRMED

`EnemiesFinder` в чанках `unit_chunk_sight_range = 1`. Civ↔civ без `War` в список не попадают. Мобы — `KingdomAsset.isFoe`.

Обычно ближайший; если кандидатов > 50 — 40% шанс случайного.

`peaceful` → не ищет врагов. `pacifist` **не** отключает поиск — воин-пацифист дерётся; pacifist режет plot `new_war`.

Warrior/king/leader не civilian, но **не фермят** same-species мирных, пока нет xenophobe / `world_law_angry_civilians` (с оговоркой same culture + same species).

В радиусе атаки: `skipBehaviour` (нет path/decision в этот кадр). Вне радиуса: task `fighting` **подменяет** follow капитана; цель города не сбрасывается.

## Связь с захватом

Стоять на тайле вражеского города (Warrior/King/Leader) качает capture **параллельно** бою. Убивать всех защитников не обязательно.

## DEBUG

Overlay стрелок целей, tooltip AI (task=`fighting`). Tool `Unit Info` показывает attack_target.

## RELATED SYSTEMS

[Армии и захват](../08_POLITICS_AND_CONFLICT/wars-armies-capture.md) · [Оборона](../08_POLITICS_AND_CONFLICT/combat-defense.md)
