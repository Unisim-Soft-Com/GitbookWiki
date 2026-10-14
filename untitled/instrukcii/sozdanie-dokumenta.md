# Создание документа

Документы — реализуют ввод первичных и специализированных документов пользователя. Конфигурирование системы в разрезе документов — это создание новых документов, настройка интерфейсной части документов, настройка действий по обработке данных, настройка печатных форм из документа.

#### [Direct link to heading](sozdanie-dokumenta.md#id-1-sposob) 1 способ

Сделаем настраиваемый документ следующего вида:

![](<../.gitbook/assets/image (368)>)

{% stepper %}
{% step %}
### Подготовка: открыть конфигуратор и выбрать схему

Открыть конфигуратор, выбрать схему `Dev`. Нужно два раза щелкнуть по строке схемы `Dev` и ввести учетные данные. Для каждого пользователя создается учетная запись или можно использовать стандартную учетную запись логин — `pavel`, пароль — `p0` или сочетание клавиш Ctrl+F12.

![](<../.gitbook/assets/image (369)>)
{% endstep %}

{% step %}
### Создать группу документов и добавить документ

* В левом гриде выбрать логический узел \[`Documents`].
* На панели инструментов выбрать меню \[`Create`] → подпункт \[`Add node`].
* В диалоге выбрать тип узла \[`Document groups`]. Назвать новую группу — Тест.

![](<../.gitbook/assets/image (370)>)

* Выбрать созданную группу, затем меню \[`Create`] → \[`Add subnode`], тип объекта — \[`Documents`], имя объекта — Тестовый документ.

![](<../.gitbook/assets/image (371)>)

* После добавления узлов обязательно нажать кнопку \[`Commit transaction`].
{% endstep %}

{% step %}
### Настройка свойств документа

В правом гриде узла — Тестовый документ введем стандартные свойства.

![](<../.gitbook/assets/image (372)>)

Свойства уровня документа (описание):

| Имя свойства | Назначение свойства                                                                                |
| ------------ | -------------------------------------------------------------------------------------------------- |
| DB ID        | Идентификационный номер типа документа. Соответствует значению поля \[SysfID] в таблице документов |
| DLL ID       | Идентификационный номер DLL                                                                        |
| DocName      | Идентификатор документа в DLL                                                                      |
| Module       | Модуль, которому принадлежит документ. Соответствует значению поля \[m] в таблице документов       |

Базовый тип документа идентифицируется значениями свойств `DLL ID` и `DocName`.

Можно скопировать стандартный набор свойств и вставить в конфигураторе:

Copy

```
[ZZZ]
DB ID=10
.type.DB ID=Integer
DLL ID=4000
.type.DLL ID=Integer
DocName=DG1p21
.type.DocName=String
Module=M
.type.Module=String
```
{% endstep %}

{% step %}
### Создать журнал для нового документа (импорт узла)

Чтобы увидеть новый документ, необходимо создать новый журнал:

* Раскрыть логический узел \[`Journals group`].
* Выбрать объект (журнал) для экспорта (например: узел Материалы). Правой кнопкой мыши → \[`Data`] → \[`Export`] → подменю \[`Node`] (Текущий без вложенных) — копирование в буфер данных узла (объекта).

![](<../.gitbook/assets/image (373)>)

* Указав уровень в дереве объектов типа Журналы (например: выбрав узел Стандартные), последовательно выбрать меню \[`Data`] → \[`Import`] → подменю \[`New SubNode`] (Как новый узел) для импорта объекта на указанный уровень дерева.

![](<../.gitbook/assets/image (374)>)

* Переименовать узел (в свойствах узла, пункт меню \[`Node Properties`] указать `Caption` – `Test` и `Section` – `J_Test`).
* Изменить свойства узла: `Caption`, `DocTypesFilter` (Условие для `ID`), `SQLFilter` (Условие для `SysFID`), `DLL`, `JournalName`.

![](<../.gitbook/assets/image (375)>)

* Зафиксировать изменения в базе данных \[`Commit transaction`].
* Открыть клиент и убедиться, что там появился новый документ (Если клиент-приложение было открыто, нажать кнопку \[F5]).
* В клиенте выбрать Журналы – Test и создать новый документ (кнопка Insert), сохранить документ.

![](<../.gitbook/assets/image (376)>)
{% endstep %}

{% step %}
### Настройка документа в конфигураторе (интерфейс)

В конфигураторе добавляем свойства документа:

* `HeaderPanel = true` — отображение панели
* `GridCount = 1` — количество гридов

Внешний вид документа изменился:

![](<../.gitbook/assets/image (377)>)
{% endstep %}

{% step %}
### Создание таблиц и представлений в БД

Создать шапку и грид — SQL-скрипт:

