# Как работают силы

**Уровень:** VANILLA для кнопок на `level1`.  
**Статус:** CONFIRMED (сцена + `PowerButton` + `PlayerControl.clickedFinal`).

## WHAT PLAYER CAN DO

Выбрать инструмент на вкладке и применить к тайлу / юниту / двум кликам (часть дипломатии).

## WHERE TO FIND IT

Имя кнопки Active/Special = `GodPower.id` (для 337 из ~340 сил на canvas).

```
PLAYER click PowerButton
  → PowerButtonSelector
  → клик по миру
  → PlayerControl.clickedFinal
  → GodPower.click_power_* / click_brush_* / click_action
  → DropManager / MapAction.terraform* / spawn / UI toggle
```

Типы исполнения (не путать имена):

| Тип | Пример | Что это |
|---|---|---|
| Terraform / кисть тайла | `tile_soil`, `wall_iron` | меняет тайл |
| `$template_drops$` | `madness`, `blessing` | снаряд/капля → `action_landed` |
| `$template_spawn_actor$` | `human`, `zombie` | новый Actor |
| `$template_drop_building$` | `flame_tower`, `tumor` | здание, не city watch tower |
| Special / overlay | `culture_layer`, `pause` | отображение или пауза |
| Два клика meta | `whisper_of_war`, `unity` | выбор двух kingdom |

Одно имя (`lightning`, `fire`, `bomb`) может жить в GodPower, spell и trait. Кнопка HUD — God Power, не заклинание мага.

## WHAT HAPPENS AFTER THE ACTION

Мир меняется только когда срабатывает делегат силы. Выбор кнопки без клика по карте ничего не делает (кроме тогглов Special).

## WHAT AI / SIMULATION DECIDES

Сила задаёт вход (trait, War, дырка в земле). Дальше NPC сами: Decision, работы, марш армии, захват.

Gaia law может блокировать **spell** травы, не обязательно одноимённую God Power — смотреть конкретный ассет.

## LIMITATIONS

- `show_tool_sizes` есть в коде; HUD размеров кисти на вкладках не инвентаризирован (PARTIALLY CONFIRMED).
- Premium/rank на силах — REQUIRES LIVE VALIDATION видимости.
- Модовые GodPowers PowerBox — MOD_ONLY.

## RELATED SYSTEMS

[Вкладки](../01_INTERFACE_AND_CONTROL/hud-tabs.md) · [NPC](../03_NPC_AND_AI/player-can-cannot.md)
