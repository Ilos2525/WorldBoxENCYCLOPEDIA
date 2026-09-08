# Кисти и терраформ

**Уровень:** VANILLA, вкладка **creation** (+ часть nature).

## WHAT PLAYER CAN DO

Рисовать тайлы, ставить **block-стены**, стирать жизнь/здания, рубить, копать.

## WHERE TO FIND IT

Вкладка World Shaping (`creation`):

- тайлы: `tile_deep_ocean` … `tile_summit`
- стены: `wall_order`, `wall_evil`, `wall_ancient`, `wall_wild`, `wall_green`, `wall_iron`, `wall_light`
- высота: `shovel_plus` / `shovel_minus`, `finger`, `vortex`
- ластики: `sponge`, `sickle`, `bucket`, `pickaxe`, `spade`, `axe`, `demolish`, `life_eraser`, `scissors`
- прочее: `border_brush`, `paint`, принтеры `printer_*`

Nature: семена биомов, удобрения, руды как drops/спавн минералов.

## WHAT HAPPENS AFTER THE ACTION

Terraform меняет тип тайла / высоту / block. Город **не** строит `wall_*`: это не city building и не `BuildingTower`.

Особые экономические эффекты ластиков (**CONFIRMED**, экономика города):

| Сила | Если цель в городе | Результат |
|---|---|---|
| `axe` по дереву | да | дерево падает **и** wood сразу в stockpile (`resources_given`) |
| `pickaxe` по минералу | — | здание месторождения **уничтожается**, городу ресурс **не** начисляется |
| `sickle` | — | меньше растительности → меньше слотов gatherer |
| `demolish` / бомбы | — | минус здания → минус слоты работ и склады |

## WHAT AI / SIMULATION DECIDES

Появились деревья/руды **на зонах города** + есть stockpile → городской AI откроет слоты woodcutter / miner_deposit. Игрок слоты не назначает.

## LIMITATIONS

- Стены-кисть ≠ городская стена-здание (такого building нет).
- Принтеры — шаблон `$template_printer$`, на canvas имена `printer_hexagon` и т.д., не id `printer`.
- Полный эффект каждого биома на Actor — не закрыт (gap biomes); семена как кнопки CONFIRMED.

## RELATED SYSTEMS

[Работы и склад](../06_CIVILIZATIONS/cities-jobs-economy.md) · [Оборона](../08_POLITICS_AND_CONFLICT/combat-defense.md)
