# Настройка Oracle GateWays Windows

HS\_FDS\_CONNECT\_INFO = firebird

HS\_FDS\_TRACE\_LEVEL = ON

{% stepper %}
{% step %}
### Настроил слушатель (oracle listener)

LISTENER:

```
LISTENER =
(ADDRESS_LIST=
  (ADDRESS=(PROTOCOL=tcp)(HOST=server1.BMEZ.WJ)(PORT=1522))
)
SID_LIST_LISTENER=
(SID_LIST=
  (SID_DESC=
    (SID_NAME=dg4odbc)
    (ORACLE_HOME=d:\oracle\product\11.2.0\tg_1)
    (PROGRAM=dg4odbc)
  )
)
ADR_BASE_LISTENER = d:\oracle\product\11.2.0\tg_1
```
{% endstep %}

{% step %}
### Настроил tnsnames на клиенте и сервере

Файл: d:\oracle\product\11.2.0\tg\_1\network\admin\tnsnames.ora

```
# tnsnames.ora Network Configuration File: d:\oracle\product\11.2.0\tg_1\network\admin\tnsnames.ora

dg4odbc =
(DESCRIPTION=
  (ADDRESS=(PROTOCOL=tcp)(HOST=server1)(PORT=1522))
  (CONNECT_DATA=(SID=dg4odbc))
  (HS=OK)
)
```
{% endstep %}

{% step %}
### Создал DBLink

```sql
CREATE DATABASE LINK DG4ODBC
CONNECT TO SYSDBA
IDENTIFIED BY <PWD>
USING 'DG4ODBC';
```

{% hint style="warning" %}
Внимание! При создании DATABASE LINKа необходимо указать пользователя и пароль с учетом регистра. Может понадобиться создать имя пользователя в верхнем регистре.
{% endhint %}
{% endstep %}
{% endstepper %}
