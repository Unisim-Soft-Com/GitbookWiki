# Поиск недостающих индексов

{% hint style="warning" %}
Проблема с недостающими индексами:

Любая таблица должна иметь индекс на поле, которое ссылается внешним ключем на tmdb\_docs.

Иначе при удалении документа блокируется вся таблица докс и все висит, когда работают хотя бы 2 пользователя.

Надо создать индексы, которые предложит скрипт — и проблема зависаний должна решиться.
{% endhint %}

{% code title="create_missing_indexes.sql" %}
```
```
{% endcode %}

select wm\_concat(chr(10)||'CREATE INDEX '||substr(constraint\_name,1,28)||'\_I ON '||table\_name||'('|| cname1 || nvl2(cname2,','||cname2,null) || nvl2(cname3,','||cname3,null) || nvl2(cname4,','||cname4,null) || nvl2(cname5,','||cname5,null) || nvl2(cname6,','||cname6,null) || nvl2(cname7,','||cname7,null) || nvl2(cname8,','||cname8,null)||');')new\_index from ( select b.table\_name, b.constraint\_name, max(decode( position, 1, column\_name, null )) cname1, max(decode( position, 2, column\_name, null )) cname2, max(decode( position, 3, column\_name, null )) cname3, max(decode( position, 4, column\_name, null )) cname4, max(decode( position, 5, column\_name, null )) cname5, max(decode( position, 6, column\_name, null )) cname6, max(decode( position, 7, column\_name, null )) cname7, max(decode( position, 8, column\_name, null )) cname8, count(\*) col\_cnt from (select substr(table\_name,1,30) table\_name, substr(constraint\_name,1,30) constraint\_name, substr(column\_name,1,30) column\_name, position from user\_cons\_columns ) a, user\_constraints b where a.constraint\_name = b.constraint\_name and b.constraint\_type = 'R' group by b.table\_name, b.constraint\_name ) cons where col\_cnt > ALL ( select count(\*) from user\_ind\_columns i where i.table\_name = cons.table\_name and i.column\_name in (cname1, cname2, cname3, cname4, cname5, cname6, cname7, cname8 ) and i.column\_position <= cons.col\_cnt group by i.index\_name ) Last updated 1 year ago
