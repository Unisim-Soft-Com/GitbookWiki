# Grants(гранты)

## Примеры добавления грантов

{% stepper %}
{% step %}
### Грант на каталог client\_bank

{% code title="Пример" %}
```
```
{% endcode %}

```sql
begin
  dbms_java.grant_permission( 'Имя_схемы',
    'SYS:java.io.FilePermission', '/share/un4/client_bank', 'ALL' );
end;
```

Добавляет грант на каталог `client_bank`.
{% endstep %}

{% step %}
### Грант на каталог и все файлы в нём

{% code title="Пример" %}
```
```
{% endcode %}

```sql
begin
  dbms_java.grant_permission( 'Имя_схемы',
    'SYS:java.io.FilePermission', '/share/un4/client_bank/*', 'ALL' );
end;
```

Добавляет грант на каталог `client_bank` и все файлы, находящиеся в нём.
{% endstep %}

{% step %}
### Рекурсивный грант на каталог и все вложенные файлы/каталоги

{% code title="Пример" %}
```
```
{% endcode %}

```sql
begin
  dbms_java.grant_permission( 'Имя_схемы',
    'SYS:java.io.FilePermission', '/share/un4/client_bank/-', 'ALL' );
end;
```

Добавляет грант на каталог `client_bank` и рекурсивно на все файлы и каталоги, находящиеся в нём.
{% endstep %}
{% endstepper %}

***

## Удаление/отключение грантов

{% stepper %}
{% step %}
### Просмотр текущих грантов

```sql
select * from dba_java_policy;
```
{% endstep %}

{% step %}
### Отключение (перевод в состояние DISABLED)

{% code title="Пример: revoke_permission" %}
```
```
{% endcode %}

```sql
dbms_java.revoke_permission(
  'USER1',
  'java.io.FilePermission',
  'd:\temp\',
  'read,write'
);
```

Выполнение этого переводает грант в состояние `DISABLED`.
{% endstep %}

{% step %}
### Удаление гранта

```sql
dbms_java.delete_permission( /* здесь SEQ отключенного гранта */ );
```

Удаляет грант.
{% endstep %}
{% endstepper %}

***

Выполнять под SYS.

Сделать COMMIT.

Перезапустить сессию (уну), где пытаемся создать/прочитать файл.
