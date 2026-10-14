# Настройка базы

{% stepper %}
{% step %}
### Выполните в базе данных

```sql
alter system flush shared_pool;
update sys.props$ set value$ = 'DD.MM.YYYY' where name = 'NLS_DATE_FORMAT';
commit;
alter system flush shared_pool;
shutdown immediate;
startup;
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Если при входе в базу возникает ошибка ORA-00604 или ORA-12705, попробуйте добавить переменную окружения:

* В Windows: Мой компьютер -> Свойства -> Дополнительно -> Переменные среды -> добавить
  * `NLS_LANG=AMERICAN_RUSSIAN.CL8MSWIN1251`

Если это не поможет, добавьте тот же параметр в реестр Oracle (regedit):

* Добавьте `NLS_LANG=AMERICAN_RUSSIAN.CL8MSWIN1251` в соответствующий ключ Oracle.
{% endhint %}

Список серверов можно разместить в реестре или в файле:

* В реестре:
  * `HKEY_CURRENT_USER\Software\CoreLab\ODAC\Connect`
* В файле:
  * `orases.xml`
