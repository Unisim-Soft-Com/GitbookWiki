# Печатные формы (PrintForms)

Объекты PrintForms служат для настройки печатных форм из документов.

Список печатных форм отображается в окне \[Document Action] при нажатии кнопки печати в документах соответствующего типа в клиентском приложении Universal Accounting.

Обычно в поддереве документа они объединены в группу и являются субузлами логического узла \[PrintForms].

Объекты типа PrintForms поддерживают все TXT‑свойства отчетов (свойства отчетов в текстовом формате).

***

## Основные свойства объекта типа PrintForms

| Имя свойства               |     Тип | Описание                                                                                                                                                                                                                                                                                                                                  | Значение для примера                            |
| -------------------------- | ------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| DLL ID                     | Integer | Идентификационный номер DLL                                                                                                                                                                                                                                                                                                               | 5002                                            |
| Index Fields               |  String |                                                                                                                                                                                                                                                                                                                                           |                                                 |
| Master Fields              |  String |                                                                                                                                                                                                                                                                                                                                           |                                                 |
| Report ID                  |  String | Идентификатор печатной формы в DLL. В печатной форме накладной при RowsInInvoice=30 будет просто ограничивать, но когда строк меньше, пустые добавлять не будет.                                                                                                                                                                          | 3                                               |
| Report Type                |  String | Типы отчетов: FormulaOne, ExcelGL2, FastReport, MSWord                                                                                                                                                                                                                                                                                    | MSWord                                          |
| SQLDetail                  |    Memo | Запрос, возвращающий данные в область Detail (область данных подчиненной таблицы) печатной формы                                                                                                                                                                                                                                          |                                                 |
| SQLHeader                  |    Memo | Запрос, возвращающий данные в область Header (область заголовка) печатной формы                                                                                                                                                                                                                                                           | `SELECT * FROM OTP WHERE NRDOC = :NRDOC --5654` |
| SQLMaster                  |    Memo | Запрос, возвращающий данные в область Master (область данных главной таблицы) печатной формы                                                                                                                                                                                                                                              | `SELECT 1 FROM DUAL`                            |
| Template                   |  String | Шаблон, используемый для генерации печатной формы                                                                                                                                                                                                                                                                                         | otpusk1.doc                                     |
| WindowCaption              |  String | Подпись окна с генерированной печатной формой                                                                                                                                                                                                                                                                                             | Отпуск (Текущий работник)                       |
| SQLAllInOne                |    Memo | Настройка печатной формы. Отправить письмо с вложением через ms outlook при нажатии на кнопку (экспорт в Excel). (начиная с версии una 4.1.5.039)                                                                                                                                                                                         | (см. скрипт ниже)                               |
| F1AutoPrint                |  String | Количество копий (3) при печати, если нажимать не стандартный значок принтера, а другой, который расположен четвертой кнопкой справа. Можно вместо 1:3 указывать 1,3,5 - это прямо номера листов для печати, когда их подразумевается много. Но сейчас такое почти не встречается. пример есть на gcc (gcc1) @ ora64 sf=42072 f1autoprint | 1:3                                             |
| F1PrintCopies              | Integer | Количество копий при печати                                                                                                                                                                                                                                                                                                               | 3                                               |
| PrintXL                    | Boolean | Кнопочка Принтер в печ.форме работает как кнопочка "принтера со значком Х (экселя)"                                                                                                                                                                                                                                                       | true                                            |
| DontEditReport             | Boolean | Запрет редактирования отчета перед печатью. Запрет экспорта в Excel.                                                                                                                                                                                                                                                                      | true                                            |
| SQLBeforePrint             |    Memo | При нажатии на принтер из печатной формы/отчета выполнится скрипт из этого свойства                                                                                                                                                                                                                                                       |                                                 |
| PrintRepeatMasterGrid      |  String |                                                                                                                                                                                                                                                                                                                                           | gr21b                                           |
| PrintRepeatMasterGridField |  String | Для множественной печати                                                                                                                                                                                                                                                                                                                  | PRM2                                            |
| DisableGotoNrdoc           | Boolean | Нельзя прыгать из печатной формы в документ                                                                                                                                                                                                                                                                                               | true                                            |
| ButtonIndex                | Integer | Нельзя прыгать из печатной формы в документ                                                                                                                                                                                                                                                                                               | true                                            |
| ButtonText                 |  String | Кнопка для вызова печатной формы будет на тулбаре номер 1 по счету                                                                                                                                                                                                                                                                        | 1                                               |
| Param\_NRDOC               |  String | Для этой печатной формы запоминается значение поля nrdoc из header-а и в SQLBeforePrint к нему можно обратиться через :f1\_nrdoc нужно чтобы в header было поле nrdoc                                                                                                                                                                     | Текст\_на\_кнопке                               |
| ViewOnly                   | Boolean | Эта форма будет видна и из журнала (в EasyInterface), то есть даже когда мы не в документе                                                                                                                                                                                                                                                | header.nrdoc                                    |
| StreamToDoc                | Boolean |                                                                                                                                                                                                                                                                                                                                           | true                                            |
| Stream\_Invisible          | Boolean |                                                                                                                                                                                                                                                                                                                                           | true                                            |
| frxStreamExt               |  String |                                                                                                                                                                                                                                                                                                                                           | .pdf                                            |
| frxEmbeddedFonts           | Boolean |                                                                                                                                                                                                                                                                                                                                           | true                                            |

