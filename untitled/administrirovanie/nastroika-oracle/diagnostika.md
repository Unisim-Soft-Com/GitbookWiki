# Диагностика

{% stepper %}
{% step %}
### Определить SID и SERIAL# сессии

Если нет возможности выполнить команду ALTER SESSION в диагностируемой сессии, нужно определить sid и serial# нужной сессии — по view v$session.
{% endstep %}

{% step %}
### Включить трассировку

Трассировку желательно включить непосредственно перед выполнением проблемного действия, чтобы уменьшить объём лишних данных.

#### Если есть возможность выполнить в диагностируемой сессии:

{% code title="SQL" %}
```sql
alter session set
events '10046 trace name context forever, level 12'
```
{% endcode %}

#### Если включение выполняется из другой сессии:

Вместо sid, serial# — значения, найденные на первом шаге.

{% code title="PL/SQL" %}
```sql
begin
  dbms_system.set_ev(sid,serial#,10046,12,'');
end;
```
{% endcode %}
{% endstep %}

{% step %}
### (Опционально) STATISTICS\_LEVEL

Значение по умолчанию для параметра statistics\_level = typical. При таком значении детальная статистика выполнения запроса (row source execution statistics) может содержать существенную погрешность. Если есть подозрения на ошибки подсчёта статистики выполнения, можно повторить трассировку с включённым:

{% code title="SQL" %}
```sql
alter session set statistics_level = all
```
{% endcode %}

{% hint style="info" %}
При этом возможно увеличение общего времени выполнения запроса из‑за дополнительной нагрузки на более точный подсчёт статистики, особенно при большом количестве относительно быстрых операций (nested loops).
{% endhint %}
{% endstep %}

{% step %}
### Выполнить проблемное действие

1. Выполнить проблемное действие в программе.
2. Дождаться окончания работы в приложении и закрыть программу (завершить сессию).

Если не завершить сессию, часть необходимой информации не попадёт в трейс-файл. Перед закрытием программы, из диагностируемой сессии нужно выполнить (если есть возможность) следующие команды:

{% code title="SQL" %}
```
```
{% endcode %}

```sql
alter session set session_cached_cursors = 0;
-- закрытие кэшированных курсоров
alter session set events '10046 trace name context off';
-- отключение трассировки
```

Именно при закрытии курсоров в трэйс-файл попадает информация о плане выполнения запросов.
{% endstep %}

{% step %}
### Проверить наличие трейс-файла

* В обычной конфигурации трейс-файлы формируются в папке udump.

Найти путь к udump можно так:

{% code title="SQL" %}
```sql
select value from v$parameter where name='user_dump_dest'
```
{% endcode %}

* Если сервер работает в Shared Server Mode, или диагностируемая сессия — job или другой background процесс, то трейс будет сформирован в папке bdump:

{% code title="SQL" %}
```sql
select value from v$parameter
where name='background_dump_dest'
```
{% endcode %}

В трейс-файле должна быть строка вида: \*\*\* SESSION ID:(sid.serial#) <дата и время> где sid и serial# — из шага 1.

Если трейс не сформировался, необходимо повторить процедуру (возможно, была некорректно идентифицирована нужная сессия).
{% endstep %}

{% step %}
### Обработать трейс-файл при помощи tkprof

Необходимо получить 4 файла, обработанных tkprof — без сортировки и с тремя видами сортировок: sort=prsela, sort=exeela, sort=fchela.

Пример (имя файла трассировки — catalog\_ora\_2384.trc). При каждом вызове указывайте новое имя выходного файла, чтобы не перезаписать уже имеющиеся. Удобно добавлять суффикс с первой буквой параметра сортировки.

1.

{% code title="Команда" %}
```bash
tkprof catalog_ora_2384.trc catalog_ora_2384.out sys=no
```
{% endcode %}

2.

{% code title="Команда" %}
```bash
tkprof catalog_ora_2384.trc catalog_ora_2384_p.out sys=no sort=prsela
```
{% endcode %}

3.

{% code title="Команда" %}
```bash
tkprof catalog_ora_2384.trc catalog_ora_2384_e.out sys=no sort=exeela
```
{% endcode %}

4.

{% code title="Команда" %}
```bash
tkprof catalog_ora_2384.trc catalog_ora_2384_f.out sys=no sort=fchela
```
{% endcode %}
{% endstep %}

{% step %}
### Сбор результатов для анализа

Для дальнейшего анализа нужны все полученные на выходе tkprof файлы и исходный файл трассировки.
{% endstep %}
{% endstepper %}

<details>

<summary>Дополнительная информация</summary>

Ссылка: http://www.sql.ru/faq/faq\_topic.aspx?fid=389

(Оригинал содержал также навигационные ссылки и заметки по 11g — они не изменяли суть процедуры.)

</details>
