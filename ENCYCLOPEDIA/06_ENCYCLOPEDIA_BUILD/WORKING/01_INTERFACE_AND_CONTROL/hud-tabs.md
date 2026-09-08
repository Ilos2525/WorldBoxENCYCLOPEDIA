# Вкладки HUD

**Статус:** VANILLA CONFIRMED (сцена `level1`). Подписи вкладок — locale `PowerTabLibrary`.

## WHAT PLAYER CAN DO

Переключать главные вкладки сил и применять инструменты к миру. После inspect объекта открывается **другая** вкладка (`selected_*`) — это не смена набора кистей мира.

## WHERE TO FIND IT

Переключатели на HUD: `t_drawing`, `t_kingdoms`, `t_creatures`, `t_nature`, `t_bombs`, `t_other` (**LIKELY** привязка к creation / noosphere / units / nature / destruction / other).

На силовых вкладках кроме `main` первым хромом идут `tab_back_button`, `pause`, `clock`.

### `main` — хаб (19 кнопок)

Пауза, часы, **inspect**, законы мира, эпохи, история, статистика, шаблоны мира, сохранения, опции, достижения, сообщество, скрыть UI, Steam, промо.

GodPowers: `pause`, `clock`, `inspect`, `hide_ui`.  
Окна: `world_info`, `world_laws`, `world_ages`, `world_history`, `statistics`, `new_world_templates`, `saves_list`, хаб `other` (не путать с окном `settings`), `achievements`, `community_links`, steam.

HUD `settings_button` открывает окно **`other`**. `ButtonEvent.openSettings()` открывает **`settings`**. Это два окна. Полное дерево настроек PARTIALLY CONFIRMED.

### `creation` — World Shaping (~50)

Тайлы океана→вершин, стены `wall_*`, лопаты, палец, воронка, ластики (`sponge`, `sickle`, `bucket`, `pickaxe`, `spade`, `axe`, `demolish`, `life_eraser`, `scissors`), `border_brush`, `paint`, fuse, fireworks, принтеры форм.

Все Active-имена совпали с `PowerLibrary`. **CONFIRMED.**

### `noosphere` — Noosphere and Life (~68)

Дипломатия: `city_select`, `relations`, `spite`, `friendship`, `inspiration`, `whisper_of_war`, `discord`, `unity`.

Списки цивилизаций **и** парные слои карты (`*_list` + `*_layer`): войны, армии, альянсы, королевства, города, кланы, религии, культуры, языки, семьи, подвиды, plots, избранное.

Оверлеи: имена, метки, курсоры, счастье, задачи, поток денег, пузыри речи…

Это вход **смотреть** Culture/Religion/Language/Kingdom. Отдельной кнопки «создать культуру» на HUD нет.

Заглушки: `TradeRoutes` / `trade_routes_zones` → `under_development`.

### `units` — существа (~123)

Почти все — spawn `GodPower` с id = имя кнопки: human/orc/elf/dwarf, животные, маги, зомби, башни-существа, civ-варианты.

Полный перечень имён: `_extract/player_access_join.json` → `main_tabs.units`.

### `nature` (~57)

Климат и катастрофы: температура ±, молния, землетрясение, торнадо, дождь, огонь, кислота, лава. Семена биомов `seeds_*`, удобрения, руды, гейзеры, вулкан, облака.

`seedsSolitude` есть кнопкой Active, id нет в дампе `PowerLibrary` — PARTIALLY CONFIRMED / возможна мёртвая кнопка.

### `destruction` — Destruction and Chaos (~40)

Взрывы, бомбы, инфекции (`zombie_infection`, `mush_spores`, `plague`, `madness`, `corrupted_brain`), `desire_*`, waypoint-артефакты, living plants/house, conway.

Кнопки `mush_unit` на вкладке **нет** (сила в коде есть).

### `other` (~36)

`magnet`, `divine_light`, `monolith`, `golden_brain`. Капли: blood rain, shield, blessing, curse, coffee, powerup, clone_rain, jazz, dispel, sleep, `dust_*`. Редакторы дождя черт и экипировки: `traits_*_rain[_edit]`, `equipment_rain[_edit]`.

## WHAT HAPPENS AFTER THE ACTION

Выбор Active-силы не меняет мир, пока нет клика/кисти по тайлу (кроме Special-тогглов: пауза, слои, hide UI).

## WHAT AI / SIMULATION DECIDES

Вкладки не приказывают NPC. Они либо меняют мир силой, либо открывают просмотр meta.

## LIMITATIONS

- Special-слои (`culture_layer`, `army_targets`, …) — отображение, не команда армии.
- `relations` — просмотр, не запись дипломатии.
- Скорость мира — кнопки TimeScale / clock, не debug SonicSpeed.

## RELATED SYSTEMS

[Силы](../02_POWERS_AND_TOOLS/how-powers-work.md) · [Дипломатические силы](../02_POWERS_AND_TOOLS/diplomacy-powers.md)
