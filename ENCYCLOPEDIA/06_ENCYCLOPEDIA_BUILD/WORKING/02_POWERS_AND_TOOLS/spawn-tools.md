# Spawn

**Уровень:** VANILLA, вкладка **units** (и часть nature/destruction как здания).

## WHAT PLAYER CAN DO

Создать нового Actor кистью spawn. Это **не** рождение (`BabyMaker`) и не правка подвида.

## WHERE TO FIND IT

Вкладка creatures: кнопки `human`, `orc`, `elf`, `dwarf`, животные, `zombie`, маги, …

```
PLAYER → GodPower spawn
  → PowerLibrary.spawnUnit
  → spawnNewUnitByPlayer(..., pMiracleSpawn: true)
  → createNewUnit
```

## WHAT HAPPENS AFTER THE ACTION

1. Берётся `ActorAsset` кнопки. Стартовые `ActorAsset.traits` копируются (у зомби-вида — `setZombie` → trait `zombie`).
2. Всем player-spawn вешается **`miracle_born`** (`can_be_given = false` в редакторе).
3. Подвид: если вид `can_have_subspecies`, ищется **ближайший** подвид того же вида (`species_spawn_radius`, default **40** тайлов). Нашли → JOIN. Нет → `newSpecies` → новый подвид. **CONFIRMED.**

Изоляция: спавн далеко от сородичей создаёт **новый Subspecies**. Спавн рядом вливает в существующий. Это главный ванильный способ плодить параллельные популяции одного вида.

## WHAT AI / SIMULATION DECIDES

Новый NPC сразу в Decision/Job loop (если не possessed). Гражданские попытаются найти город/работу. Зомби-вид — поведение ассета зомби, не «заражение соседа».

## Ложные ожидания

| Кнопка | Не делает |
|---|---|
| `zombie` | не вешает `zombie` на уже живых; спавнит новый зомби-вид |
| `zombie_infection` | не `addTrait("zombie")`; даёт `infected` при условиях |
| Spawn human | не копирует выбранного inspect-юнита (это не clone_rain) |

`mush_unit` в библиотеке есть, **кнопки на units нет** — spawn mush с toolbar не подтверждён.

## Clone

**other → `clone_rain`:** клон соседа с копией traits + `clone` + `miracle_born` + `fragile_health`. Другой конвейер, не spawn-кнопка вида.

## DEBUG

`FastSpawn` / `UltraFastSpawn` убирают задержку спавна. Не новый вид существ.

## MOD_ONLY

PowerBox extra spawns / FindAllCreatures — не ваниль.

## RELATED SYSTEMS

[Подвид и членство](../04_SPECIES_AND_POPULATION/species-subspecies.md) · [Clone и рождение](../04_SPECIES_AND_POPULATION/reproduction-mortality.md)
