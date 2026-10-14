# Экспорт в DBF файл

Экспорт данных без шаблона dbf.

Функция:

```sql
make_dbf
(ora_table_name VARCHAR2,
 dbf_filename VARCHAR2,
 l_src_char_set VARCHAR2 DEFAULT NULL,
 l_dst_char_set VARCHAR2 DEFAULT NULL,
 dbf_tmpl_filename VARCHAR2 DEFAULT NULL)
```

В функцию необходимо передать имя таблицы или вьюхи, а также путь и имя создаваемого файла на сервере. Также можно передать входящую и исходящую кодировку (см. пример в описании пакета).

Путь берется из параметров directory:

```sql
select directory_path into v_directory
from all_directories
where directory_name = 'MAIL_DBF';
```

{% stepper %}
{% step %}
### Шаг — дать права для директории (требуется выполнение под SYS)

Пример (выполнить под SYS):

```plsql
begin
  dbms_java.grant_permission( 'DEV', 'SYS:java.io.FilePermission',
  '/var/un4/mail_dbf/*',  'read,write' );
end;
```

Права вступают в силу в новых сессиях.
{% endstep %}

{% step %}
### Шаг — пример получения пути и вызова make\_dbf

```plsql
declare
  v_directory long;
begin
  select directory_path into v_directory
  from all_directories
  where directory_name = 'MAIL_DBF';
```

```plsql
  un$ora2dbf.make_dbf(
    'VMS_OPER_MARSH',
    v_directory||'/oper_marsh.dbf',
    null,
    'RUSSIAN_CIS.CL8MSWIN1251'
  );
end;
```
{% endstep %}

{% step %}
### Особенность: заполнение заголовков столбцов

По умолчанию функция make\_dbf генерирует dbf-файл с заголовками столбцов, которые дополняются пробелами.

Если нужно дополнять пустыми значениями (NULL) — необходимо изменить функцию make\_dbf: заменить

```plsql
tmp_raw := utl_raw.cast_to_raw(RPAD(l_flds(i).NAME, 11, ' '));
```

на

```plsql
tmp_raw := utl_raw.cast_to_raw(RPAD(l_flds(i).NAME, 11, chr(0)));
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Параметры l\_src\_char\_set и l\_dst\_char\_set позволяют задать преобразование кодировок. Путь к файлу формируется с использованием значения из ALL\_DIRECTORIES.
{% endhint %}
