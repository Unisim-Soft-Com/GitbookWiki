# Права доступа ACL

### Создание и управление ACL (Oracle DBMS\_NETWORK\_ACL\_ADMIN)

{% stepper %}
{% step %}
### Создаем ACL для курсов валют

```sql
-- 1 создаем ACL для курсов валют
EXECUTE DBMS_NETWORK_ACL_ADMIN.CREATE_ACL(
  'acl_for_get_curs.xml',
  'ACL for getting curs',
  'BOX',
  TRUE,
  'connect'
);
```

```sql
-- даем права другой схеме на существующую ACL
EXECUTE DBMS_NETWORK_ACL_ADMIN.ADD_PRIVILEGE(
  'acl_for_get_curs.xml',
  'THK',
  TRUE,
  'connect'
);
```

{% hint style="info" %}
Допускается добавление нескольких хостов в один ACL.
{% endhint %}

```sql
-- добавляем хосты в ACL
EXECUTE DBMS_NETWORK_ACL_ADMIN.ASSIGN_ACL(
  'acl_for_get_curs.xml',
  '*.cbpmr.net'
);
```

```sql
COMMIT;
```
{% endstep %}

{% step %}
### Создаем ACL для получения гугл-координат

```sql
-- 2 создаем ACL для получения гугл-координат
EXECUTE DBMS_NETWORK_ACL_ADMIN.CREATE_ACL(
  'acl_for_get_crd.xml',
  'ACL for getting coords',
  'BOX',
  TRUE,
  'connect'
);
```

```sql
-- даем права другой схеме на существующую ACL
EXECUTE DBMS_NETWORK_ACL_ADMIN.ADD_PRIVILEGE(
  'acl_for_get_crd.xml',
  'THK',
  TRUE,
  'connect'
);
```

{% hint style="info" %}
Допускается добавление нескольких хостов в один ACL.
{% endhint %}

```sql
-- добавляем хосты в ACL
EXECUTE DBMS_NETWORK_ACL_ADMIN.ASSIGN_ACL(
  'acl_for_get_crd.xml',
  '*.googleapis.com'
);
```

```sql
COMMIT;
```
{% endstep %}

{% step %}
### Создаем ACL для отправки почты через stunnel (localhost)

```sql
-- 3 создаем ACL для отправки почты через stunnel (localhost)
EXECUTE DBMS_NETWORK_ACL_ADMIN.CREATE_ACL(
  'acl_for_sendmail.xml',
  'ACL for sending mail',
  'BOX',
  TRUE,
  'connect'
);
```

```sql
-- даем права другой схеме на существующую ACL
EXECUTE DBMS_NETWORK_ACL_ADMIN.ADD_PRIVILEGE(
  'acl_for_sendmail.xml',
  'THK',
  TRUE,
  'connect'
);
```

{% hint style="info" %}
Допускается добавление нескольких хостов в один ACL. Можно указывать комбинации хост-порт.
{% endhint %}

```sql
-- добавляем хосты в ACL (host + порт)
EXECUTE DBMS_NETWORK_ACL_ADMIN.ASSIGN_ACL(
  'acl_for_sendmail.xml',
  'localhost',
  465,
  465
);

-- добавляем еще комбинацию хост-порт
EXECUTE DBMS_NETWORK_ACL_ADMIN.ASSIGN_ACL(
  'acl_for_sendmail.xml',
  'localhost',
  2525,
  2525
);
```

```sql
COMMIT;
```
{% endstep %}
{% endstepper %}

***

### Просмотр и проверка

```sql
-- просмотр списка схем, которые имеют права на использ. ACL
select acl, principal, privilege, is_grant, invert
from dba_network_acl_privileges;
```

```sql
-- проверка хостов, которые разрешены в ACL
select host, lower_port, upper_port, acl
from dba_network_acls;
```

***

### Удаление ACL и отключение привязки к хосту

```sql
-- удаляем ACL
execute DBMS_NETWORK_ACL_ADMIN.DROP_ACL('acl_for_send_mail.xml');

COMMIT;
```

```sql
-- отключаем привязку к хосту
BEGIN
  DBMS_NETWORK_ACL_ADMIN.UNASSIGN_ACL(
    host => '*.cbpmr.net'
  );
END;
/

COMMIT;
```

<details>

<summary>Полный синтаксис отключения привязки к хосту</summary>

```sql
DBMS_NETWORK_ACL_ADMIN.UNASSIGN_ACL (
  acl IN VARCHAR2 DEFAULT NULL,
  host IN VARCHAR2 DEFAULT NULL,
  lower_port IN PLS_INTEGER DEFAULT NULL,
  upper_port IN PLS_INTEGER DEFAULT NULL
);
```

</details>

***

Last updated 1 year ago
