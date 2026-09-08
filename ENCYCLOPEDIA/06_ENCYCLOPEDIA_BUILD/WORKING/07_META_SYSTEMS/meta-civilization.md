# Культура, язык, религия, книги, клан, семья

Не сливать в одно «общество». У NPC отдельные id-ссылки.

## Общий ванильный доступ

Noosphere: `*_list` + `*_layer`. Inspect → `selected_*` → trait editor (где есть).  
Основание цивилизации создаёт **culture + language + clan** (гейты подвида). **Religion при основании civ не создаётся.**

PowerBox duplicate/create culture/language/religion = **MOD_ONLY**.

---

## Culture — VANILLA

Мета с CultureTrait, onomastics (шаблоны имён), banner, книги, списки городов/королевств.

- Actor / City / Kingdom держат **по одному** указателю; внутри королевства у жителей могут быть разные культуры.
- Trait editor культуры → `base_stats` носителей при следующем `updateStats`.
- Onomastics — вкладка культуры, не языка.
- Нет дерева технологий; `MAX_LEVEL` не живая механика.
- Гейт: `has_advanced_memory`.

Игрок не кистью «создаёт культуру на тайле». Появление — симуляция основания / конвертация / рождение (`applyParentsMeta`).

## Language — VANILLA

Параллельный meta, LanguageTrait, **без** вкладки Onomastics.  
Гейт: `has_advanced_communication` (не memory).  
Даёт `base_stats` в updateStats. Не поле культуры.

## Religion — VANILLA

Параллельный meta. Гейт как у культуры: `has_advanced_memory`.

- **`base_stats` религии не мержатся** в `updateStats`. Decisions/spells — да, если можно.
- HUD `selected_religion`: имена детей как clan_* — PARTIALLY CONFIRMED, не путать объекты.
- Rites / plots (`big_cast_madness`) завязаны на религию при **продолжении**, не всегда при force-start.
- Закон `world_law_rites` для AI-пула rites.

## Books — VANILLA

Не MetaObject. Запись в `World.world.books`, лежит в слотах **здания**. Culture/Language/Religion индексируют через handler.

Игрок: просмотр `city_books`; не доказан прямой «написать книгу» кликом бога. Создание — AI / plots (force plot = FORCED). Не выдавать TestBook debug за ваниль без кнопки.

## Clan — VANILLA

Не Family и не отдельный класс Bloodline. Членство лидеров/«великих»; `base_stats` в updateStats. Royal clan для короля.

Редактор `clan_trait_editor`. Новый клан — симуляция (`newClan` у короля/лидера без клана), не кисть.

## Family — VANILLA

`Family` **без** traits. Родители/дети/alpha. Не succession. Списки `families` / `city_families` / слой — просмотр.

Создаётся размножением (`applyParentsMeta`), не редактором «создать семью».

## LONG-TERM

Смена meta-trait бьёт по всем носителям. Смена ActorTrait — один NPC. Книги — медленная передача, не мгновенная конвертация королевства.

## RELATED SYSTEMS

[Редакторы](../01_INTERFACE_AND_CONTROL/editors.md) · [Наследство](../06_CIVILIZATIONS/kingdoms-succession-loyalty.md) · [Plots](../01_INTERFACE_AND_CONTROL/possession-and-plots-ui.md)
