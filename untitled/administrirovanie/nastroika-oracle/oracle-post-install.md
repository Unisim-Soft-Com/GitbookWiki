# Oracle post install

{% stepper %}
{% step %}
### Доступ к консоли Database Control

Database Control URL:

http://poseidon.autovoczal.com:1158/em

Команды для консоли/SQL\*Plus:

```
chcp 1251

sqlplus sys/sys as sysdba

show parameter global_names

alter system set global_names=true;

show parameter sort_area_size

alter system set sort_area_size=655360 scope=spfile;

show parameter sga_

alter system set sga_max_size=162M scope=spfile;

shutdown immediate;

startup mount;

alter database open;

// или просто
startup

alter system set sga_target=164M;

show parameter pga_

alter system set pga_aggregate_target=18M;
```

Настройка табличных пространств через консоль (EM):

* sysaux -> 500MB (datafile size)
* system -> 600MB (datafile size), 100MB (additional)
* undo -> 100MB (datafile size), 100MB (additional)
* users -> 100MB (datafile size), 10MB (additional)
{% endstep %}

{% step %}
### Включение ARCHIVELOG и настройка резервного копирования

Откройте Database Control:

http://poseidon.autovoczal.com:1158/em

В EM: Maintenance -> Recovery Settings -> включить ARCHIVELOG Mode

На сервере: Control panel -> Local Security Policy -> Local Policies -> User Rights Assignment -> Log on as a batch job -> Add user -> добавить пользователя Slava

На сайте нажмите Apply и перезапустите сервисы консоли.

Проверка режима архивации:

```sql
select log_mode from v$database;
```

Перезапустите сервисы консоли (в Windows — рестарт консоли).

В консоли EM:

* Recovery settings — папка: G:\Flash
* BackUp settings — папка: G:\BackUp (после указания выполнить Test Backup сверху)
* Schedule Backup -> Schedule Customized Backup: Options -> поставить 2 галочки возле delete
  * Установить время (ежедневно, бесконечно), OK

Далее в Maintenance можно просмотреть Jobs

RMAN (команды в cmd):

```
rman
connect target
// exit
```

Проверьте/установите размер хранилища для восстановления:

```sql
show parameter db_recovery_file_dest_size

alter system set db_recovery_file_dest_size=2000M;
```

(в режиме MOUNT)

Manage Current Backups — можно анализировать ситуацию.

Если файлы заархивированы, их можно удалить. Если случайно удалили и не заархивировали — использовать SELECT и CROSSCHECK в интерфейсе/консоли RMAN на вкладке бэкапов.

Пример последовательности восстановления:

```
shutdown immediate;
startup mount;
alter database recovery until cancel;
alter database open resetlogs;
```

Лог сервера можно просмотреть в файле:

G:\oracle\product\10.2.0\admin\virtual\bdump\alert\_virtual.log

В EM: Maintenance -> Perform Recovery

Примечание: recovery — это откат всех изменений, затем применение изменений из архива. Экспорт данных выполняется утилитой exp.

Если возникают проблемы, выключите БД и переведите в режим MOUNT — тогда доступны операции Restore и Recovery.
{% endstep %}

{% step %}
### Создание схем и импорт данных

Откройте скрипты (примерный путь):

F:\Good071120-4.1.2.031\script\sys

Подготовьте папки для файлов заранее.

Рекомендация по размещению: индексные табличные пространства на одном физическом диске, остальные — на других.

Указывать AUTOEXTEND ON NEXT 100M для файлов данных.

Запуск скриптов (пример):

```
cd F:\Good071120-4.1.2.031\script\sys

-- опционально
user_UN4$repozitar.sql --опциональный - надо добавить grant create any table

user_UN4pack.sql

sys_Traffic.sql
```

Импорт через run.bat:

F:\Good071120-4.1.2.031\text\import\run.bat

Перед запуском в run.bat правильно указываем сервер БД, новую и старую схему (из которой был сделан экспорт). Файл экспорта должен называться expdat.dmp.

(содержание ran.dat imp1 virtual built built)

После окончания импорта просмотреть лог импорта (impлог).

Далее подключаемся к созданной схеме и компилируем представления, триггеры, пакеты.
{% endstep %}

{% step %}
### Установка corefiles и настройка клиента (UniAC/Good)

Настройки BDE Administrator:

* mpriv -> C:\temp
* на второй вкладке drivers\native\paradox\netdir -> C:\temp

Запустить uniacclient из папки good (для HK логин/пароль — dep/q)

В клиенте:

* Server -> virtual
* Name in DB -> новая схема

Обязательно должен быть установлен принтер (хотя бы условный).

Настройки Office:

* Excel -> Macros -> безопасность -> Low
* Excel -> Trusted Publishers -> галочка у "Trust visual basic projects"
* Аналогичные настройки в Word

Выполнить базовую проверку программы — сделать пару отчетов, заполнить справочники.
{% endstep %}

{% step %}
### Финальные RMAN-операции и очистка архивов

Выполните:

```
chcp 1251

rman
connect target;
crosscheck archivelog all;
delete expired archivelog all;
```
{% endstep %}
{% endstepper %}
