# Ошибки при expdp и impdp в Oracle XE 10g

При вызове expdp появляются ошибки:

* ORA-39006: internal error
* ORA-39213: Metadata processing is not available

Если ошибки возникли после перехода на однобайтную кодировку (CL8MSWIN1251), выполните следующие действия.

{% stepper %}
{% step %}
### Распаковать архив в папку rdbms

Скачать и распаковать содержимое архива в папку `rdbms` согласно пути установки Oracle.

Пример пути: D:\oracle\product\10.2.0\server\rdbms\\

Ссылка на архив: https://yadi.sk/d/8EedrSYP3Wo3Jc (xml.rar)
{% endstep %}

{% step %}
### Выполнить запрос с правами SYS

После распаковки архива выполнить команду в SQL\*Plus под пользователем SYS:

```sql
SQL> execute dbms_metadata_util.load_stylesheets;
```
{% endstep %}
{% endstepper %}

Если после выполнения этих шагов проблема не исчезла — проверьте правильность пути распаковки и права доступа к файлам в папке rdbms.
