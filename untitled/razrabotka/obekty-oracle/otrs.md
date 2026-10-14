# OTRS

## Запрос 1

```sql
SELECT datest, login, wcomment, clcieventid, round(sum(utime)/3600,2) time
from vxuserwork
where del=0 and nticket=НОМЕР_ЗАЯВКИ
group by datest, login, wcomment, clcieventid
```

## Запрос 2

```sql
SELECT nticket, wcomment, clcieventid, round(sum(utime)/3600,2) time
from vxuserwork
where del=0 /*and nticket=НОМЕР_ЗАЯВКИ*/ and trunc(datest)='03.01.2011' and login='epavlovscaia'
group by nticket, datest, wcomment, clcieventid
order by datest
```

## Запрос 3

```sql
select *
FROM XUSERWORK t_uw
WHERE
TO_CHAR(datest,'MM.yyyy')=TO_CHAR(SYSDATE,'MM.yyyy') AND userid=':[UserID]:'
```

## Запрос 4

```sql
select t_uw.*
FROM XUSERWORK t_uw
WHERE
TO_CHAR(datest,'MM.yyyy')=TO_CHAR(SYSDATE,'MM.yyyy') AND userid=':[UserID]:'
and nticket='2011051310216'
order by DATEST
```
