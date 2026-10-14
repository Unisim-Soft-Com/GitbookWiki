# Пакет для управления логированием данных pkg\_log\_data\_util

Пакет для управления логированием данных pkg\_log\_data\_util есть на схеме box b и в svn.

Пакет предназначен для включения логов на изменение данных в таблицах. Проблемы могут возникнуть (ошибка при создании триггера), если в таблицах используются поля пользовательских типов/коллекций (напр. un$cm).

{% hint style="warning" %}
Если таблицы содержат поля пользовательских типов или коллекций (например, un$cm), создание триггеров может завершиться ошибкой.
{% endhint %}

В пакете есть следующие процедуры:

* enable\_table\_log — включить лог на таблицу (вызывает процедуры create\_table\_log и create\_trigger\_log)
* create\_table\_log — создать таблицу для логов
* create\_trigger\_log — создать логирующий триггер

Имя таблицы для логов можно указать явно либо получить автоматически как имя\_таблицы\_log. Имя триггера присваивается автоматически: имя\_таблицы\_trg\_log.

Пример включения логов на таблицу:

{% code title="Пример" %}
```plsql
begin
  PKG_LOG_DATA_UTIL.ENABLE_TABLE_LOG('tslrprm_calenddz');
end;

begin
  PKG_LOG_DATA_UTIL.ENABLE_TABLE_LOG('tslrprm_linkd');
end;
```
{% endcode %}

Ссылка на связанный материал:

* Автоматическая генерация скриптов pkg\_gen\_ddl\_util: https://unisim-soft.gitbook.io/wiki/razrabotka/obekty-oracle/standartnye-pakety/avtomaticheskaya-generaciya-skriptov-pkg\_gen\_ddl\_util

Last updated 1 year ago
