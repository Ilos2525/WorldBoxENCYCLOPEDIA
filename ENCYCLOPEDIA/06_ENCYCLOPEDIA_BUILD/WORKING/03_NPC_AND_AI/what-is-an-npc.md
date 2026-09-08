# Что такое NPC

**Статус:** CONFIRMED. LIVE не требовался для этой модели.

## WHAT PLAYER CAN DO

Inspect конкретного существа. Это экземпляр на карте, не «вид human» и не «весь город».

## Модель

```
Actor (runtime на карте)
  + ActorData (сейв)
  + ссылки на meta (subspecies, city, culture, …)
  + runtime: CitizenJob, attack_target, statuses, AI job/task
```

| Слой | Чей |
|---|---|
| Этот NPC | id, имя, HP, nutrition, happiness, stamina, traits, экип, profession, ids meta, родители |
| Вид | `ActorAsset` — каталог, ванильный редактор **не** пишет |
| Подвид | гены и subspecies traits; у NPC только **ссылка** |
| Гены | только у Subspecies, **личного генома нет** |
| CitizenJob | runtime слот города, **не** profession |
| UnitProfession | Unit / Warrior / King / Leader |

Голод = низкий `nutrition`, не отдельный trait. Болезни могут быть trait (`plague`) или status — смотреть ассет.

## WHERE TO FIND IT

Inspect / вкладка `selected_unit` / окно `unit`. Списки избранного на noosphere.

## WHAT AI / SIMULATION DECIDES

Каждый кадр читает и личные поля, и чужие объекты (культура даёт статы всем носителям при dirty).

## LIMITATIONS

Смена черты **культуры** ≠ смена `Actor.traits`.  
Смена `Actor.traits` ≠ смена birth-шаблона подвида.

## RELATED SYSTEMS

[Статы](stats-traits-equipment.md) · [Подвид](../04_SPECIES_AND_POPULATION/species-subspecies.md)
