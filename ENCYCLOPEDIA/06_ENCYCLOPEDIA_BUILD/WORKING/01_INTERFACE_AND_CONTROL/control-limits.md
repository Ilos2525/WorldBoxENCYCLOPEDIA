# Границы прямого контроля

**Главный ответ раздела:** интерфейс WorldBox даёт силы бога и редакторы объектов, а не RTS-приказы.

## VANILLA — игрок может

- Менять рельеф, спавнить, капать статусы и часть traits
- Inspect и редактировать **одного** NPC (черты с `can_be_given`, экип)
- Редактировать meta: подвид, культура, законы мира
- Force-start Plot на выбранном NPC
- Possession одного юнита
- Дипломатические силы: Whisper (две стороны), Unity (два kingdom), Discord, Spite, Inspiration, Friendship — каждая со своей семантикой
- Включать/выключать World Laws (окно с main)

## VANILLA — игрок не может (подтверждено исследованиями)

| Намерение | Что есть вместо этого |
|---|---|
| Назначить этого NPC шахтёром / фермером | CitizenJob ставит городской AI |
| Выбрать короля | SuccessionTool / royal clan; UI «heir» = прогноз |
| Назначить city leader, пока слот занят | смена только когда лидер исчез |
| Приказать армии атаковать выбранный город | цель = ближайший reachable enemy city |
| Приказать юниту бить выбранную цель | `attack_target` ищет AI |
| Парный «заключить мир между A и B» как Whisper | Friendship — drop на цель, выход из войны; нет pair-peace picker |
| Поставить городскую watch tower | город строит сам; игрок ставит другие tower-drops |
| Выдать золото складу города пылью | `dust_gold` = забыть kingdom/city |
| Построить stockpile / mine кликом «поставь здание civ» | нет; только симуляция города или разрушение/терраформ |
| Править ActorAsset (вид целиком) | нет редактора Species |
| Пересадить живущего NPC в другой подвид кнопкой unit-окна | unit/subspecies окна `setSubspecies` для пересадки не вызывают |

## Просмотр vs действие

| Выглядит как контроль | На деле |
|---|---|
| `wars_list`, `armies_list`, `army_targets` | список / оверлей |
| `relations` | просмотр |
| Mind tab | last Decision, не приказ |
| Favorite | флаг сортировок, не AI-король |
| Слой культуры/религии | покраска карты |

## DEBUG

После unlock можно ломать симуляцию (SonicSpeed, Infinite Resources, IgnoreDamage) и **смотреть** Job/Task. Это не ванильный способ «играть за короля».

## INTERNAL

City/Kingdom behaviour ticks, набор воинов, выбор лидера, Decision loop.

## MOD_ONLY

PowerBox: создать/наполнить армию, convert city, EditResources — обходят ванильные границы. Не описывать как стандарт.

## LONG-TERM EFFECTS

Игрок задаёт **условия** (война, traits, еда на карте, законы). Дальше население, работы, войны и захват считает симуляция. Исключение кадров: Possession.

## RELATED SYSTEMS

[Что игрок может у NPC](../03_NPC_AND_AI/player-can-cannot.md) · [Эксперименты](../10_PLAYER_EXPERIMENTS/README.md)
