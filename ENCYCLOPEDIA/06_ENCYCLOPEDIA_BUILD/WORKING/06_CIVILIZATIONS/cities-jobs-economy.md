# Город, работы, экономика

Три слоя, которые путают чаще всего:

| Слой | Примеры | Кто назначает |
|---|---|---|
| UnitProfession | Unit, Warrior, King, Leader | город / succession |
| CitizenJob | miner, farmer, builder, attacker… | слоты города |
| Decision/task | make_items, put_out_fire, find_house | нейросеть, не слот job |

## VANILLA — что игрок может

| Действие | Инструмент | Эффект |
|---|---|---|
| Больше деревьев/кустов на зонах | удобрения, семена | слоты woodcutter/gatherer **если есть stockpile** |
| Минералы на зонах | nature ores | miner_deposit |
| Срубить дерево **в городе** | creation `axe` | wood **сразу в склад** |
| Уничтожить месторождение | `pickaxe` | destroy **без** выдачи городу |
| Скосить / снести | sickle, demolish, бомбы | минус слоты и здания |
| Добавить людей | spawn civ | больше adults → больше слотов (в т.ч. воинов) |
| Закон армии | world laws | слоты `attacker` |
| Смотреть склад | city_inventory | tooltip, клик не меняет число |

**Нет кнопки:** назначить miner этому NPC; выдать золото складу; вручную поставить stockpile/mine/ветряк civ; выбрать клетку стройки города.

Без склада gatherers **не открываются**.

`dust_gold` ≠ золото. Юниты забывают kingdom и city.

Рецепты вида (хлеб и т.д.) в production есть; отдельной baker CitizenJob нет.

`hasEnoughFoodForArmy()` в коде **всегда true**. Реальный food-gate армии — другие ветки tasks (PARTIALLY CONFIRMED смысл еды).

## INTERNAL

```
CityBehCheckCitizenTasks → слоты
BehCityActorFindNewJob → setCitizenJob
  попытка Warrior (gold>10, закон армии, adults>15, таймер…)
  builder приоритет
  если еды 0 — gatherers
  round-robin
```

King/leader не идут в farmer/miner. `attacker` переводит в Warrior, не «добыча».

## DEBUG

CityInfiniteResources, FastConstruction, DrawCitizenJobIcons, CitizenJob* фильтры.

## MOD_ONLY

PowerBox EditResources.

## WHAT AI DECIDES

Кто какой работой занят, куда строить, когда ветряк появится (farmer требует ветряк).

## RELATED SYSTEMS

[Кисти](../02_POWERS_AND_TOOLS/terraform-brushes.md) · [Армии](../08_POLITICS_AND_CONFLICT/wars-armies-capture.md)