{% code title="Создать таблицы и view" %}
```sql
-- Создать таблицу для шапки документа.
create table tmdb_test_m
(
 nrdoc number not null,
 cod number,
 txtcoment  varchar2(200 byte)
);

-- Создать уникальный индекс для таблицы tmdb_test_m.
create unique index tmdb_test_m_pk on tmdb_test_m
(nrdoc);

-- Добавить ограничения в таблицу tmdb_test_m.
alter table tmdb_test_m add (
constraint tmdb_test_m_pk
primary key
(nrdoc)
using index tmdb_test_m_pk
enable validate);

alter table tmdb_test_m add (
constraint tmdb_test_m_fk
foreign key (nrdoc)
references tmdb_docs (cod)
on delete cascade
deferrable initially deferred
enable validate);

-- Создать вид(вьюху) vmdb_test_m
create or replace view vmdb_test_m
as
select t.*
,(select denumirea from vms_univers where cod=t.cod) clccodt
from tmdb_test_m t;

-- Создать таблицу для  грида  документа.
create table tmdb_test_d
(
nrdoc number(38) not null,
nrdoc1 number(38) not null,
cod integer,
cant number
);

-- Создать последовательность tmdb_test_d_seq.
create sequence tmdb_test_d_seq
start with 1
maxvalue 999999999
minvalue 1
nocycle
cashe 20
noorder;

-- Создать уникальные индексы для таблицы tmdb_test_d.
create index tmdb_test_d_fk on tmdb_test_d
(nrdoc);

create unique index tmdb_test_d_pk on tmdb_test_d
(nrdoc, nrdoc1);

-- Создать триггер для таблицы tmdb_test_d.
create or replace trigger tmdb_test_d_trg
before insert on tmdb_test_d for each row
begin
 if :new.nrdoc1 is null then
  select tmdb_test_d_seq.nextval into :new.nrdoc1 from dual;
 end if;
end;

-- Создать ограничения для таблицы tmdb_test_d.
alter table tmdb_test_d add (
constraint tmdb_test_d_pk
primary key
(nrdoc, nrdoc1)
using index tmdb_test_d_pk
enable validate);

alter table tmdb_test_d add (
constraint tmdb_test_d_fk
foreign key (nrdoc)
references tmdb_docs (cod)
on delete cascade
deferrable initially deferred
enable validate);

-- Создать вид(вьюху) vmdb_test_d.
create or replace view vmdb_test_d
as
select t.*
,(select denumirea from vms_univers where cod=t.cod) clccodt
from tmdb_test_d t;
```
{% endcode %}
{% endstep %}

{% step %}
### Настройка источников данных (шапка и грид)

* В документе указать для шапки view `vmdb_test_m`, для грида — `vmdb_test_d`.
* В шапке: зажав Ctrl + правый клик в шапке → выбрать `Edit query`.

![](<../.gitbook/assets/image (378)>)

* В открывшемся окне настроить параметры запроса как на рисунке.

![](<../.gitbook/assets/image (379)>)

* Перейти на вкладку (в окне редактирования запроса) и нажать последовательно кнопки, отмеченные на скриншотах, установить галочку и подтвердить.

![](<../.gitbook/assets/image (380)>)

![](<../.gitbook/assets/image (381)>)

![](<../.gitbook/assets/image (382)>)

![](<../.gitbook/assets/image (383)>)

![](<../.gitbook/assets/image (384)>)

![](<../.gitbook/assets/image (385)>)

Нажать кнопку подтверждения на каждом этапе, чтобы применить настройки.

* На гриде: нажать Alt+Q и аналогичным образом настроить для вида `vmdb_test_d`. Основные отличия — список ключей для обновления и порядок сортировки.

![](<../.gitbook/assets/image (386)>)

* На вкладке `Insert` добавить SQL-запрос: select tmdb\_test\_d\_seq.nextval into :nrdoc1 from dual; — этот запрос заполняет поле `nrdoc1` значениями из последовательности `tmdb_test_d_seq`.

![](<../.gitbook/assets/image (387)>)
{% endstep %}

{% step %}
### Дизайн шапки документа

* В шапке: Ctrl + правый клик → `Design`.
* Добавить на панель четыре элемента:
  * `StaticText` — подпись для справочника
  * `StaticText` — подпись для комментария
  * `UnDBEdit` — ввод значения поля справочник
  * `DBEdit` — ввод значения поля комментарий
* В свойствах компонентов `UnDBEdit` и `DBEdit` установить свойство `DataField`:
  * Для поля справочник: `CLCCODT`
  * Для поля комментарий: `TXTCOMENT`

Шапка документа:

![](<../.gitbook/assets/image (388)>)
{% endstep %}

{% step %}
### Настройка грида (таблицы)

* На гриде нажать сочетание клавиш Alt+D.
* В открывшемся окне настроить необходимые свойства грида (колонки, типы, ключи, сортировку и т.д.) как на скриншоте.

![](<../.gitbook/assets/image (389)>)

В результате получится настроенный документ:

![](<../.gitbook/assets/image (390)>)
{% endstep %}
{% endstepper %}
