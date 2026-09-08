# OPEN RESEARCH GAPS

**Фаза:** C1  
**Дата:** 2026-09-08  
**Правило:** сюда попадают только пробелы, которые **блокируют ответ энциклопедии**.  
Новое исследование игры **не начинать автоматически**. Закрывать при тестировании рабочей энциклопедии.

Формат записи:

```
QUESTION
→ WHY IT MATTERS
→ WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS
→ RESEARCH PRIORITY
```

Приоритеты:

| Код | Смысл |
|---|---|
| **P0** | Без этого v1 врёт игроку |
| **P1** | Нужно для полного ответа приоритетных разделов |
| **P2** | Улучшает точность; v1 может сказать «не закрыто» |
| **P3** | Внутренний хвост; игроку почти не нужен |
| **DO_NOT_RESEARCH** | Не открывать проход, пока энциклопедия не упрётся в живой вопрос |

Ниже **нет P0 из отсутствия документов `05`**. P0-разрыв C1 — интеграция, не код.

---

# GAPS FOUND DURING AUDIT

## GAP-01 — Живая проверка UI и Debug unlock

QUESTION  
Работает ли в этом билде цепочка GraphyCaller (11-й клик), точный состав вкладок debug-окна, сохраняемость опций и видимость Wiki burger так, как описано кодом?

WHY IT MATTERS  
Debug — приоритет v1. Код подтверждён; LIVE не выполнялся. Статья не должна писать «нажмите сюда» как LIVE_CONFIRMED.

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
Раздел 1: `debug-menu.md`, `windows-and-inspect.md`.  
Частично: NPC inspect / Mind tab.

RESEARCH PRIORITY  
**P1** — только LIVE-прогон уже описанного. Не искать новые debug-классы.

PARTIAL UPDATE (игрок, LIVE)  
Состав вкладок debug-окна закрыт: **Абсолютно всё / Отладочные стрелки / Карта / Курсор / Читы / Система**.  
Получен большой dump кнопок по вкладкам → `debug-menu.md`.  
**LIVE NEGATIVE:** UnlockAll*, IgnoreDamage, UltraFastSpawn, TestAds, Actor AI, Unit Info — нет во вкладках.  
Остаётся OPEN: вход в New Debug Window / DebugTool; глубокие эффекты «по имени»; burger ×11; сохраняемость опций.

---

## GAP-02 — Живая проверка редакторов (Traits / Subspecies)

QUESTION  
Совпадает ли ванильный Trait Editor / Subspecies editor с трассой prefab-событий и с эффектами, описанными в `05`?

WHY IT MATTERS  
Приоритетные разделы 2–4. Код есть; LIVE помечен в исследованиях.

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
`trait-editor.md`, `subspecies-player-control.md`, карточки «Как поставить черту / изменить подвид».

RESEARCH PRIORITY  
**P1** LIVE-валидация. Не расширять каталог неизвестных редакторов.

---

## GAP-03 — Полный каталог Decision id для игрока

QUESTION  
Какой полный список Decision / Job / Task видит игрок в UI, и какое человеческое имя у каждого?

WHY IT MATTERS  
NPC_CORE сознательно не каталогизировал все Decision. Для «почему NPC сделал X» достаточно pipeline + примеры. Полный справочник — отдельный объём.

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
Исчерпывающий указатель решений. **Не** блокирует статьи «как устроен AI» и «игрок не выбирает Decision».

RESEARCH PRIORITY  
**P2 / DO_NOT_RESEARCH** сейчас. Писать в v1: pipeline CONFIRMED, полный список имён — не интегрирован.

---

## GAP-04 — Housing, happiness, food consumption как отдельный контур

QUESTION  
Как жильё, счастье и фактическое потребление еды (не склад/армия-заглушка) ограничивают рост города с точки зрения игрока?

WHY IT MATTERS  
Исследования reproduction / mortality / jobs закрыли соседние контуры. `hasEnoughFoodForArmy()` = always true уже известен. Бытовой контур города в `04` остаётся PARTIAL (city life).

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
Сценарии «почему город не растёт», если ответ не reproduction/mortality/jobs/stockpile.

RESEARCH PRIORITY  
**P2**. v1 отвечает через уже известные гейты. Не начинать фазу Housing, пока карточка эксперимента не упрётся в стену.

---

## GAP-05 — Biomes: доступ игрока и полный эффект на юнита

QUESTION  
Какие ванильные инструменты меняют биом, и какой полный набор эффектов биома на Actor (включая random trait from biome)?

WHY IT MATTERS  
`04`: Biomes = MAP_ONLY. Powers знают семена биомов как Drop/GodPower id. Полного player-канона биомов нет.

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
Полная статья «биомы». Не блокирует terraform-кисти и disasters architecture.

