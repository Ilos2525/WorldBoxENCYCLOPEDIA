# Войны, армии, захват

## Война

`DiplomacyManager.startWar` → объект `War`. Для civ: `isEnemy` ⇔ активная война. Без War цивилизации не в войне.

Типы: `normal` (plot new_war), `whisper_of_war`, `spite` (total, forced, нельзя stop_war plot), `rebellion`, `inspire`. Поле `clash` не создаётся в init — INTERNAL curiosity.

Conquest как WarType нет: захват городов — параллельная система во время isEnemy.

### VANILLA начать

| Инструмент | Стороны выбирает игрок? |
|---|---|
| Whisper of War | да, две стороны |
| Spite drop | цель капли |
| Inspiration | город → новое kingdom + война |
| Force plot new_war | автор NPC, цель код |
| AI plot | INTERNAL |

`startWar` законы не читает. Выключение `world_law_diplomacy` → `stopAllWars` и режет AI plots.

### VANILLA закончить

Нет pair-peace picker. Friendship drop; plot `attacker_stop_war` если `can_end_with_plot` (не spite); смерть main / 0 городов после 10 лет; закон дипломатии off.

Захват города войну **сам не заканчивает**.

Получатель захвата может быть **main** войны, не штурмующая армия.

## Армии

Army = meta, **1 на город**. Warrior = profession. Можно набирать **без войны**; марш только если война и заполнение ~**70%**.

Цель капитана = ближайший reachable enemy city. **Нет** ванильных приказов армии. Окно/слой army_targets — визуал.

Капитан на вражеском городе предпочитает тайл watch tower.

PowerBox create/add/remove army = **MOD_ONLY**.

## Захват

Warrior/King/Leader на тайлах вражеского города → очки → ticks до **100** → `finishCapture` → `joinAnotherKingdom(pCaptured)`.

Очки каждый кадр сбрасываются — нужно присутствие. Нет захватчиков → ticks **падают** (−0.5), не мгновенный ноль.

Защитники-воины стопорят прогресс при ticks ≥ 5. Watch tower: **+10** хозяину каждые 0.1с × число готовых башен.

Гражданский Unit очки не даёт. Убивать всех не обязательно.

Convert city кистью = **MOD_ONLY** (PowerBox).

## Rebellion

Plot / inspiration → `makeOwnKingdom`, не capture ticks. Осколок не наследует allianceID.

## RELATED SYSTEMS

[Дипломатические силы](../02_POWERS_AND_TOOLS/diplomacy-powers.md) · [Бой и башни](combat-defense.md)
