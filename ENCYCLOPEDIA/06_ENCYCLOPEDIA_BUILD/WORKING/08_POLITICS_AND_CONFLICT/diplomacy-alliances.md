# Дипломатия и союзы

Три слоя — не одно «отношение»:

| Слой | Что сохраняется |
|---|---|
| DiplomacyRelation | пара kingdom + `timestamp_last_war_ended` |
| Opinion | **считается при чтении**, не сейв; порог good = total ≥ 0 |
| Alliance | членство, тип Normal или Forced |
| War | вражда civ↔civ |
| Friendship drop | выход из войны, не статус дружбы |

Enum `DiplomacyState` нигде не читается. Мёртвый.

## VANILLA — силы

См. [дипломатические силы](../02_POWERS_AND_TOOLS/diplomacy-powers.md). Кратко:

- **Unity:** два kingdom → Forced alliance, минуя opinion; не если isEnemy; войну само не гасит
- **Discord:** leave альянса
- **Plots** alliance_create/join/destroy на короле: force-start, партнёра часто выбирает код
- AI Normal alliance — INTERNAL
- `relations` — VIEW

Opinion слагаемые (примеры): in_war −500, truce +100 ≤5 лет, alliance +30, same wars +50. Игрок редко пишет opinion напрямую — он меняет War/Alliance/культуру, сумма пересчитывается.

## WHAT AI DECIDES

`getWarTarget` только если opinion **не** good. Alliance join читает good. Unity opinion не читает.

`DiplomacyManager` тик ~2с считает supreme ranking, не «объявить войну».

## MOD_ONLY

PowerBox create alliance может сначала помирить. Ваниль Unity — нет.

## RELATED SYSTEMS

[Войны](wars-armies-capture.md)
