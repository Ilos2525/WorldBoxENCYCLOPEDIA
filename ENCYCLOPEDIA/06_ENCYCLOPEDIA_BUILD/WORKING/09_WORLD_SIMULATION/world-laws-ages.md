# Законы мира, эры, долгосрочные следствия

## VANILLA — законы

Вкладка main → окно `world_laws`. Исполнение 49 законов — канон `04` world-laws **CONFIRMED** как слой. Состав кликов внутри prefab не выгружался (QUE-0070) — окно открывается CONFIRMED.

Примеры, которые игрок использует как рычаги:

| Закон | На что влияет (игрок) |
|---|---|
| civ/animals babies | естественное размножение |
| old_age | natural death |
| civ_army | слоты воинов |
| diplomacy | AI plots + `stopAllWars` при выключении |
| rites | AI-пул религиозных rites |
| angry_civilians | гражданские в бою |
| Gaia / nature | часть заклинаний и tile damage, не все God Powers |

`WorldLaws.enable` в коде только включает; UI тогглит bool. Premium на cursed — ассет.

## Эры

Окно `ages` / `world_ages`. Колесо эр CLOSED в `04`. Часть черт (`moonchild`) активна только в нужную эру.

## Катастрофы

Архитектура disasters CLOSED. Кнопки nature (молния, торнадо, огонь) — игрок; облака мира — симуляция. Biomes целиком — gap, не CLOSED.

## Expeditions

**NEGATIVE CANON.** Системы отрядов-экспедиций нет. Достижения explorer считают открытые ассеты, не поход.

## Долгосрочно (уже подтверждённые контуры)

Игрок меняет законы, рельеф, traits подвида, войны. Дальше: рост/смерть населения, работы, AI plots, захват, смена королей, meta-конвертация.

Не закрыто для v1: Housing/Happiness как полный ответ «почему город не растёт», лодки, полный biome dump.

## DEBUG

World Laws tool в debug; SonicSpeed ломает «честное» время.

## RELATED SYSTEMS

[Размножение](../04_SPECIES_AND_POPULATION/reproduction-mortality.md) · [Войны](../08_POLITICS_AND_CONFLICT/wars-armies-capture.md)
