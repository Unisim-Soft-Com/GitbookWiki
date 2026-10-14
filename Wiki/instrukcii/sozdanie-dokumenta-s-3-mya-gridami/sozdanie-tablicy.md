# Создание таблицы

В качестве примера возьмем вымышленный объект Кафе-бар " _Veine_". Наш документ будет состоять из трех гридов и шапки. В шапке будет выбираться Кафе-бар " _Veine_" и отдел снабжения. В первом гриде будут находится наименования блюд. Во втором гриде — наименования продуктов для приготовления блюд. В третьем гриде — наименования продуктов для замены.

Любой объект в среде СУБД Oracle должен носить название. Ниже приведена расшифровка названий, которые будут использоваться при создании Таблиц (Tables), Видов (Views), Индексов (Indexes), Последовательности (Sequences) и Триггеров (Triggers).

![](<../../.gitbook/assets/image (871)>)

![](<../../.gitbook/assets/image (872)>)

![](<../../.gitbook/assets/image (873)>)

![](<../../.gitbook/assets/image (874)>)

![](<../../.gitbook/assets/image (875)>)

![](<../../.gitbook/assets/image (876)>)

Прежде чем создать любой документ, необходимо представить как он будет выглядеть в готовом виде: определить сколько в нём будет колонок, их типы, где будут первичные и внешние ключи, какие колонки будут со значением "Not Null" и т.д.

Grid № 1

* Колонка NRDOC является первичным ключом и связана внешним ключом с TMDB\_DOCS (колонка COD). (В таблице TMDB\_DOCS одна запись — один документ.)
* Колонка NRDOC1 так же является частью первичного ключа.
* Колонка Дата (DATA) предназначена для записи даты.
* Колонка Код (DISH) связана внешним ключом со справочником TMS\_UNIVERS (колонка COD).
* Колонка Наименование блюд (CLCDISHT) предназначена для вставки текста из справочника TMS\_UNIVERS.
* Колонки Передано (CANT1), Возвращено (CANT2) и Итого кол-во (CANT3) — числовые.

Grid № 2

* Колонки NRDOC, NRDOC1 и NRDOC2 являются составным первичным ключом.
* NRDOC, NRDOC1 связаны внешним ключом с таблицей YVEINE\_TMDB\_INTAKE\_LIST\_A (Grid 1).
* Колонка Код (PRODUCT) связана внешним ключом со справочником TMS\_UNIVERS (COD).
* Колонка Наименование продуктов (CLCPRODUCTT) — текст из TMS\_UNIVERS.
* Колонки Норма (CANT1), Цена (PRET1) и Сумма (SUMA1) — числовые.

Grid № 3

* Колонки NRDOC, NRDOC1, NRDOC2 и NRDOC3 являются составным первичным ключом.
* NRDOC, NRDOC1, NRDOC2 связаны внешним ключом с таблицей YVEINE\_TMDB\_INTAKE\_LIST\_B (Grid 2).
* Колонка Код (PRODUCT) связана внешним ключом со справочником TMS\_UNIVERS (COD).
* Колонка Наименование продуктов для замены (CLCPRODUCTT) — текст из TMS\_UNIVERS.
* Колонка Количество (CANT1) — числовая.

![](<../../.gitbook/assets/image (877)>)

Используемое программное обеспечение:

* ОС Windows 8.1 Build 9431
* Oracle VM VirtualBox 4.2.18 r88780
* Toad for Oracle 11.6
* Oracle 10g 10.2.0.3
* Universal Accounting Build 4.1.5.52

Глава 1 — Создание таблицы

{% stepper %}
{% step %}
### Подготовка: подключение и переход в Schema Browser

* Подключитесь к рабочей схеме через Toad, заполнив необходимые поля и нажав кнопку подключения.

![](<../../.gitbook/assets/image (878)>)

* Перейдите в Schema Browser с помощью соответствующей кнопки.

![](<../../.gitbook/assets/image (879)>)
{% endstep %}

{% step %}
### Таблица A: YVEINE\_TMDB\_INTAKE\_LIST\_A — создание и настройка колонок

1. Создание таблицы

* Нажмите создание новой ноды/таблицы и укажите имя таблицы: YVEINE\_TMDB\_INTAKE\_LIST\_A.

![](<../../.gitbook/assets/image (880)>)

2. Добавление колонок (через Add Column)

