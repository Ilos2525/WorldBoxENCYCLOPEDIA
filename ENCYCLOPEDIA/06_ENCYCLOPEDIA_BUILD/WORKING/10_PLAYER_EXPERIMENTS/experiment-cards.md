# Карточки экспериментов v1

Все статусы ниже — по коду и UI-исследованиям. Живой прогон карты не делался: где важен клик в билде, пометка REQUIRES LIVE VALIDATION в связанных статьях.

---

## E01. Начать войну между двумя королевствами

**Можно ли?** Да (VANILLA)

**Способ:** Whisper of War

**Шаги:** noosphere → `whisper_of_war` → клик по двум сторонам.

**Что произойдёт:** `startWar` тип `whisper_of_war`; `isEnemy`; альянсы могут втянуться (`alliance_join`).

**Ограничения:** не мирный договор наоборот. Цель армии после этого выбирает AI.

**Альтернативы:** Spite (total war, не pair picker); force plot `new_war`; ждать AI.

**DEBUG / MOD:** не нужно.

---

## E02. Назначить конкретного NPC королём

**Можно ли?** Нет (VANILLA)

**Способ:** нет кнопки.

**Что произойдёт:** после смерти короля `SuccessionTool` берёт royal clan / fallback.

**Ограничения:** UI heir = прогноз.

**Альтернативы:** убить короля и править состав royal clan косвенно; force plots власти.

**DEBUG / MOD:** не выдавать мод-корону за ваниль.

---

## E03. Назначить NPC шахтёром

**Можно ли?** Нет напрямую (VANILLA)

**INTERNAL:** `City.setCitizenJob`.

**Альтернативы:** положить минералы + stockpile на зонах; ждать слот `miner`/`miner_deposit`. Не pickaxe «выдать руду складу» — pickaxe уничтожает месторождение без кредита.

**DEBUG:** фильтры CitizenJob*. **MOD:** EditResources не назначает job.

---

## E04. Приказать армии атаковать выбранный город

**Можно ли?** Нет (VANILLA)

**Что есть:** 1 Army/город; марш если война и ~70% заполнения; цель = ближайший reachable enemy.

**Оверлей `army_targets`:** визуал.

**MOD_ONLY:** PowerBox army tools.

---

## E05. Приказать юниту бить выбранную цель

**Можно ли?** Нет (VANILLA), кроме косвенного урона кистями

**AI:** ближайший враг в чанке sight 1; `peaceful` не ищет; `pacifist` всё равно дерётся.

**Possession:** игрок водит тело, это не combat-order меню.

---

## E06. Выдать madness через Trait Editor

**Можно ли?** Нет. `can_be_given = false`

**Способ:** destruction → `madness` (area r≈3) **Да**

**Снять:** `divine_light`. В редакторе remove тоже закрыт.

**Не путать:** rite `big_cast_madness` (случайный вражеский город, 80%, прогресс).

**Trait rain:** не обходит can_be_given.

---

## E07. Кнопка zombie_infection делает зомби

**Можно ли так думать?** Нет

**Факт:** капля даёт `infected` при `can_turn_into_zombie`. Trait `zombie` — spawn кнопки `zombie` (новый юнит) или transform после смерти заражённого.

---

## E08. Добавить золото городу пылью dust_gold

**Можно ли?** Нет

**Факт:** `forgetKingdomAndCity`. Склад смотреть в city_inventory без изменения кликом.

**DEBUG:** CityInfiniteResources. **MOD:** EditResources.

---

## E09. Поставить городскую сторожевую башню

**Можно ли?** Нет кистью watch_tower_*

**Город** строит сам (pop 30, hall, ресурсы). Игрок ставит flame/ice/angle/corrupted_brain — это **не** city defense + capture ticks.

Стены `wall_*` — block-тайлы, не city wall building.

---

## E10. Создать новый подвид того же вида

**Можно ли?** Да, косвенно

**Шаги:** spawn вида с `can_have_subspecies` дальше чем nearby (default 40 тайлов) от существующих members → `newSpecies`. Рядом → JOIN старому.

**Нельзя:** редактор Species; кнопка unit-окна «сменить подвид живущему».

**Editors подвида** меняют шаблон популяции, не ActorAsset.

---

## E11. Birth Traits меняют уже живущих

**Можно ли?** Нет

Контейнер не итерирует units. Для живущих: subspecies traits / genetics dirty / личный ActorTrait editor.

---

## E12. Открыть Debug и смотреть AI

**Можно ли?** Да (DEBUG), Mind last Decision — Да (VANILLA без debug)

**Шаги смотреть AI (DEBUG):**  
1. GraphyCaller ×11 → bug HUD → окно debug  
2. На **рамке** окна клик `NewDebugWindow` (не вкладки)  
3. Dropdown панели: **Actor AI** / **Unit Info** / **Actor Decisions** / **Actor Stats**  

Дополнительно на карте: стрелки + `OverlayCursorActor` + вкладка Курсор.  
**Last Decision** — ванильный Mind (debug не нужен).

**Не:** SonicSpeed за ваниль; Unlock не в save; `~` = лог.  
UnlockAll* / IgnoreDamage / UltraFastSpawn / TestAds — **DEAD UI** (кнопок нет). Actor AI не искать во вкладках.

---

## E13. Заключить мир между двумя выбранными королевствами

**Можно ли как Whisper?** Нет pair-peace

**Частично:** Friendship drop (выход из войны цели); plot stop_war если тип позволяет; выключить закон дипломатии (все войны); ждать симуляцию.

Unity **не** мирит.

---

## E14. Захватить город за игрока

**Можно ли напрямую передать kingdom?** Нет ванильной convert-кисти

**Частично:** начать войну → дождаться воинов на тайлах → ticks 100. Получатель может быть main войны, не ваша «армия».

**MOD_ONLY:** PowerBox convert city.

---

## E15. Почему NPC не размножается

**Частично диагностируется ванилью**

Проверить: законы babies; возраст breeding; nutrition; infertile; pregnant/afterglow; лимит offspring; private place / important person; sapience vs animal law.

Не CitizenJob. Не кнопка reproduce.

Жильё/счастье как полный ответ — OPEN/gap.

---

## E16. Possession vs обычный AI

**Да:** selected_unit → possession. Decision и ai.update выкл.

Не управление городом/армией.

---

## E17. Expeditions

**Можно ли?** Нет. **NEGATIVE CANON.** Системы нет.

---

## E18. Создать культуру / религию кистью

**VANILLA:** нет GodPower «new culture». Списки на noosphere = просмотр/editor.

Religion не создаётся при основании civ. Duplicate — **MOD_ONLY**.
