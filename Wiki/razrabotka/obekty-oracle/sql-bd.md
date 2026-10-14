# SQL; BD

## Пути / файлы

* Good-ы:
  * \builder\work\good
  * \srv-unsdc1\arhiv\ArcGood
  * file:///X:\test4.ora\arc
* \srv-usgw1\ftp\pub
* \192.168.0.2\public\install — инстал от тех отдела

## Отчёты / параметры

* отчет CST => обращение к датам `:datebegin`, `:datefinal`

## Полезные SQL-приёмы и запросы

*   Объединение значений поля через запятую:

    ```sql
    select wm_concat(поле) from таблица;
    ```
* Тексты пакетов, вьюшек и т.п.:
  * `user_source` (или `all_source` под sys-ом)
*   Получение данных, какими они были час назад:

    ```sql
    select … from таблица as of timestamp (systimestamp - interval '1' hour) a where …;
    ```

    (вместо `hour` может быть `minute` и т.п.)
*   Получение версии Oracle:

    ```sql
    select * from v$version;
    -- или
    select VERSION from V$INSTANCE;
    ```

    (выполнять под `sys`-ом)
*   Параметры сессии:

    ```sql
    select * from NLS_Session_Parameters;
    ```
*   Лог входов в программу (если используется новый конфигуратор):

    ```sql
    select * from a$act t where action='l' --and new_value<>'Login successful';
    ```
*   Форматирование числа с разделителями по 3 цифры:

    ```sql
    SELECT trim(TO_CHAR(-1234567819.12,'999G999G999G999D99','NLS_NUMERIC_CHARACTERS = ''. '' '))
    FROM DUAL;
    ```
*   Пользователи в новом конфигураторе:

    ```sql
    select id,username,OBJ_ID,password||(select old_value from a$act t where action='p' and t.obj_id=a.obj_id
    and stamp=(select max(t1.stamp) from a$act t1 where t1.action='p' and t1.obj_id=t.obj_id)) r
    from a$users$v a where enabled=1 --and admin=1
    order by id;
    ```
*   Контексты:

    ```sql
    grant select on v_$context to public;
    select * from v$context;
    SELECT * FROM all_context;
    ```

## Таблицы / поля / функции и где что берётся

* `tmdb_docs_add` — данные со вкладки "Информация" документов
* `userid` from `tparams` (текущий user клиента)\
  или `sys_context('envun4','param_userid')` -> получим код текущего пользователя в клиенте; далее можно вытащить его имя из `xusers`
* `unp_ini.get_strings` => название документа по `sysfid`
* `tmdb_cm.sptype`:
  * \=0 — основная проводка
  * \=1 — вспомогательная
  * \=2 — зарегистрированные остатки
  * \=3 — (?) П для А/П счетов
* `un$valuta.getcurs` — курс валюты
* `yimport.get_parameter` — курс евро
* `un$currencytotxt.romspell` — сумма прописью на соответствующем языке
* `un$xparamsintrepr.getparameter` — данные со вкладки General
*   Получение свойства конфигуратора из узла соответствующего документа:

    ```sql
    select ivalue from a$adp where obj_id = (
      select obj_id from a$docs$v where sysfid = 48331
    ) and key='TIPAUTOCOMPLETARE';
    ```

    (например, для документа с `sysfid = 48331`)
* `xgridprop` (в старом администраторе); `a$lob` (в новом конфигураторе) — таблицы с дизайнами
* Значения `xgridprop.objtype`:
  * \=0 — это дизайн
  * \=1 — это cst-документ
  * \=2 — это информация о проводках
  * \=3,5 — это выпадающий справочник, отчет
* `tmdb_syssv.vpret` и т.д. — заголовки столбцов из `tms_syss`.\
  Если колонка `vpret` непустая, то вместо PRET в выпадающем справочнике `tms_syss` в клиенте будет видно внесенное название

## Конфигуратор / история изменений

* `a$act` можно отследить историю изменений узлов в конфигураторе.
  * Маленькие буквы в колонке `action` — это действия со свойствами.
  * Большие — со всем узлом.
  * `d`/`D` — удаление и т.п.

## Прочее

* `tmdb_cm.sptype` — см. выше (виды проводок)
* `tmdb_docs_add` — см. выше (информация документа)
* Примеры путей и ссылок сохранены в исходном виде.

Сохранённые ресурсы:

* [PreviousOTRS](otrs.md)

Last updated 1 year ago