* NRDOC — NUMBER(10), PK, Not Null.
* NRDOC1 — NUMBER(10), PK, Not Null.
* ID — NUMBER(10).
* DATA — DATE.
* DISH — NUMBER(10).
* CANT1, CANT2, CANT3 — NUMBER(10) (одинаковая точность).

(скриншоты процесса добавления колонок)

![](<../../.gitbook/assets/image (881)>)

3. Создание ограничений (Constraints)

* На вкладке Constraints уже показан PK (две колонки). Создайте внешний ключ (Foreign Key) для NRDOC, ссылающийся на таблицу TMDB\_DOCS (поле COD). Установите опции On Delete Cascade и Deferrable-Initially Deferred.

![](<../../.gitbook/assets/image (882)>)

* Создайте внешний ключ для DISH, ссылающийся на справочник TMS\_UNIVERS (поле COD).

![](<../../.gitbook/assets/image (883)>)

4. Обновление списка объектов и проверка

* Нажмите Refresh all objects и найдите созданную таблицу в поиске.

![](<../../.gitbook/assets/image (884)>)
{% endstep %}

{% step %}
### Таблица B: YVEINE\_TMDB\_INTAKE\_LIST\_B — создание и настройка колонок

1. Создание таблицы

* Создайте новую таблицу с именем YVEINE\_TMDB\_INTAKE\_LIST\_B.

2. Добавление колонок

* NRDOC — NUMBER(10), PK, Not Null.
* NRDOC1 — NUMBER(10), PK, Not Null.
* NRDOC2 — NUMBER(10), PK, Not Null.
* ID — NUMBER(10).
* CANT — NUMBER(10).
* PRET1 — NUMBER(10).
* SUMA1 — NUMBER(10).
* PRODUCT — NUMBER(10).

(скриншоты добавления колонок)

3. Ограничения и внешние ключи

* PK: NRDOC, NRDOC1, NRDOC2 (отображается на вкладке Constraints).
* Добавьте внешний ключ на (NRDOC, NRDOC1), ссылающийся на YVEINE\_TMDB\_INTAKE\_LIST\_A (NRDOC, NRDOC1). Установите On Delete Cascade и Deferrable-Initially Deferred.
* Добавьте внешний ключ для PRODUCT, ссылающийся на справочник TMS\_UNIVERS (COD).

(скриншоты выбора таблиц/полей и опций)

4. Обновление и проверка

* Refresh all objects и найдите YVEINE\_TMDB\_INTAKE\_LIST\_B в списке.
{% endstep %}

{% step %}
### Таблица C: YVEINE\_TMDB\_INTAKE\_LIST\_C — создание и настройка колонок

1. Создание таблицы

* Создайте таблицу YVEINE\_TMDB\_INTAKE\_LIST\_C.

2. Добавление колонок

* NRDOC — NUMBER(10), PK, Not Null.
* NRDOC1 — NUMBER(10), PK, Not Null.
* NRDOC2 — NUMBER(10), PK, Not Null.
* NRDOC3 — NUMBER(10), PK, Not Null.
* ID — NUMBER(10).
* CANT1 — NUMBER(10).
* PRODUCT — NUMBER(10).

(скриншоты добавления колонок)

3. Ограничения и внешние ключи

* PK: NRDOC, NRDOC1, NRDOC2, NRDOC3.
* Добавьте внешний ключ (NRDOC, NRDOC1, NRDOC2), ссылающийся на YVEINE\_TMDB\_INTAKE\_LIST\_B (NRDOC, NRDOC1, NRDOC2). Включите On Delete Cascade и Deferrable-Initially Deferred.
* Добавьте внешний ключ для PRODUCT, ссылающийся на справочник TMS\_UNIVERS (COD).

(скриншоты выбора таблиц/полей и опций)

4. Обновление, поиск и Commit

* Нажмите Refresh all objects и найдите YVEINE\_TMDB\_INTAKE\_LIST\_C.
* Для завершения транзакции сохраните изменения командой Commit.

![](<../../.gitbook/assets/image (885)>)
{% endstep %}
{% endstepper %}

Примечание: все скриншоты и иллюстрации сохранены как в оригинале и указывают на внешние ресурсы. Не меняйте названия таблиц и полей при создании — они согласованы с описанием грида и связями (TMDB\_DOCS, TMS\_UNIVERS и т.д.).

Если нужно, могу:

* Сгенерировать SQL DDL команды для создания этих таблиц, ограничений и индексов.
* Преобразовать подробные скриншоты и подписи в отдельный пошаговый гайдинг для вставки в интерфейс GitBook с разбиением на меньшие шаги.
