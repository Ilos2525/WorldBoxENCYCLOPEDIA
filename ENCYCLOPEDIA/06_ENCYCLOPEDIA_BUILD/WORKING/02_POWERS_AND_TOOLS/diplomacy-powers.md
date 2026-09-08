# Дипломатические силы

**Уровень:** VANILLA, вкладка **noosphere**.  
Это не RTS-дипломатия с договором. Каждая кнопка делает **разное**.

`relations` — **VIEW**, не запись отношения.

## Whisper of War

| | |
|---|---|
| Игрок | выбирает **две** стороны (A и B) |
| Код | `startWar` тип `whisper_of_war` |
| Альянсы | `alliance_join` = да: в войну тянутся члены альянсов |
| Конец plot `attacker_stop_war` | да (`can_end_with_plot`) |

**VANILLA DIRECT.** Главный способ «натравить два королевства».

## Spite

Drop на цель → `eventSpite` → тип `spite`: **total war**, `forced_war`, атакующий выходит из альянса. Plot stop_war **не** может закончить spite.

Игрок не picking пары как Whisper; цель выбирается каплей.

## Inspiration

Drop → `City.useInspire` → новое kingdom + War тип `inspire` (флаг rebellion). Не захват города ticks. Отделение, затем война old vs new.

## Friendship

Drop на цель → leaveWar / Peace для связанной войны. **Не** объект «дружба» и **не** парный picker мира как у Whisper.

Нет ванильной кнопки «выбрать королевство A и B и заключить мир».

При альянсе Friendship может снять с войны **членов той же** войны (см. alliances research).

## Unity

Два клика по kingdom → `forceAlliance` тип **Forced**, минуя opinion `canJoin`. Нельзя если уже `isEnemy`. Не гасит текущую войну само (в отличие от PowerBox create alliance).

Если у сторон разные альянсы — A сначала leave, потом merge.

## Discord

Drop на город → `alliance.leave` этого kingdom. Если остался 1 член — dissolve. Если ушедший был main войны — остаток альянса тоже leave **этой** войны.

## Законы

Выключение дипломатии (`world_law_diplomacy`) режет AI-plots с `requires_diplomacy` и вызывает `stopAllWars()`. Сам `startWar` из сил **законы не читает**.

## WHAT AI / SIMULATION DECIDES

После появления `War`: `Kingdom.isEnemy` ⇔ активная война. Армии маршируют, если набраны; бой и захват — отдельные системы. Opinion пересчитывается при чтении (`opinion_in_war` −500).

## MOD_ONLY

PowerBox `powerbox_create_alliance` мирит пару перед союзом. Ванильный Unity этого не делает.

## RELATED SYSTEMS

[Войны и армии](../08_POLITICS_AND_CONFLICT/wars-armies-capture.md) · [Дипломатия и союзы](../08_POLITICS_AND_CONFLICT/diplomacy-alliances.md)
