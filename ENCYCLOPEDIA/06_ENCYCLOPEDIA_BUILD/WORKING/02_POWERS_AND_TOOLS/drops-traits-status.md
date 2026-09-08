# Капли: статус, черты, дожди, пыль

**Уровень:** VANILLA, вкладка **other** (часть destruction).

## Blessing / curse / shield / coffee / sleep / dispel / powerup / jazz / blood_rain

Капли `$template_drops$` → area status или trait.

| Кнопка | Типичный эффект | Уровень |
|---|---|---|
| `blessing` | `addTrait("blessed")` + снять status `cursed` | VANILLA |
| `curse` | статус/проклятие (не путать с blessed) | VANILLA |
| `shield`, `coffee`, `sleep`, `powerup` | status таймерные | VANILLA |
| `clone_rain` | новый клон: копия traits + `clone` + `miracle_born` + `fragile_health` | VANILLA |
| `divine_light` | `clearBadTraitsFrom` (traits с флагом divine light), в т.ч. madness | VANILLA |
| `magnet` | status `magnetized` | VANILLA |
| `monolith`, `golden_brain` | особые здания/объекты силы | VANILLA |

## Trait Rain

```
other → traits_gamma/delta/omega_rain_edit  → окно набора id
other → traits_*_rain                       → useTraitRain
```

Дождь **пропускает** trait, если операция Add и `!can_be_given`. Это не секретный обход редактора для madness.

Equipment rain — то же для предметов (`equipment_rain_edit` / `equipment_rain`).

Premium flags в коде редакторов дождя — REQUIRES LIVE VALIDATION.

## Пыль — важная ловушка

Кнопки `dust_white`, `dust_black`, `dust_red`, `dust_blue`, `dust_gold`, `dust_purple` стоят рядом с красками.

**`dust_gold` не выдаёт золото городу или NPC.**  
Эффект: юниты **забывают** kingdom и city (`forgetKingdomAndCity`). **CONFIRMED** (экономика / jobs research).

Не использовать как «добавить gold на склад».

## Tumor / biomass тайлы

Destruction здания `tumor` / `biomass` → ходьба по тайлу → `tumor_infection` / madness (с фильтрами). INDIRECT + area тайла, не unit editor.

## WHAT AI / SIMULATION DECIDES

Status/trait → `updateStats` и decisions. Clone — отдельный новый Actor со своим AI. Divine light только снимает помеченные «плохие» черты, не лечит всё.

## DEBUG / MOD_ONLY

UnlockAllTraits не заменяет rain. PowerBox не нужен для этих капель.

## RELATED SYSTEMS

[Traits NPC](../03_NPC_AND_AI/stats-traits-equipment.md) · [Spawn](spawn-tools.md)
