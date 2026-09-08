# Бой юнита и оборона

Детали таргетинга: [combat-targeting](../03_NPC_AND_AI/combat-targeting.md).

## VANILLA

Игрок не отдаёт «атакуй этого». Молния/бомбы — урон по области, не combat command.

## Городские watch tower

Единственная **civ** стреляющая оборона + очки capture хозяину.

Город строит сам (`order_watch_tower`: pop 30, hall, камень/золото, лимит 1 + бонусы). Игрок **не** ставит `watch_tower_*`.

Недостроенная не стреляет. Во время capture/danger новых строек нет.

Радиус поиска как у юнитов (chunk sight 1). Civ↔civ только если War.

## Другие «башни» игрока

| Drop | Стреляет | City building |
|---|---|---|
| flame_tower | fireball | нет (demon kingdom) |
| corrupted_brain | madness_ball | нет |
| ice_tower | нет (заморозка + cold_one) | нет |
| angle_tower | нет (спавн angle) | нет |

## Стены

Кисти `wall_*` — terraform **block** тайлы. Город их не строит. Это не BuildingTower.

Barracks — слоты воинов, не выстрел.

## WHAT AI DECIDES

Башня сама ищет цель. Капитан штурма целится в тайл watch tower. Юниты бьют attack_target параллельно ticks захвата.

## RELATED SYSTEMS

[Захват](wars-armies-capture.md)
