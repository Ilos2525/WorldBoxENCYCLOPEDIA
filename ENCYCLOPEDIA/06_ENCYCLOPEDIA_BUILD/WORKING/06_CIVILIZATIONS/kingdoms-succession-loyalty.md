# Королевства, наследство, лидеры, лояльность

## Король

**VANILLA:** нельзя кликом назначить конкретного NPC королём.

Король = `Kingdom.king` + profession King. Первый король — основатель civ.

После смерти: `KingdomBehCheckKing` → пауза `timer_new_king` → кандидат из **royal clan** (fallback иначе) → `setKing`. UI «heir» = `findNextHeir` = **прогноз**, не назначенный наследник.

Kingdom живёт без короля, пока есть города. Family поля succession **не** читает.

Shattered crown / chaos могут расколоть города в новые kingdom (симуляция после смены короны).

## Royal clan

`KingdomData.royal_clan_id`. `setKing` вызывает `trySetRoyalClan`. Overlay «клан короля» = `king.clan`, в интеррегнуме может не совпасть с royal_clan_id.

Игрок правит Clan traits редактором клана — это не «выбрать следующего короля», но меняет пул/статы членов.

## City leader

**Не король.** Король не становится city leader (`setLeader` отказывается). Столица может иметь отдельного лидера.

Живой лидер **не заменяется**, пока слот занят. Смерть/уход → `CityBehCheckLeader`. Пул: сначала royal clan по королевству, иначе любой клан; Family не читается.

Игрок не назначает лидера кнопкой.

## Loyalty

Слагаемые включают traits лояльности, mood, diplomacy/stewardship лидера (вычитаются), столица / new_conquest / культура vs столица. Игрок влияет косвенно: traits лидера, захват, культура.

Полная формула каждого слагаемого — в исследовании 19; v1: лояльность считает город, не ползунок игрока. Inspect `i_loyalty` — просмотр.

Низкая лояльность → путь к rebellion plot (не кнопка «восстань»). Inspiration drop — другой вход отделения.

## VANILLA влияние

Убить короля / лидера; force plot; сменить clan/culture traits; война и захват; законы.

## MOD_ONLY

Не описывать мод-корону как ваниль.

## RELATED SYSTEMS

[Клан](../07_META_SYSTEMS/meta-civilization.md) · [Войны и мятеж](../08_POLITICS_AND_CONFLICT/wars-armies-capture.md)
