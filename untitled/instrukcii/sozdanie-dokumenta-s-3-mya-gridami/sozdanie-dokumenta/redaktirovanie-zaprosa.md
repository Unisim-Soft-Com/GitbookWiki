# Редактирование запроса

{% stepper %}
{% step %}
### Редактирование запроса Grid №1

1. Находясь в поле **Grid № 1**, откройте окно изменения запроса — горячие клавиши **Alt+Q**.

![](<../../../.gitbook/assets/image (667)>)

2. Перейдите на вкладку свойств и в поле `View` укажите: `YVEINE_VMDB_INTAKE_LIST_A`.

![](<../../../.gitbook/assets/image (668)>)

* В фильтре на выборку запишите: `RDDOC=:COD`
* В порядке сортировки укажите колонку: `NRDOC1`
* Список ключевых полей для обновления: `NRDOC` и `NRDOC1`

![](<../../../.gitbook/assets/image (669)>)

3. Перейдите на вкладку SQL Generator и по шагам получите SQL:

* Нажмите Get Tables

![](<../../../.gitbook/assets/image (670)>)

![](<../../../.gitbook/assets/image (671)>)

* Получите таблицу

![](<../../../.gitbook/assets/image (672)>)

* Нажмите Get Table Fields для получения табличных полей

![](<../../../.gitbook/assets/image (673)>)

![](<../../../.gitbook/assets/image (674)>)

* Нажмите Generate SQL для генерации SQL-запроса

![](<../../../.gitbook/assets/image (675)>)

![](<../../../.gitbook/assets/image (676)>)

4. Сгенерированные SQL-примеры:

* Запрос для добавления записей (Insert)

![](<../../../.gitbook/assets/image (677)>)

* Примеры изменения (Update)

![](<../../../.gitbook/assets/image (678)>)

* Примеры удаления (Delete)

![](<../../../.gitbook/assets/image (679)>)

* Обновления / Refresh

![](<../../../.gitbook/assets/image (680)>)

5. На вкладке SQL сгенерирован SELECT-запрос для вида `YVEINE_VMDB_INTAKE_LIST_A` с фильтром `NRDOC =: COD` и сортировкой по `NRDOC1`.

![](<../../../.gitbook/assets/image (681)>)

6. Чтобы сохранить изменения при выходе:

* Поставьте галочку напротив "Save on exit"

![](<../../../.gitbook/assets/image (682)>)

* Нажмите OK

![](<../../../.gitbook/assets/image (683)>)

В результате все изменения будут сохранены при выходе.

![](<../../../.gitbook/assets/image (684)>)
{% endstep %}

{% step %}
### Редактирование запроса Grid №2

1. Откройте окно изменения запроса для **Grid № 2** (Alt+Q).

![](<../../../.gitbook/assets/image (685)>)

2. В поле `View` укажите: `YVEINE_VMDB_INTAKE_LIST_B`.

* Фильтр на выборку: `NRDOC=:NRDOC AND NRDOC1=:NRDOC1`
* Порядок сортировки: `NRDOC2`
* Список ключевых полей для обновления: `NRDOC;NRDOC1;NRDOC2`

![](<../../../.gitbook/assets/image (686)>)

3. На вкладке SQL Generator выполните те же шаги:

* Get Tables

![](<../../../.gitbook/assets/image (687)>)

![](<../../../.gitbook/assets/image (688)>)

![](<../../../.gitbook/assets/image (689)>)

* Get Table Fields

![](<../../../.gitbook/assets/image (690)>)

![](<../../../.gitbook/assets/image (691)>)

* Generate SQL

![](<../../../.gitbook/assets/image (692)>)

![](<../../../.gitbook/assets/image (693)>)

4. Результаты:

* Insert

![](<../../../.gitbook/assets/image (694)>)

![](<../../../.gitbook/assets/image (695)>)

* Update

![](<../../../.gitbook/assets/image (696)>)

![](<../../../.gitbook/assets/image (697)>)

* Delete

![](<../../../.gitbook/assets/image (698)>)

![](<../../../.gitbook/assets/image (699)>)

* Refresh

![](<../../../.gitbook/assets/image (700)>)

5. Сохранение изменений:

* Поставьте галочку "Save on exit"

![](<../../../.gitbook/assets/image (701)>)

* Нажмите OK

![](<../../../.gitbook/assets/image (702)>)

![](<../../../.gitbook/assets/image (703)>)
{% endstep %}

{% step %}
### Редактирование запроса Grid №3

1. Откройте окно изменения запроса для **Grid № 3** (Alt+Q).

![](<../../../.gitbook/assets/image (704)>)

2. В поле `View` укажите: `YVEINE_VMDB_INTAKE_LIST_C`.

* Фильтр на выборку: `NRDOC=:NRDOC AND NRDOC1=:NRDOC1 AND NRDOC2=:NRDOC2`
* Порядок сортировки: `NRDOC3`
* Список ключевых полей для обновления: `NRDOC;NRDOC1;NRDOC2;NRDOC3`

![](<../../../.gitbook/assets/image (705)>)

3. На вкладке SQL Generator:

* Get Tables

![](<../../../.gitbook/assets/image (706)>)

![](<../../../.gitbook/assets/image (707)>)

![](<../../../.gitbook/assets/image (708)>)

* Get Table Fields

![](<../../../.gitbook/assets/image (709)>)

![](<../../../.gitbook/assets/image (710)>)

* Generate SQL

![](<../../../.gitbook/assets/image (711)>)

![](<../../../.gitbook/assets/image (712)>)

4. Результаты:

* Insert

![](<../../../.gitbook/assets/image (713)>)

![](<../../../.gitbook/assets/image (714)>)

* Update

![](<../../../.gitbook/assets/image (715)>)

![](<../../../.gitbook/assets/image (716)>)

* Delete

![](<../../../.gitbook/assets/image (717)>)

![](<../../../.gitbook/assets/image (718)>)

* Refresh

![](<../../../.gitbook/assets/image (719)>)

![](<../../../.gitbook/assets/image (720)>)

5. На вкладке SQL появился SELECT-запрос, выбирающий поля из вида `YVEINE_VMDB_INTAKE_LIST_C` с фильтром `NRDOC=:NRDOC AND NRDOC1=:NRDOC1 AND NRDOC2=:NRDOC2`, сортировка по `NRDOC3`.

![](<../../../.gitbook/assets/image (721)>)

6. Сохранение изменений:

* Отметьте "Save on exit" и нажмите OK.

![](<../../../.gitbook/assets/image (701)>)

![](<../../../.gitbook/assets/image (702)>)
{% endstep %}
{% endstepper %}
