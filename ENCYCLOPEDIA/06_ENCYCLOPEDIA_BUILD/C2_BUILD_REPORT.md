# C2 BUILD REPORT

**Дата:** 2026-09-08  
**Папка:** `WorldBox Research/06_ENCYCLOPEDIA_BUILD/WORKING/`

## Что создано

Рабочий слой энциклопедии игрока (~40 markdown-файлов): вход, 10 разделов, 18 карточек экспериментов. Источники `04` и `05` не удалялись и не копировались целиком.

## Разделы приоритета 1–5 — собраны

| Раздел | Состояние |
|---|---|
| 01 Interface and Control | Полный v1: вкладки, окна, редакторы, possession/plots, границы |
| 02 Powers and Tools | Полный v1: конвейер сил, терраформ, spawn, инфекции, капли, дипломатия; ловушки имён кнопок |
| 03 NPC and AI | Полный v1: модель Actor, статы/traits, AI pipeline, can/cannot, бой |
| 04 Species and Population | Полный v1: вид≠подвид, гены/birth, reproduction/mortality |
| 05 Debug | Полный v1: unlock, наблюдение vs читы vs INTERNAL vs моды |

## Разделы 06–10 — начаты и покрывают уже исследованное

| Раздел | Состояние |
|---|---|
| 06 Civilizations | Работы/экономика + король/лидер/лояльность |
| 07 Meta | Сводка Culture/Language/Religion/Books/Clan/Family |
| 08 Politics | Дипломатия, войны/армии/захват, башни |
| 09 World | Законы, эры, negative Expeditions |
| 10 Experiments | 18 карточек «можно ли» |

Мета-системы и политика сжаты в сводки: детали остаются в `05_PLAYER_RESEARCH`. Для ответа игроку сводки самодостаточны.

## Что ещё можно дособрать из уже имеющихся исследований (не новый код)

- Полные списки кнопок units/nature из `_extract` как справочник id
- Расширить Culture/Language/Religion из длинных документов `05` (конвертация, книги по типам, clan ascension)
- Больше слагаемых loyalty/opinion по таблицам фаз 19/21
- Больше World Laws «что включить чтобы…» из канона `04` world-laws.md

Это полировка, не пробел доступа.

## Реальные пробелы (не закрывать автоисследованием)

Как в `OPEN_RESEARCH_GAPS.md`: LIVE debug burger и layout окна debug; LIVE редакторов; Housing/Happiness; полный Decision catalog; Biomes; Boats; формулы статов VQ-06.

В статьях это помечено CONFIRMED / PARTIALLY / REQUIRES LIVE VALIDATION / OPEN, не выдано за LIVE_CONFIRMED.

## Уровни доступа

VANILLA / DEBUG / INTERNAL / MOD_ONLY проведены через приоритетные статьи и эксперименты. PowerBox army/convert/resources/duplicate meta отделён.

## Навигация `04`

Симуляционный канон не переписывался массово. Рабочий вход игрока — эта папка `WORKING/`.
