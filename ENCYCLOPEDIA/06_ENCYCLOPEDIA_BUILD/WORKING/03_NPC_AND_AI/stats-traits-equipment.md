# Статы, черты, экипировка, способности

## Источники итогового `Actor.stats` (`updateStats`) — CONFIRMED

Порядок merge (упрощённо):

```
subspecies.base_stats (+ пол) иначе asset
  + clan (+ пол)
  + language
  + culture
  + личные diplomacy/stewardship/intelligence/warfare в data
  + Status.base_stats
  + дефолт-оружие если слот пуст
  + ActorTrait.base_stats (может быть выключен эрой)
  + personality короля/лидера
  + бонус уровня
  + экипировка (сломанное ×0.5)
  → normalize, baby ×0.5 damage/health, …
```

**Religion `base_stats` в этот merge не входят.** Религия может добавлять decisions/spells, если `canUseReligionSpells`. Не писать «все meta дают статы одинаково».

Гены влияют через подвид, не через отдельный genome NPC.

## VANILLA — как игрок меняет черты этого NPC

Окно unit → Traits:

- только `can_be_given` / `can_be_removed`
- `affects_mind` режется тегом `strong_mind`
- `can_edit_traits` на виде
- после успеха — `scar_of_divinity` + stun from UI
- цель всегда один `SelectedUnit`; мультивыбор сбрасывается

Сразу: callbacks add/remove, `setStatsDirty`, holders (combat actions, spells, decisions, special effects) пересобираются **на этом клике**.

Чтение симуляцией: `hasTrait`, merge статов, holders, callbacks (death/growth). Примеры прямых веток: `peaceful` (не ищет врагов), `infertile`, `immortal` (natural death), `mute`, `pacifist` (**не** отключает бой — только plot new_war).

## VANILLA — экип

`unit_equipment_editor` → слоты → merge в том же `updateStats`.

## Способности

Не отдельный «skill tree». Боевые приёмы и заклинания приходят с trait/ассетом/экипом в holders. `skill_combat` / `skill_spell` считаются от warfare/intelligence.

Profession ≠ способность. King/Leader получают personality-статы только на этих ролях.

## DEBUG

`Actor Stats` + `ShowHiddenStats` — просмотр. UnlockAllTraits снимает lock ассетов, не `addTrait` выбранному.

## LIMITATIONS

- `moonchild`/`nightchild` остаются в HashSet; числовой бонус только в нужную эру.
- Точные формулы mass/stamina/XP — OPEN (VQ-06); источники статов закрыты.
- Housing/happiness как полный контур города — не этот документ (gap).

## RELATED SYSTEMS

[Редакторы](../01_INTERFACE_AND_CONTROL/editors.md) · [Капли черт](../02_POWERS_AND_TOOLS/drops-traits-status.md) · [AI](ai-pipeline.md)
