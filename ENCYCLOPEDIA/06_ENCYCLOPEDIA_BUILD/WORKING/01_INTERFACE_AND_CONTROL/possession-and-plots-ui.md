# Possession и Plots в интерфейсе

Два разных инструмента на вкладке выбранного юнита. Не путать с кистью `madness` и с просмотром списка plots на noosphere.

---

## Possession

**Уровень:** VANILLA (кнопка + хоткей `control_unit`).

### WHAT PLAYER CAN DO

Временно водить **одного** NPC: статус `possessed`, обычный AI Decision + `ai.update` **выключены**.

### WHERE TO FIND IT

- `selected_unit` → `unit_possession` → `ButtonEvent.clickPossess` **CONFIRMED**
- хоткей possession (`HotkeyLibrary.control_unit`)

Spectate (`unit_spectate`) — слежение, не управление AI.

### WHAT HAPPENS AFTER THE ACTION

```
PLAYER possess
  → status possessed
  → ControllableUnit: игрок задаёт движение
  → кадр Actor: нет makeDecisionFor, нет ai.update
```

Снятие статуса — снова автономный AI.

### WHAT AI / SIMULATION DECIDES

Пока possessed — **ничего** из Decision/Job/Task. Боевой поиск врагов у possessed связан с отдельными правилами aggro (см. бой). Magnet (`magnet` на other) — другой статус (`magnetized`), цель не атакуема.

### LIMITATIONS

- Это не «приказ всему городу».
- Не замена редактора черт и не смена профессии.
- Долгосрочно NPC остаётся тем же Actor; после выхода AI читает текущие traits/войну/голод как обычно.

---

## Plots в UI

**Уровень:** VANILLA. Три разных власти.

| UI | Где | Власть |
|---|---|---|
| Plots editor | selected_unit → `unit_plots` → вкладка Plots | **force-start** Plot на этом NPC |
| Список | noosphere → `plots_list` → `list_plots` | **VIEW** живых заговоров |
| Карточка | окно `plot` | **VIEW** прогресса; побочно unlock ассета |

God Power «запустить plot» **нет**. `PlayerControl` не вызывает `tryStartPlot`.

### WHAT HAPPENS AFTER FORCE-START

`PlotsEditor.addAugmentation` → `PlotManager.tryStartPlot(..., pForced=true)`.

Для force полный `checkIsPossible` (деньги, уровень, законы) **не** обязателен — короткий `check_can_be_forced`. Продолжение и `action` всё равно считает симуляция (религия, вражеский город, прогресс…).

Пример rite `big_cast_madness`: цель — жители **случайного вражеского города**, не кисть игрока; 80% `addTrait("madness")` при завершении. Без религии plot сорвётся на continue. Кисть Destruction `madness` — **другой** вход (сразу area).

### WHAT AI / SIMULATION DECIDES

Без редактора: Decision `try_new_plot` → `BehTryNewPlot` → полный `checkIsPossible`. Rites религии попадают в AI-пул только при `world_law_rites` и ReligionTrait с `plot_id`.

Редактор показывает PlotAsset с `show_in_meta_editor` (обычно все), не только пул религии.

### LIMITATIONS

- Игрок выбирает **тип** plot и **автора**. Цель города/партнёра часто выбирает код.
- Список plots не даёт «отменить войну кликом по строке».
- Канон 28 id: симуляция в `04` `plots.md`; здесь — доступ игрока.

**INTERNAL:** AI сам стартует plots.  
**MOD_ONLY:** не требуется для force-start ванилью.

## RELATED SYSTEMS

[NPC AI](../03_NPC_AND_AI/ai-pipeline.md) · [Войны](../08_POLITICS_AND_CONFLICT/wars-armies-capture.md) · [Кисть madness](../02_POWERS_AND_TOOLS/destruction-infections.md)
