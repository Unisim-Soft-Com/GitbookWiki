# Создание триггеров

Для использования последовательности создадим для каждой таблицы триггер. Для этого перейдем в списке на вкладку _Triggers_.

![](<../../.gitbook/assets/image (919)>)

{% stepper %}
{% step %}
### Создание первого триггера

Нажимаем кнопку создания нового триггера.

![](<../../.gitbook/assets/image (920)>)

В поле имени записываем имя триггера: `YVEINE_TMDB_INTAKE_LIST_A_TRG`.

![](<../../.gitbook/assets/image (921)>)

С помощью многоточия выбираем таблицу для данного триггера — `YVEINE_TMDB_INTAKE_LIST_A`, затем подтверждаем выбор.

![](<../../.gitbook/assets/image (922)>)

![](<../../.gitbook/assets/image (923)>)

Устанавливаем галочку напротив `Insert` (триггер будет срабатываться Before Insert).

![](<../../.gitbook/assets/image (924)>)

Перейдём на вкладку "Body" и запишем PL/SQL блок. Комментарий и PL/SQL блок на скриншотах показывают логику: если колонка `NRDOC1` пустая, то ей присваивается следующее значение последовательности.

![](<../../.gitbook/assets/image (925)>)

![](<../../.gitbook/assets/image (926)>)

После внесения тела триггера нажимаем OK для сохранения — триггер будет создан.

![](<../../.gitbook/assets/image (927)>)

Для появления созданного триггера в списке нажмите "Refresh all objects".

![](<../../.gitbook/assets/image (928)>)

В списке _Triggers_ появится `YVEINE_TMDB_INTAKE_LIST_A_TRG`. На вкладке "Source" будет сохранён PL/SQL блок.

![](<../../.gitbook/assets/image (929)>)

Проверить PL/SQL блок можно на вкладке "Source".

![](<../../.gitbook/assets/image (930)>)

При необходимости вкладка "Errors" покажет ошибки.

![](<../../.gitbook/assets/image (931)>)

![](<../../.gitbook/assets/image (932)>)
{% endstep %}

{% step %}
### Создание второго триггера

Нажимаем создание нового узла/триггера.

![](<../../.gitbook/assets/image (933)>)

В поле имени записываем `YVEINE_TMDB_INTAKE_LIST_B_TRG`.

![](<../../.gitbook/assets/image (934)>)

С помощью многоточия выбираем таблицу `YVEINE_TMDB_INTAKE_LIST_B`.

![](<../../.gitbook/assets/image (935)>)

Устанавливаем галочку `Insert` (Before Insert).

![](<../../.gitbook/assets/image (936)>)

Перейдём на вкладку "Body" и запишем PL/SQL блок, аналогичный первому, но для колонки `NRDOC2`.

![](<../../.gitbook/assets/image (937)>)

![](<../../.gitbook/assets/image (938)>)

Нажимаем OK для сохранения триггера.

![](<../../.gitbook/assets/image (939)>)

Обновляем список объектов ("Refresh all objects") чтобы увидеть новый триггер в списке.

![](<../../.gitbook/assets/image (940)>)

В списке появится `YVEINE_TMDB_INTAKE_LIST_B_TRG`. На вкладке "Source" будет PL/SQL блок для `NRDOC2`.

![](<../../.gitbook/assets/image (941)>)

![](<../../.gitbook/assets/image (942)>)
{% endstep %}

{% step %}
### Создание третьего триггера

Нажимаем создание нового триггера.

![](<../../.gitbook/assets/image (943)>)

В поле имени записываем `YVEINE_TMDB_INTAKE_LIST_C_TRG`.

![](<../../.gitbook/assets/image (944)>)

Выбираем таблицу `YVEINE_TMDB_INTAKE_LIST_C` и подтверждаем выбор.

![](<../../.gitbook/assets/image (945)>)

![](<../../.gitbook/assets/image (946)>)

Перейдём на вкладку "Body" и запишем PL/SQL блок, аналогичный предыдущим, но для колонки `NRDOC3`.

![](<../../.gitbook/assets/image (947)>)

![](<../../.gitbook/assets/image (948)>)

Сохраняем триггер нажатием OK.

![](<../../.gitbook/assets/image (949)>)

Обновляем список объектов ("Refresh all objects") чтобы увидеть `YVEINE_TMDB_INTAKE_LIST_C_TRG`.

![](<../../.gitbook/assets/image (950)>)

![](<../../.gitbook/assets/image (951)>)

Готовые соответствия:

* Триггер `YVEINE_TMDB_INTAKE_LIST_A_TRG` — колонка `NRDOC1`. ![](<../../.gitbook/assets/image (952)>)
* Триггер `YVEINE_TMDB_INTAKE_LIST_B_TRG` — колонка `NRDOC2`. ![](<../../.gitbook/assets/image (953)>)
* Триггер `YVEINE_TMDB_INTAKE_LIST_C_TRG` — колонка `NRDOC3`. ![](<../../.gitbook/assets/image (954)>)
{% endstep %}

{% step %}
### Завершение — сохранение транзакции

Для завершения текущей транзакции с сохранением нажмите кнопку "Commit".

![](<../../.gitbook/assets/image (955)>)

![](<../../.gitbook/assets/image (956)>)
{% endstep %}
{% endstepper %}
