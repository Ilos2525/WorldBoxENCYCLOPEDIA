# Разрушение и инфекции

**Уровень:** VANILLA, вкладка **destruction** (часть — nature).

Имена кнопок **не равны** именам traits. Это самый частый ложный вывод.

## Madness

| | |
|---|---|
| Игрок | destruction → `madness` |
| Цель | юниты в чанке, радиус ≈ 3 |
| Эффект | `addTrait("madness")` сразу, **без** `can_be_given` |
| Trait editor | madness **нельзя** выдать |
| Снять | other → `divine_light` (у madness `can_be_removed_by_divine_light`); в редакторе `can_be_removed = false` |
| Не путать | plot rite `big_cast_madness` (случайный вражеский город, 80%, нужен прогресс) |

**VANILLA CONFIRMED.**

Дополнительно: здание `biomass` → тайл → step может дать madness (фильтр tumor). INDIRECT.

## Desire_*

Кнопки `desire_alien_mold`, `desire_computer`, `desire_golden_egg`, `desire_harp` — area `addTrait` того же id, r≈3. Сразу `forcedKingdomAdd`.

`waypoint_*` спавнят **здание**, не desire-trait.

## Инфекции

| Кнопка | Trait | Условие | Не делает |
|---|---|---|---|
| `zombie_infection` | `infected` | `can_turn_into_zombie` и нет `zombie` | не `addTrait("zombie")` |
| `mush_spores` | `mush_spores` | `can_turn_into_mush` | нет кнопки `mush_unit` на HUD |
| `plague` | `plague` | все в r≈4; повтор — shake | — |
| `corrupted_brain` | drop здания | моб-башня, не city | не watch tower |

Живой юнит становится зомби **не** каплей zombie, а цепочкой инфекция → смерть → `turnIntoZombie` (новый юнит). **CONFIRMED.**

`infected` можно также выдать unit editor (`can_be_given` default true). Капля — массовый вход.

## Бомбы / стихии

Destruction + nature: TNT, nuke, fire, acid, lava, lightning, earthquake, tornado… Урон/`getHit`/terraform. Не combat-приказ «атакуй того».

Lightning на nature ≠ spell `summon_lightning` у мага.

## WHAT AI / SIMULATION DECIDES

После madness: callbacks (в т.ч. смена kingdom — фаза 5). После plague/infected: тик урона, возможный transform при смерти. Город и войны сами.

## LIMITATIONS

- Trait Rain **не** обходит `can_be_given`: madness/zombie/desire дождём не выдаются.
- Cure как GodPower на canvas **нет**. Снятие plague/infected/mush/tumor — drop `cure` через спелл мага (`cast_cure`) или ждать каст. INDIRECT.

## RELATED SYSTEMS

[Капли](drops-traits-status.md) · [Смертность](../04_SPECIES_AND_POPULATION/reproduction-mortality.md) · [Plots madness](../01_INTERFACE_AND_CONTROL/possession-and-plots-ui.md)
