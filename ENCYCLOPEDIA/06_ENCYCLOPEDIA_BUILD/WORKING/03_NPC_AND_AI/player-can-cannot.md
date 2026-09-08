# Что игрок может и не может у NPC

## VANILLA — прямое изменение

| Действие | Инструмент | Что меняется |
|---|---|---|
| Черты (разрешённые) | unit trait editor | HashSet + статы + holders + scar |
| Экип | equipment editor | слоты → статы |
| Часть traits/status area | madness, blessing, plague, coffee, shield, sleep, magnet… | area, не всегда тот же id что кнопка |
| Спавн | вкладка units | новый Actor + miracle_born |
| Клон | clone_rain | новый NPC |
| Урон / лечение мира | молния, бомбы, огонь… | getHit / terraform |
| Позиция косвенно | кисти, magnet, пальцы | тайл |
| Possession | кнопка / хоткей | AI выкл, игрок водит |
| Force plot | unit_plots | старт plot **этим** автором |
| Favorite | selected_unit | флаг |
| Топор в городе | axe | wood складу, не статы NPC |

Inspect / Mind / Genealogy / spectate — не симуляция (кроме просмотра).

## VANILLA — нельзя приказать напрямую

| Намерение | Кто решает |
|---|---|
| Конкретная CitizenJob | `City.setCitizenJob` |
| Стать воином / королём / лидером | пороги города и SuccessionTool |
| Конкретная цель боя | `findEnemyObjectTarget` |
| Конкретный город для армии | ближайший reachable enemy |
| Обычный AI path (кроме possess) | Decision loop |
| Гены этого тела | редактор **подвида** (все members dirty) |
| Profession кистью | нет GodPower |

## INTERNAL

Назначение работ, набор армии, выбор лидера при пустом слоте, NeuroLayer Decision, захват ticks.

## DEBUG

Смотреть AI; читы IgnoreDamage / MakeUnitsFollowCursor. Нет найденной кнопки «дать этот trait этому NPC» в debug — для выдачи editor/rain.

## MOD_ONLY

PowerBox army add/remove, convert city — обход.

## Цепочка после клика (не possess)

```
PLAYER изменил trait / HP / войну / еду на карте
  → NPC updateStats / finder врагов / city jobs
  → Decision / fighting / citizen job
  → мир меняется сам
```

Пример: +`peaceful` → не ищет врагов; армия города всё равно может идти.

## RELATED SYSTEMS

[Бой](combat-targeting.md) · [Эксперименты](../10_PLAYER_EXPERIMENTS/README.md)
