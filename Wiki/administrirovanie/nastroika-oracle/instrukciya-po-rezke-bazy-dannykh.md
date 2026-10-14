# Инструкция по резке базы данных

{% stepper %}
{% step %}
### Настройка tablespaces

Вначале настраиваем tablespaces так же, как на оригинальном сервере. Можно использовать un4Versions.

```sql
CREATE TABLESPACE TABSPACE_ARHIV DATAFILE
'F:\oradata11\TABSPACE_ARHIV.DBO' SIZE 500M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TABSPACE_GARA DATAFILE
'F:\oradata11\TABSPACE_GARA.DBO' SIZE 200M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_DB1 DATAFILE
'F:\oradata11\TBS_GARA_DB1.DBO' SIZE 200M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_DB3 DATAFILE
'F:\oradata11\TBS_GARA_DB3.DBO' SIZE 200M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_DB4 DATAFILE
'F:\oradata11\TBS_GARA_DB4.DBO' SIZE 200M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_DB5 DATAFILE
'F:\oradata11\TBS_GARA_DB5.DBO' SIZE 1212800K AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_DBT DATAFILE
'F:\oradata11\TBS_GARA_DBT.DBO' SIZE 200M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_IND2 DATAFILE
'F:\oradata11\TBS_GARA_IND2.DBO' SIZE 200M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_IND2B0 DATAFILE
'F:\oradata11\TBS_GARA_IND2BO.DBO' SIZE 200M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_IND2CM DATAFILE
'F:\oradata11\TBS_GARA_IND2CM.DBO' SIZE 200M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_IND2RU DATAFILE
'F:\oradata11\TBS_GARA_IND2RU.DBO' SIZE 200M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_SYS DATAFILE
'F:\oradata11\TBS_GARA_SYS.DBO' SIZE 100M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBS_GARA_SYS2 DATAFILE
'F:\oradata11\TBS_GARA_SYS2.DBO' SIZE 100M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBSROLLBIG DATAFILE
'F:\oradata11\TBSROLLBIG.DBO' SIZE 600M AUTOEXTEND ON NEXT 20M;
CREATE TABLESPACE TBSROLLSMALL DATAFILE
'F:\oradata11\TBSROLLSMALL.DBO' SIZE 200M AUTOEXTEND ON NEXT 20M;
```
{% endstep %}

{% step %}
### Установка вспомогательных схем

Устанавливаем схемы: UN4PUBLIC, ARHIV, ADM.

Важно: не ставим схему GARA и собственный un4public у автовокзала — их нужно брать со старого сервера.

Совет: все эти схемы можно переносить с помощью режима сравнения схем в un4Versions.
{% endstep %}

{% step %}
### Создание документа с остатками

Выполните процедуру:

```sql
adm.close_sold('01.01.2011');
```

Эта процедура:

* удаляет проводки и документы до указанной даты;
* предварительно создает копии проводок и документов в базе архив (tmdb\_cm\_2011, tmdb\_docs\_2011).

Примечания:

* CLOSE\_SOLD\_REZKA — вариант, который не удаляет проводки. Создает остатки с кодом 0, а старому документу остатков присваивает nextval значение сиквенса.
{% endstep %}

{% step %}
### Экспорт по фильтру (включая документ остатков и все более поздние операции)

Идея: экспортировать только отрезок базы, начиная с документа остатков. (Фильтр по дате был впервые реализован для автовокзала и затем адаптирован для бухгалтерии).

Шаги: A. Указываем параметры подключения. Выбираем схему GARA и Oracle directory.

B. На вкладке «Резка базы»:

* ставим дату (например, если нужно оставить весь 2011 год и остальные — дата = 01.01.2011);
* в списке документов указываем номер документа остатков (например, 1), созданного на предыдущем шаге;
* нажать кнопку «Установить фильтр для резки».

В результате таблица doks будет отфильтрована по условию:

Datamanual >= to\_date('01.01.2012') or cod = 1

Проверить фильтр можно на вкладке «Фильтр на таблицы», поставив галочку «Контроль вручную».

C. Вернуться на вкладку «Действия» и нажать «Экспорт по фильтру».
{% endstep %}

{% step %}
### Импорт дампа на новом сервере

Импортировать полученный дамп на новом сервере стандартно, согласно инструкции по импорту схемы с помощью uniVersions. После импорта пересоздать индексы.
{% endstep %}
{% endstepper %}

[PreviousBackUp при помощи uniVersions](eksport-import-skhemy-oracle/backup-pri-pomoshi-universions.md) [NextFGA](fga.md)
