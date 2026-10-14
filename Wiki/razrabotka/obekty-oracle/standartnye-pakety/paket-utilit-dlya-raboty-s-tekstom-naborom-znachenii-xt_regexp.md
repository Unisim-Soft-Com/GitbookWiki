# Пакет утилит для работы с текстом, набором значений xt\_regexp

Пакет — https://github.com/xtender/XT\_REGEXP

Описание пакета — https://github.com/xtender/XT\_REGEXP/wiki/%D0%9A%D1%80%D0%B0%D1%82%D0%BA%D0%BE%D0%B5-%D0%BE%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D0%B5

## Краткое описание

Function list:

### split\_simple

```sql
function split_simple(p_str in varchar2, p_delim in varchar2)
return varchar2_table pipelined;
```

Простое разбиение строки по подстроке-делимитеру (без регулярных выражений).

### split

```sql
function split(pStr varchar2, pDelimRegexp varchar2, pMaxCount number default 0)
return varchar2_table;
```

Функция разбивает строку по подстрокам, соответствующим регулярному выражению.

Примеры:

```sql
select * from table(
  xt_regexp.split('Please, make me happy!','(?<=,)\s')
);
```

```sql
select * from table(
  xt_regexp.split('Please, make me happy!','\s',3)
);
```

### matches

```sql
function matches(
  pStr varchar2,
  pPattern varchar2,
  pCANON_EQ number default 0,
  pCASE_INSENSITIVE number default 0,
  pCOMMENTS         number default 0,
  pDOTALL           number default 0,
  pMULTILINE        number default 0,
  pUNICODE_CAS      number default 0,
  pUNIX_LINES       number default 0
)
return boolean;
```

Функция возвращает true, если входная строка соответствует регулярному выражению.

Параметры:

* pStr — строка для проверки;
* pPattern — регулярное выражение;
* прочие параметры — модификаторы регулярного выражения:
  * CANON\_EQ — canonical equal;
  * CASE\_INSENSITIVE — регистронезависимый поиск;
  * COMMENTS — игнорировать комментарии (начинаются с #);
  * DOTALL — символ . включает разделитель строк (по умолчанию — нет);
  * LITERAL — шаблон не как регулярное выражение;
  * MULTILINE — многострочный режим;
  * UNICODE\_CASE — учёт регистра для Unicode;
  * UNIX\_LINES — разделитель строк — \n.

### get\_matches

```sql
function get_matches(
  pStr varchar2,
  pPattern varchar2,
  pMaxCount number default 0,
  pCANON_EQ number default 0,
  pCASE_INSENSITIVE number default 0,
  pCOMMENTS         number default 0,
  pDOTALL           number default 0,
  pMULTILINE        number default 0,
  pUNICODE_CAS      number default 0,
  pUNIX_LINES       number default 0)
return varchar2_table;
```

Функция возвращает коллекцию совпавших подстрок. Параметры как в функции matches, кроме pMaxCount — максимальное количество возвращаемых строк (0 или не указан — вернуть все).

Пример:

```sql
select * from table(
  xt_regexp.get_matches('Please, make me happy!','\S*m\S*')
);
```

### join\_matches

```sql
function join_matches(
  pStr varchar2,
  pPattern varchar2,
  pDelim varchar2 default ';',
  pCANON_EQ number default 0,
  pCASE_INSENSITIVE number default 0,
  pCOMMENTS         number default 0,
  pDOTALL           number default 0,
  pMULTILINE        number default 0,
  pUNICODE_CAS      number default 0,
  pUNIX_LINES       number default 0)
return varchar2;
```

Аналог get\_matches, но возвращает строку — объединённые элементы коллекции через заданный разделитель.

### replace\_all

```sql
function replace_all(pStr varchar2, pPattern varchar2, pReplacement varchar2)
return varchar2;
```

Заменяет все совпадения шаблона на заданную строку замены.

Пример — добавить "Scott!!!!" после слова "Please" перед запятой:

```sql
select xt_regexp.replace_all(
  'Please, make me happy!',
  '(?<=Please)(,)',
  '$1 Scott!!!!'
) from dual;
```

Результат: Please, Scott!!!! make me happy!

### replace\_first

```sql
function replace_first(pStr varchar2, pPattern varchar2, pReplacement varchar2)
return varchar2;
```

Как replace\_all, но заменяет только первое вхождение.
