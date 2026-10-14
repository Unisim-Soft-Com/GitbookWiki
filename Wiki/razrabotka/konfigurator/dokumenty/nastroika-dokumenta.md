# Настройка документа

(Direct link: https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/dokumenty/nastroika-dokumenta#nastroika-dokumenta)

Основные свойства документа определяются 2-мя параметрами:

* **DLL ID (Integer) =4000;**
* **DocName (String)=DG1p21;**

Включение шапки документа:

* **HeaderPanel (Boolean)=true;**

Включение панели в нижней части экрана:

* **PanelHeight1 (String)=100;**

Количество гридов в документе:

* **GridCount (Integer)=1**

Параметр для доступа к документу пользователей из других групп (не админов), доступ к документу в журнале:

* **Use in DB (Boolean)=true**

Поле типа DBMemo в дизайнере панели или шапки используется для вывода больших текстовых полей. Выбираем **DATAFIELD** из грида, которому подчиняется данное поле.

Привязка экшена к объекту button:

* Изменяем свойство **params** объекта button:
  * **TargetType=doc.action**
  * **action\_id=5**

Открываем произвольную панель (карточку) по кнопке:

* Внимание! Для работы панели необходимо добавить в tms\_univers строку с полем cod=0, иначе карточка не откроется.
  * **TargetType=cartela**
  * **TargetSection=ATTR\_EDI\_PL**
  * **nrdoc=\_nrdoc**
  * **MainTA=1**

При смене сисфида подгружается весь дизайн и функционал.

Итоги в документах (XTT):

* Необходимо включить в гриде по **ALT+D**, затем включить в **SagiProperties** по **ALT+Q** и добавить вычисляемые поля на вкладке **XTT**.

Соответствие полей документа и полей вьюхи:

* Счет — Ct и Dt
* Аналитика — Ctsc, Dtsc
* Центр затрат — CtDep, DtDep
* Субконто (или МОЛ) — CtSc1, Dtsc1

Стандартные (НЕНАСТРАИВАЕМЫЕ) документы имеют следующие настройки Alt+Q:

* Для шапки вьюха **VMDB\_ST201M** и поля для Кт части Ct, CtDep, CtSc, CtSc1 и Dt, DtDep, DtSc, DtSc1 для Дт части соответственно.
* Для грида вьюха **VMDB\_ST201D**. Поля настраиваются аналогично.

Автозаполнение шапки

* В запросе шапки документа, на вкладке **SQL** запросов, в Insert добавить:

```plsql
DECLARE
  v_par number;
BEGIN
  -- Устанавливаем значение параметра, например, если выбираем из узла
  v_par := pkg_adm_util.get_adm_text('cont_topl','','PTL');

  -- Указать параметр в запросе
  INSERT INTO имя_таблицы (поля, наше_поле)
  VALUES (:поля, v_par);
END;
```

Можно в шапке документа в дизайне указать параметр default на нужном поле.

***

## Быстрый поиск

(Direct link: https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/dokumenty/nastroika-dokumenta#bystryi-poisk)

Например:

```
ORIGIN=COD_OC
_KB=0
SpeedSearch=1
SpeedText=1
SpeedWhole=1
TIP=Q
SQL1=SELECT COD,pkg_mat_docs.tmc_get_ct(cod) denumirea
SQL2=,Un$to_Number(CODVECHI) inv_num
SQL3=FROM VMS_UNIVERS U WHERE TIP='F' AND GR1='100' AND ISARHIV IS NULL
SQL4=ORDER BY CODVECHI
LISTFIELDS=COD,DENUMIREA,INV_NUM
RESULTFIELDS=COD_OC,CLCCOD_OCT,INV_NUM
```

***

## Опции на документе

(Direct link: https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/dokumenty/nastroika-dokumenta#opcii-na-dokumente)

**GridMaster1, GridMaster2, GridMaster3** в документах типа **DG1p21**:

Если свойство **HeaderPanel=true**, то:

* Для первого грида — GridMaster1, для второго — GridMaster2 и т.д.

Для любого грида применимо:

* если = 0 — грид подчиняется шапке (Header);
* если = -1 — грид подчиняется docs-у.

Случай, когда в документе есть 3 грида:

* Если **gridMaster3 = -1**, то 3-й грид подчиняется docs-у.
* Если **gridMaster3 = 0**, то 3-й грид подчиняется шапке.
* Если **gridMaster3 = 1**, то 3-й грид подчиняется первому.
* Если **gridMaster3 = 2**, то 3-й грид подчиняется второму.

Если свойство **HeaderPanel=false**, то номера X свойств каждого из гридов, описанные выше, будут действовать как X-1.

**GridHeight1** определяет размер и положение первого грида:

* Если значение > 0 — грид будет расположен снизу по отношению к шапке (или главному гриду).
* Если значение < 0 — грид будет справа.

Для остатков:

* **SoldAllowGrids=gr21a,gr21b** — указываем гриды, для которых будет открываться форма остатков.
* **SoldGRB\_CANT=cant** — указываем поле (в гриде), по которому будет суммироваться значение (например, чтобы кол-во в гриде не превысило кол-во в остатках). Также на этом поле позиционируется курсор при добавлении строки из остатков в грид.

Следующие 2 параметра работают, если в SoldAllowGrids указан только один грид. Если гридов несколько, то имена полей в гридах остатков и гридах документа должны совпадать соответственно.

* **SoldListFields=cod\_tvr,brand\_cod** — поля для выборки из грида остатков.
* **SoldRezultFields=cod\_tvr,brand** — поля для вставки в грид документа.

Для настройки второго грида в форме остатков:

* **SoldSubMaster** — определяет подчиненность второго грида в остатках (F8):
  * если = 0 — второй грид подчиняется первому;
  * если = -1 — подчиняется docs-у.
* **SoldSubMasterSize=350** — определяет размер подчиненного грида (положение вроде не меняется).

Для вкладки дополнительно:

```
[ZZZ]
XCST=true
.type.XCST=Boolean
XCST GridCount=2
.type.XCST GridCount=Integer
.Hint.XCST GridCount=<=3
XCST GridHeight1=150
.type.XCST GridHeight1=Integer
XCST GridHeight2=150
.type.XCST GridHeight2=Integer
XCST GridMaster1=-1
.type.XCST GridMaster1=Integer
XCST GridMaster2=-1
.type.XCST GridMaster2=Integer
```

Позиционирование панели инстр. (toolbar)

```
[ZZZ]
UseToolBar=true
.type.UseToolBar=Boolean
UseToolBarBottom=true
.type.UseToolBarBottom=Boolean
UseToolbarHints=false
.type.UseToolbarHints=Boolean
UseToolbarSorting=true
.type.UseToolbarSorting=Boolean
```

Будет задаваться вопрос для подтверждения:

```
[ZZZ]
ConfirmText=Generam formulele contabile?
.type.ConfirmText=String
.MISS.eng.ConfirmText=Сформировать проводки?
.MISS.rom.ConfirmText=Generam formulele contabile?
.MISS.rus.ConfirmText=Сформировать проводки?
```

Скрыть кнопку экшенов:

```
[ZZZ]
ShowActionsEnabled=false
.type.ShowActionsEnabled=Boolean
```

Параметры в экшене, загрузка файла (пример PL/SQL):

```plsql
declare
  v_nrdoc1 int;
  v_comment varchar2(100):='Loaded '||to_char(sysdate,'dd.mm.yyyy hh24:mi:ss');
  v_encoding number(10):=:encoding_def;
  v_separator char(1):=:separator_def;
  v_ROW1_DETAIL number(10):= :ROW1_DETAIL_def;
  v_ROW1_MASTER number(10):= :ROW1_MASTER_def;
  v_ROWN_MASTER number(10):= :ROWN_MASTER_def;
begin
  select nvl(max(nrdoc1),0)+1 into v_nrdoc1 from tmdb_docs_ole where nrdoc=:nrdoc;

  insert into tmdb_docs_ole (nrdoc,nrdoc1,pfile,txtcomment,oleobj)
  values (:nrdoc,v_nrdoc1,:filename,v_comment,empty_blob()) returning oleobj into :file;

  update VMDB_ORDERS_SETINGS
  set unicode=:encoding,separator=:separator,ROW1_MASTER=:ROW1_MASTER,ROWN_MASTER=:ROWN_MASTER,
      ROW1_DETAIL=:ROW1_DETAIL
  where nrdoc=:nrdoc;
end;
```

Комментарии к интерфейсу загрузки файла (внутри блока):

```
.text.file=Nume fisier:
.type.file=file
.width.file=401
.filter.file=CSV files (*.csv)|*.csv|MS Excel files (*.xls)|*.xls|All files (*.*)|*.* 
.type.filename=filename
.src.filename=file
.text.encoding= Codificarea fisierului:
.type.encoding=List,S,U,1
.def.encoding=:encoding_def
.width.encoding=150
.text.separator=Separator:
.def.separator=:separator_def
.width.separator=40
.text.ROW1_DETAIL=Primul rind din tabel
.def.ROW1_DETAIL=:ROW1_DETAIL_def
.width.ROW1_DETAIL=40
.text.ROW1_MASTER=Primul rind al caciulei
.def.ROW1_MASTER=:ROW1_MASTER_def
.width.ROW1_MASTER=40
.text.ROWN_MASTER=Ultimul rind al caciulei
.def.ROWN_MASTER=:ROWN_MASTER_def
.width.ROWN_MASTER=40

encoding_def=field_dmDG1_sq21_UNICODE
separator_def=field_dmDG1_sq21_separator
ROW1_DETAIL_def=field_dmDG1_sq21_ROW1_DETAIL
ROW1_MASTER_def=field_dmDG1_sq21_ROW1_MASTER
ROWN_MASTER_def=field_dmDG1_sq21_ROW1_MASTER
```

Экшен, который выполняет скрипт:

* На форме настроено действие "Экспорт заявки в EDI"
  * Его имя секции — ZAIAVAKA\_POSU.MAKE\_XML

Его SQL1:

```plsql
begin
  ylnl_edi_order_xml(:order);
  :batch:= 
    'move \\oravirt\\dpdump\\order-'||:order||'.xml'||
    ' X:\\EDI\\ExiteSync\\outbox'||chr(13)||chr(10)||
    'X:'||chr(13)||chr(10)||
    'cd \\EDI\\ExiteSync'||chr(13)||chr(10)||
    'main.bat';
end;
```

Комментарий:

```
order=field_fmFS1c_sq01_NRDOC
```

***

## Опции на экшене

(Direct link: https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/dokumenty/nastroika-dokumenta#h41e43f44643843843d43044d43a44843543d435)

* в xwiki

***

## Опции на печатной форме

(Direct link: https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/dokumenty/nastroika-dokumenta#h41e43f44643843843d43043f43544743044243d43e43944443e44043c435)

```
[ZZZ]
AutoOk=true
.type.AutoOk=Boolean
AutoSelect=true
.type.AutoSelect=Boolean
```

Эти два свойства используются для автоматической печати ПФ без возможности выбора из списка (т.е. список ПФ не отображается). Если использовать любое из свойств отдельно, то на этой ПФ будет ставиться галочка (автовыбор ПФ).

ПФ с шаблоном в Word:

```
[ZZZ]
DLL ID=5002
.type.DLL ID=Integer
Report ID=MSWord
.type.Report ID=String
SQL Main=.MEMO.ZZZ.SQL Main
.type.SQL Main=Memo
SQL1=.MEMO.ZZZ.SQL1
.type.SQL1=Memo
Template=perev_prof_vicet.doc
.type.Template=String
WindowCaption=Заявление на вычет
.type.WindowCaption=String
```

Пример SQL частей для печатной формы:

\[.MEMO.ZZZ.SQL Main]

```sql
select clcdtsc0t clcarendt, clcdtsc1t clcavtot,
  (select sum(suma0) from vmdb_arenda_act where nrdoc=:nrdoc) suma_tot,
  to_char(datamanual,'month') p_month,
  to_char(datamanual,'YYYY') p_year,
  c.*
from VMDB_REG r, vms_company c, vmdb_docs d
where nrdoc = :nrdoc
  and r.nrdoc = d.cod
```

\[.MEMO.ZZZ.SQL1]

```sql
select dtnum0 num_doc, descr_type clcsct, kontr clckontrt, suma0 suma
from vmdb_arenda_act
where nrdoc = :nrdoc
```

В шаблоне мастер имеет заголовок: \[\[Table1]]. Этот заголовок ОБЯЗАТЕЛЬНО должен располагаться в верхней ячейке таблицы, которая является гридом для строк мастера.

Пример:

| \[\[Table1]]    |              |              |              |   |
| --------------- | ------------ | ------------ | ------------ | - |
| \[Num\_doc] чек | \[Clckontrt] | За \[clcsct] | \[suma] руб. |   |

Каждому свойству вида **SQL1, SQL2** соответствует таблица в шаблоне с заголовком вида: **Table1, Table2**.

Чтобы корректно выпадал календарь на поле дата (заполнялось) нужно:

* в Edit query, вкладка Sagi Properties установить галочку напротив свойства:
  * **SagiModeNotAbort** — позволяет неявное редактирование

Настройка справочника в гриде VMS\_SYSS:

* Поле **Filter** можно задавать ограничение в зависимости от соседних полей и обращаться к ним через ссылку на поля соседних колонок.

Изображение (пример настройки справочника в гриде VMS\_SYSS):

![Настройка справочника в гриде VMS\_SYSS](<../../../.gitbook/assets/image (9)>)