***

## Дублирование печатных форм документа

Задача: создать для документа печатные формы, идентичные печатным формам другого документа.

{% stepper %}
{% step %}
### Шаг 1

Найти в дереве документов документ с требуемыми печатными формами.
{% endstep %}

{% step %}
### Шаг 2

Выбрать узел PrintForms с субузлами – печатными формами этого документа.
{% endstep %}

{% step %}
### Шаг 3

Экспортировать этот узел с субузлами:

Меню: \[Экспорт / Импорт] → \[Экспорт] → \[Текущий (Все)] → \[Ини (стд.)].
{% endstep %}

{% step %}
### Шаг 4

Выбрать документ, для которого требуется продублировать печатные формы (уровень документа).
{% endstep %}

{% step %}
### Шаг 5

Импортировать печатные формы:

Меню: \[Экспорт / Импорт] → \[Вставить] → \[Как новый субузел].

В окне \[Выбор узла из шаблона] включить флажок \[Выбрать с вложенными узлами].
{% endstep %}

{% step %}
### Шаг 6

Зафиксировать изменения в базе данных.
{% endstep %}
{% endstepper %}

***

## Прочие настройки и советы

* Если нужна одна дата, а не период: установить свойство SingleDate=true.
* Включение дополнительной панели элементов: PanelHeightMaster=100\
  (PanelHeightMaster = -100 — панель будет справа)
* Фильтры на шапке формы:
  * FilterSc1Visible=true
  * FilterSc1Caption=’Название’
  * FilterScVisible=true
  * FilterScCaption=’Название’
  * FilterDEPVisible=true
  * FilterDEPCaption=’Название’
* Количество фильтров по дате:
  * DateCount=2
* Включение тулбара над гридом:
  * UseToolbar=true — свойство самого документа или формы.
* ButtonText="\[Заполнить]" — добавляется в caption. При нажатии в аккаунте на кнопку \[Заполнить], расположенную на тулбаре, выполнится caption, в котором определено свойство ButtonText="\[Заполнить]".
* HeaderPanel=true — включение шапки.
*   Вычисление итогов для грида:

    * XTT1=SUMA — Суммирование значений грида.
    * XCST=true
    * XCST GridCount=1
    * XCST Summary1= DTCANT4

    Для отображения суммы в клиенте необходимо в дизайне (ALT+D) в настройках грида (кнопка Grid) включить ShowSummary и включить SaveProps.\
    В Редакторе запросов (ALT+Q) на вкладке SagiProperties включить XTTShowSummary.
* Автообновление формы (время указывается в сек.):
  * \[ZZZ]
  * RefreshPanelVisible=true
  * RefreshTimerEnabled=true
  * .type.RefreshTimerEnabled=Boolean
  * RefreshTimerInterval=5
  * .type.RefreshTimerInterval=Integer
* Свойство DatePrefix=имя (например V\_) необходимо для последующего обращения к датам:
  * sys\_context('ENVUN4','V\_DATAB')
  * sys\_context('ENVUN4','V\_DATAF')

***

## Настройка подчиненных гридов в форме

(См. оригинальную секцию по настройке подчиненных гридов.)\
Прямая ссылка: https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/dokumenty/pechatnye-formy-printforms#h41d43044144244043e43943a43043f43544743044243d43e43944443e44043c44b

***

## Отправка письма с вложением через MS Outlook при нажатии на кнопку (экспорт в Excel)

(начиная с версии una 4.1.5.039)

Пример вызова:

```
ylin_docs.zaiav_list_xl(:nrdoc, :SQLHeader, :SQLMaster, :SQLDetail, :XLSCRIPT);
```

<details>

<summary>XLSCRIPT (пример)</summary>

XLSCRIPT := 'Sub start()'

CHR(10) 'Dim OutApp As Object'

CHR(10) 'Dim OutMail As Object'

CHR(10) 'Set OutApp = CreateObject("Outlook.Application")'

CHR(10) 'Set OutMail = OutApp.CreateItem(0)'

CHR(10) 'On Error Resume Next'

CHR(10) 'With OutMail'

CHR(10) '.to = "'v\_mail' "'

CHR(10) '.CC = "'v\_mail\_cc' "'

CHR(10) '.BCC = "'v\_mail\_bcc' "'

CHR(10) '.Subject = "Заявочный лист"'

CHR(10) '.Body = "'v\_body' "'

CHR(10) '.Attachments.Add ActiveWorkbook.FullName'

CHR(10) '.Display'

CHR(10) 'End With'

CHR(10) 'Set OutMail = Nothing'

CHR(10) 'Set OutApp = Nothing'

CHR(10) 'End Sub';

</details>

***

Last updated 1 year ago
