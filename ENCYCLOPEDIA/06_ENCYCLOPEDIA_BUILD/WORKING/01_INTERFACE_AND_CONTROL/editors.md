# Редакторы

**Статус:** входы HUD CONFIRMED. Premium-lock кнопки редактора черт — в коде; видимость REQUIRES LIVE VALIDATION.

Редактор меняет **свой** объект. Их нельзя подменять друг другом.

| Редактор | Объект | Не меняет |
|---|---|---|
| Unit Traits | `Actor.traits` одного NPC | подвид, гены, birth list |
| Unit Equipment | слоты предметов этого NPC | CitizenJob |
| Subspecies Traits | `Subspecies` traits | `ActorAsset` (вид) |
| Birth Traits | шаблон рождения подвида | живущих NPC |
| Genetics | геном **подвида** | личный геном NPC (его нет) |
| Culture / Language / Clan / Kingdom traits | meta-объект | личные ActorTrait, если нет отдельной симуляции |
| Trait / Equipment Rain editor | набор id для дождя | не то же, что unit editor |
| World Laws | включение законов мира | не редактор NPC |
| Plots editor | force-start Plot **этим** NPC | не кисть madness |

## VANILLA — где открыть

```
Выбрать объект (inspect / список)
  → вкладка selected_*
  → кнопка редактора
  → ScrollWindow meta + внутренняя вкладка
```

Подтверждённые методы (сцена + код):

| Кнопка | Метод |
|---|---|
| `unit_trait_editor` | `ButtonEvent.openUnitTabTraitsEditor` |
| `unit_equipment_editor` | `openUnitTabEquipmentEditor` |
| `culture_trait_editor` | `SelectedCulture.openTraitsEditorTab` |
| `culture_onomastics` | `openOnomasticsTab` |
| `subspecies_trait_editor` | `SelectedSubspecies.openTraitsEditorTab` |
| `subspecies_birth_traits_editor` | `openBirthTraitsTab` |
| `subspecies_genetics` | `openGeneticsTab` |
| `language_trait_editor` | `SelectedLanguage.openTraitsEditorTab` |
| `clan_trait_editor` | `SelectedClan` (и отдельный GO на religion tab — аномалия имён) |
| `kingdom_trait_editor` | королевство |
| `world_laws` на main | окно законов **CONFIRMED**; состав prefab QUE-0070 не разбирался |
| `traits_*_rain_edit` на other | `trait_rain_editor` CONFIRMED |
| `equipment_rain_edit` | `equipment_rain_editor` CONFIRMED |

## WHAT HAPPENS AFTER THE ACTION (unit traits)

```
клик в ActorTraitsEditor
  → addTrait / removeTrait (если can_be_given / can_be_removed)
  → callbacks, setStatsDirty, stun from UI
  → маркер scar_of_divinity
```

Эффект статов — **на этом же клике**, не при следующем рождении. Подробно: [NPC traits](../03_NPC_AND_AI/stats-traits-equipment.md).

Черты с `can_be_given = false` (madness, zombie, desire_*, clone…) **этим редактором не выдаются**. Другие входы: [капли и инфекции](../02_POWERS_AND_TOOLS/drops-traits-status.md).

## WHAT AI / SIMULATION DECIDES

После смены черт/экипа AI на следующем кадре (если не possessed) заново читает decisions/holders. Игрок не выбирает новую Job кнопкой редактора.

Правка **культуры** меняет `base_stats` всех носителей при их следующем `updateStats`, не копию на одном акторе.

Правка **birth traits** не итерирует живущих `subspecies.units`.

## DEBUG

`UnlockAllTraits` и т.п. снимают lock **с ассетов**, не выдают черту выбранному NPC. Выдача конкретному — ванильный editor / rain.

`debugUnlockAll` в `ButtonEvent` — методы есть; кнопок на главных вкладках нет.

## MOD_ONLY

PowerBox EditResources и прочие окна мода ≠ эти редакторы.

## LIMITATIONS

- Нет ванильного редактора **Species** (`ActorAsset`).
- Нет кнопки «назначить CitizenJob» в редакторах.
- Religion trait editor на HUD не подтверждён однозначно (имена clan_*).
- Onomastics: кнопка есть; алгоритм имён — OPEN (VQ-07), не нужен для «где кликнуть».

## RELATED SYSTEMS

[Подвид](../04_SPECIES_AND_POPULATION/species-subspecies.md) · [Plots UI](possession-and-plots-ui.md)
