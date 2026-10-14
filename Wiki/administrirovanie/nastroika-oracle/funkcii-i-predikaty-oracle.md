# Функции и предикаты oracle

* Функция удаляет все спец. символы:

{% code title="Пример" %}
```sql
select regexp_replace('AQ83D 29 EU/B<>!//\!!sg,. ?','\W?','',1,0,'i')
from dual
```
{% endcode %}

* Пересекающиеся интервалы дат:

{% code title="Пример" %}
```sql
select 1 from dual
where (sysdate,sysdate+1) overlaps (sysdate+2,sysdate+3);
```
{% endcode %}

Ссылки:

* http://www.orafaq.com/node/2067
* http://www.sql.ru/forum/actualthread.aspx?tid=389945
