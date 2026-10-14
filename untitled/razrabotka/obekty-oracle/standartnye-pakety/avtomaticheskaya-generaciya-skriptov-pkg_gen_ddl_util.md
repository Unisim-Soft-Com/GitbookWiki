# Автоматическая генерация скриптов pkg\_gen\_ddl\_util

Пакет для генерации скриптов DDL — `pkg_gen_ddl_util` — есть на схеме `box` и в SVN.

В пакете есть функция для генерации скрипта простого триггера (с использованием переменной типа %ROWTYPE) на вьюху.

Пример использования функции из пакета:

{% code title="Пример" %}
```plsql
begin
  say(pkg_gen_ddl_util.get_view_trigger('YPMR_VSLRPRM_MROT','YPMR_tSLRPRM_MROT'));
end;
```
{% endcode %}
