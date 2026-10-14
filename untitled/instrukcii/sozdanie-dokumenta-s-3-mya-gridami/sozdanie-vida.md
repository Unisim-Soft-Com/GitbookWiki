# Создание вида

## 2.1 Создание вида (вариант № 1)

{% stepper %}
{% step %}
### Создание первого вида

Так как напрямую с таблицами не работают, создадим вид (View). Для этого перейдем в список Views и нажмем на

![](<../../.gitbook/assets/image (957)>)

для создания нового вида (View).

![](<../../.gitbook/assets/image (958)>)

Напротив поля для имени запишем имя вида (View).

![](<../../.gitbook/assets/image (959)>)

На вкладке Source пишем скрипт, который выберет все колонки из таблицы `YVEINE_TMDB_INTAKE_LIST_A`. После чего нажимаем OK.

![](<../../.gitbook/assets/image (960)>)

![](<../../.gitbook/assets/image (961)>)

В результате появится созданный вид.

![](<../../.gitbook/assets/image (962)>)
{% endstep %}

{% step %}
### Создание второго вида

Нажимаем на создание нового вида и задаем имя для второго вида.

![](<../../.gitbook/assets/image (963)>)

![](<../../.gitbook/assets/image (964)>)

На вкладке Source записываем скрипт, который выберет все колонки из таблицы `YVEINE_TMDB_INTAKE_LIST_B`, затем нажимаем OK.

![](<../../.gitbook/assets/image (965)>)

![](<../../.gitbook/assets/image (966)>)

![](<../../.gitbook/assets/image (967)>)
{% endstep %}

{% step %}
### Создание третьего вида

Для создания третьего вида повторяем те же шаги: создаём новый вид, указываем имя, на вкладке Source пишем выбор всех колонок из таблицы `YVEINE_TMDB_INTAKE_LIST_C` и подтверждаем OK.

![](<../../.gitbook/assets/image (726)>)

![](<../../.gitbook/assets/image (727)>)

![](<../../.gitbook/assets/image (728)>)

![](<../../.gitbook/assets/image (729)>)

![](<../../.gitbook/assets/image (730)>)
{% endstep %}
{% endstepper %}

После создания видов нажимаем "Refresh all objects" для появления созданных Views, затем завершаем транзакцию с сохранением нажатием Commit.

![](<../../.gitbook/assets/image (731)>)

![](<../../.gitbook/assets/image (732)>)

![](<../../.gitbook/assets/image (733)>)

***

## 2.2 Создание вида (вариант № 2)

{% stepper %}
{% step %}
### Быстрое создание вида через редактор

Перейдем в редактор.

![](<../../.gitbook/assets/image (734)>)

Напишем скрипт создания вида:

CREATE VIEW ... SELECT \* FROM YVEINE\_TMDB\_INTAKE\_LIST\_A

Для запуска используем горячие клавиши Ctrl+Enter.

![](<../../.gitbook/assets/image (735)>)

![](<../../.gitbook/assets/image (736)>)
{% endstep %}

{% step %}
### Создание второго и третьего вида через редактор

Аналогично: пишем и выполняем скрипты создания видов для таблиц `YVEINE_TMDB_INTAKE_LIST_B` и `YVEINE_TMDB_INTAKE_LIST_C`, выполняя каждый скрипт через Ctrl+Enter.

![](<../../.gitbook/assets/image (737)>)

![](<../../.gitbook/assets/image (738)>)
{% endstep %}
{% endstepper %}

После этого откройте Views и с помощью поиска найдите созданные виды.

![](<../../.gitbook/assets/image (739)>)

![](<../../.gitbook/assets/image (740)>)

***

## 2.3 Добавление дополнительных колонок в вид

Тип данных у всех колонок (кроме `DATA`) — Data Type `NUMBER(10)`. Это означает, что данные из справочников будут в виде цифрового кода, так как колонка `COD` в справочнике `TMS_UNIVERS` имеет такой же тип. Поэтому необходимо создать новые колонки с другим типом данных (например, текстовые вычисляемые колонки), в которых будут отображаться значения из справочника.

{% stepper %}
{% step %}
### Копируем скрипт в редактор

Переходим на вкладку Script и копируем его в редактор с помощью кнопки Edit.

![](<../../.gitbook/assets/image (741)>)

![](<../../.gitbook/assets/image (742)>)
{% endstep %}

{% step %}
### Добавляем вычисляемую колонку для первого вида

Добавляем вычисляемую (CLC) текстовую (T) колонку `CLCDISHT` и записываем к ней подзапрос:

SELECT DENUMIREA FROM TMS\_UNIVERS WHERE COD = A.DISH

Для выполнения используем Ctrl+Enter.

![](<../../.gitbook/assets/image (743)>)

В результате появится дополнительная колонка `CLCDISHT`.

![](<../../.gitbook/assets/image (744)>)
{% endstep %}

{% step %}
### Добавляем вычисляемые колонки для второго вида

Для второго вида повторяем процесс: копируем скрипт в редактор, добавляем вычисляемую (CLC) текстовую (T) колонку `CLCPRODUCTT` с подзапросом:

SELECT DENUMIREA FROM TMS\_UNIVERS WHERE COD = A.PRODUCT

Выполняем Ctrl+Enter.

![](<../../.gitbook/assets/image (745)>)

![](<../../.gitbook/assets/image (746)>)

![](<../../.gitbook/assets/image (747)>)

![](<../../.gitbook/assets/image (748)>)

После выполнения появится колонка `CLCPRODUCTT`.

![](<../../.gitbook/assets/image (749)>)
{% endstep %}

{% step %}
### Добавляем вычисляемые колонки для третьего вида

Для третьего вида также копируем скрипт, добавляем вычисляемую (CLC) текстовую (T) колонку `CLCPRODUCTT` с тем же подзапросом:

SELECT DENUMIREA FROM TMS\_UNIVERS WHERE COD = A.PRODUCT

Выполняем Ctrl+Enter.

![](<../../.gitbook/assets/image (750)>)

![](<../../.gitbook/assets/image (751)>)

![](<../../.gitbook/assets/image (752)>)

Появится колонка `CLCPRODUCTT`.
{% endstep %}
{% endstepper %}

После всех изменений сохраните транзакцию с помощью Commit.

![](<../../.gitbook/assets/image (753)>)

![](<../../.gitbook/assets/image (754)>)
