# Размножение, рост, смертность

**Уровень роста:** AI Decision, не кнопка «размножиться» и не CitizenJob.

## VANILLA — чем игрок влияет на рост

- World Laws: `world_law_civ_babies` / `world_law_animals_babies`
- Traits: `infertile` и статы `offspring` (editor / гены подвида)
- Еда/nutrition на карте (косвенно); порог `nutrition_cost_new_baby` = 50 если `needsFood()`
- Не спамить spawn: естественный birth — другой слой
- Изоляция подвида / birth traits — шаблон детей

Игрок **не** выбирает партнёра и не запускает `makeBaby` кликом (кроме косвенно: законы, traits, безопасность города).

## Конвейер birth — CONFIRMED

```
Decision reproduction (нейросеть)
  → BehCheckReproductionBasics
  → стратегия подвида (sexual / asexual / …)
  → Egg / Pregnancy / Immediate
  → BabyMaker.makeBaby
```

Стоп-фильтр: закон babies, `canBreed`, возраст `age_breeding` подвида, лимит детей, nutrition, не pregnant/afterglow, important person **или** private place.

Sapient с lifespan > 30: adult 16, breeding **18** (cap). Иначе формула от lifespan.

Sexual vs asexual — SubspeciesTrait strategy. Детали партнёра не разворачивать сверх research: AI ищет lover / один родитель.

Жильё как лимит birth в city life — PARTIAL / gap Housing; v1 не выдумывает полный контур домов.

## Смертность

Единый сток: `getHit` → HP≤0 → `die`.

Симуляция: старость (`world_law_old_age`), голод (закон starvation, nutrition=0), бой, огонь, вода, чума, инфекция, утопление…

Игрок: кисти урона, plague/madness/infection, бомбы. `IgnoreDamage` — DEBUG.

`immortal` режет natural death, не все AttackType.

Death callbacks (nuke on death) — traits phase 5; не «кнопка смерти в редакторе».

## Clone vs birth vs spawn

| Путь | Родители | miracle_born | Birth template |
|---|---|---|---|
| Естественный ребёнок | да | нет (кроме divine reproduction → miracle_bearer на родителе) | да |
| Player spawn | нет | да | нет; JOIN nearby subspecies |
| clone_rain | визуальный «родитель» | да + clone + fragile | нет |

## LONG-TERM

Выключенные babies + включённая старость → убыль. Спавн игрока обходит естественный фильтр, но засоряет miracle_born. Новый подвид в изоляции размножается в **своём** шаблоне.

## RELATED SYSTEMS

[Законы мира](../09_WORLD_SIMULATION/world-laws-ages.md) · [Инфекции](../02_POWERS_AND_TOOLS/destruction-infections.md)
