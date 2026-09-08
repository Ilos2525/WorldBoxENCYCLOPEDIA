# Вид, подвид, членство

**Статус:** CONFIRMED по коду + ванильный HUD. LIVE spawn-расстояния не гонялись (REQUIRES LIVE VALIDATION визуала; правило кода закрыто).

## Три объекта

| Имя | Код | Ванильный редактор |
|---|---|---|
| **Species (вид)** | `ActorAsset` | **нет** |
| **Subspecies (подвид)** | meta мира: id, nucleus, traits, birth list | Traits / Birth / Genetics |
| **Membership** | `Actor.subspecies` ссылка | окна unit/subspecies **не** пересаживают живущего |

Несколько подвидов одного вида — норма. У каждого свой геном и birth-контейнер.

Членство **не** копирует SubspeciesTrait в `Actor.traits`. Статы подвида читаются при `updateStats`.

## VANILLA — создать новый подвид

Единственный массовый способ, который игрок контролирует позицией спавна:

```
spawn вида с can_have_subspecies
  → getNearbySpecies (stop at first), радиус species_spawn_radius (default 40)
  → если есть → JOIN
  → иначе newSpecies → новый подвид, этот NPC JOIN
```

Спавн в изоляции → новая популяция. Спавн в куче того же вида → та же популяция.

Окна подвида **не** вызывают `setSubspecies` для перекладки уже живущего NPC на другой экземпляр.

## VANILLA — смотреть / править существующий

Noosphere → `subspecies_list` или inspect юнита → подвид → editors.

## SIMULATION / INTERNAL

Эволюция (`parent_subspecies` / `evolved_into`) — симуляция, не кнопка «эволюционировать сейчас». Не разворачивать неисследованный каталог эволюции в v1; факт: это не editor NPC.

## MOD_ONLY

Не требуется для isolate-spawn. Не путать с мод-кнопками duplicate.

## LIMITATIONS

`!can_have_subspecies` → подвида нет.  
Правка одного подвида не синхронизирует остальные того же вида.

## RELATED SYSTEMS

[Spawn](../02_POWERS_AND_TOOLS/spawn-tools.md) · [Гены](genetics-birth-traits.md)