RESEARCH PRIORITY  
**P2**. v1: семена/кисти из уже известных powers; не объявлять систему биомов CLOSED.

---

## GAP-06 — Boats / Docks standalone

QUESTION  
Что игрок может сделать с лодками и доками напрямую, помимо стыка Production/Buildings?

WHY IT MATTERS  
`04` явно NOT_CLOSED standalone. Не приоритет ТЗ v1.

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
Морские сценарии, торговля водой, «как построить флот».

RESEARCH PRIORITY  
**P2 / DO_NOT_RESEARCH** для v1.

---

## GAP-07 — Формулы характеристик (VQ-06)

QUESTION  
Точные формулы mass / stamina / XP / nutrition на Actor?

WHY IT MATTERS  
Слой `updateStats` (что мержится) CONFIRMED. Числовые формулы — открытый VQ-06 в `04`.

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
Статья «точные числа статов». Не блокирует «откуда статы берутся» (subspecies, traits, equipment, …).

RESEARCH PRIORITY  
**P2**. v1 описывает источники статов, не притворяется таблицей формул.

---

## GAP-08 — Onomastics algorithm (VQ-07)

QUESTION  
Как именно выбирается имя?

WHY IT MATTERS  
Архитектура имён есть в `09_NAMES_AND_ONOMASTICS`. Алгоритм не приоритет игрока v1.

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
«Почему юнит назван так».

RESEARCH PRIORITY  
**P3 / DO_NOT_RESEARCH** для v1.

---

## GAP-09 — War type `clash` (VQ-02)

QUESTION  
Зачем поле `clash` в `WarTypeLibrary`, если `init()` его не создаёт?

WHY IT MATTERS  
INTERNAL curiosity. На ванильный вход игрока не влияет.

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
Ничего в player-цепочке войны.

RESEARCH PRIORITY  
**P3 / DO_NOT_RESEARCH**.

---

## GAP-10 — Law readers / CursedSacrifice (VQ-04)

QUESTION  
Полный список читателей законов и роль CursedSacrifice?

WHY IT MATTERS  
Исполнение 49 законов CLOSED. Хвост не блокирует «где включить закон».

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
Исчерпывающий technical appendix законов.

RESEARCH PRIORITY  
**P2**.

---

## GAP-11 — Мод-поверхность сверх уже отделённого PowerBox

QUESTION  
Полный список кнопок всех модов копии (ModernBox, RulerBox, TPI, …) как справочник?

WHY IT MATTERS  
Для ванили достаточно правила: моды не ваниль; известные PowerBox army/convert/resources помечены. Полный каталог модов раздует энциклопедию.

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
Исчерпывающий мод-указатель. Не блокирует «это мод».

RESEARCH PRIORITY  
**P3 / DO_NOT_RESEARCH**. v1 держит известные MOD_ONLY и общее правило.

---

## GAP-12 — Полные ID Power / Disaster / Biome (RQ-03)

QUESTION  
Исчерпывающий список id?

WHY IT MATTERS  
Архитектура powers/disasters CLOSED; списки в `04` уже большие. «Каждая неизвестная катастрофа» не нужна для v1.

WHICH ENCYCLOPEDIA ANSWERS IT BLOCKS  
Полный реестр id. Не блокирует «как работает сила/катастрофа».

RESEARCH PRIORITY  
**P2 / DO_NOT_RESEARCH** пока карточка эксперимента не спросит конкретный отсутствующий id.

---

# НЕ ПРОБЕЛЫ (не открывать исследование)

Эти темы `04` ещё помечает как NOT_CLOSED / MAP_ONLY / ACTIVE. Для рабочей энциклопедии **знание уже лежит в `05`**. Нужна интеграция, не новый проход по коду:

- UI / доступ игрока
- Debug Menu
- War / Diplomacy / Alliances
- Army
- City capture
- Culture / Language / Religion / Books
- Clan / Family
- Succession / Leadership / Loyalty / Rebellion
- Citizen jobs player limits
- Watch towers / walls player limits
- NPC core / Possession / updateStats
- Species / Subspecies / Genetics / Birth / Reproduction / Mortality
- Plots / Rites player access
- Expeditions — **NEGATIVE_CANON**, системы нет

---

# КАК ПОЛЬЗОВАТЬСЯ ЭТИМ ФАЙЛОМ В C2

1. Если при сборке статьи не хватает факта из `04`+`05` — добавить GAP сюда, **не** идти в декомпил «на всякий случай».
2. Если факт есть в `05`, но не в WORKING — это задача интеграции, не GAP.
3. LIVE-прогоны (GAP-01, GAP-02) — отдельное решение, не часть аудита.

Счётчик на момент C1: **12 записанных GAP**, из них **0 P0 по отсутствию исследования**, **2 P1 LIVE**, остальные отложены.
