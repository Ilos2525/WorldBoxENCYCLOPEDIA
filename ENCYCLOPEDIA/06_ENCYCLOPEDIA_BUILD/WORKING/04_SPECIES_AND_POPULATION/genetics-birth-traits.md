# Генетика и Birth Traits

Три независимых контейнера на **одном** выбранном Subspecies.

## Subspecies Traits

Редактор `subspecies_trait_editor`. Пишет `saved_traits` подвида. Фильтры вида (`trait_filter_subspecies`) какие id нельзя.

Влияет на **живущих members** через dirty/`updateStats` (как культура на носителях), не копируется в ActorTrait HashSet.

## Birth Traits

Редактор `subspecies_birth_traits_editor`. Список ActorTrait **будущих** детей / шаблон.

При **создании** подвида в контейнер копируются стартовые `ActorAsset.traits`. Дальше редактор пишет только этот список.

**Не** итерирует живущих `subspecies.units`. Уже родившиеся не получают новые birth traits задним числом.

Не равно «черты, которые есть у матери сейчас».

## Genetics

Редактор `subspecies_genetics`. Геном `Nucleus` на подвиде.

`genesChangedEvent`: dirty/confuse + пересчёт **статов**. Фенотип существующих пересобирается только если индекс нелегален (`checkIfPhenotypeIsLegit`) — не «мгновенно все сменили внешность».

Личного генома у Actor нет. Смотреть гены одного NPC = смотреть **его подвид**.

Randomize / mutation seed — поля save подвида.

## Наследование при рождении (не editor)

`BabyMaker` читает подвид + родителей (`traitsInherit` / meta родителей). Это третий процесс: не birth-list целиком и не «все черты матери».

Player spawn не идёт через BabyMaker: miracle_born + nearby subspecies.

## Clone rain

Копия traits **родителя-клона**, плюс маркеры clone/fragile/miracle_born. Не birth template подвида.

## LIMITATIONS

Нет кнопки «сделать этого NPC генетическим исключением внутри подвида».  
Полный dump GeneAsset не делался — не нужен для модели уровней.

## RELATED SYSTEMS

[Редакторы UI](../01_INTERFACE_AND_CONTROL/editors.md) · [Размножение](reproduction-mortality.md)
