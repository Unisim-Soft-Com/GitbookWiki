# Интерфейс

## Общие свойства

| Название свойства   | Тип     | Описание                                                                  | Значение для примера                                                                                                    |
| ------------------- | ------- | ------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| TBForms             | Boolean | Отобразить тулбар Формы: все секции из ToolBarFormSections.               | false                                                                                                                   |
| TBJournals          | Boolean | Отобразить тулбар Журналы. Меню журналы выводится в строку.               | true                                                                                                                    |
| TBWindowList        | Boolean |                                                                           | false                                                                                                                   |
| TBDocCmd            | Boolean |                                                                           | true                                                                                                                    |
| TBPeriod            | Boolean | Отобразить тулбар Период: текущая дата, перод просмотра и редактирования. | true                                                                                                                    |
| TBIconSize          | String  |                                                                           | 3                                                                                                                       |
| TBIconStyle         | String  |                                                                           | 2                                                                                                                       |
| ToolBarFormSections | String  | Список секций, которые будут отображены в тулбаре формы                   | \*Producte,F\_PROD\_GR, F\_PRODUCTS, \*"Cliente,Клиенты", F\_CLIENTS, F\_AGENTS, _Rute,F\_ROUTES, F\_RUTE\_DESF,_,F\_UM |

***

## Скрыть элементы пользовательского интерфейса

Скрыть элементы пользовательского интерфейса можно с помощью свойств Hide. Ниже перечислены группы свойств с описанием и изображениями.

### Пункты главного меню

| Имя свойства      | Тип     | Описание                                | Внешний вид                                  |
| ----------------- | ------- | --------------------------------------- | -------------------------------------------- |
| HideMenuDoc       | Boolean | Действия над документом                 | ![](<../../../.gitbook/assets/image (1077)>) |
| HideMenuDict      | Boolean | Справочники                             | ![](<../../../.gitbook/assets/image (1078)>) |
| HideMenuSysS      | Boolean | Справочник SysS (по умолчанию включено) | ![](<../../../.gitbook/assets/image (1079)>) |
| HideMenuReps      | Boolean | Отчеты                                  | ![](<../../../.gitbook/assets/image (1080)>) |
| HideMenuRepSelect | Boolean | Дерево отчетов в меню "Отчеты"          |                                              |
| HideMenuForms     | Boolean | Формы                                   | ![](<../../../.gitbook/assets/image (1081)>) |
| HideMenuUtil      | Boolean | Сервис                                  | ![](<../../../.gitbook/assets/image (1082)>) |
| HideMenuWindow    | Boolean | Окна                                    | ![](<../../../.gitbook/assets/image (1083)>) |
| HideMenuHelp      | Boolean | Помощь                                  | ![](<../../../.gitbook/assets/image (1083)>) |
| HideMenuJrnlStd   | Boolean | Скрывает журнал Все, если true          |                                              |

***

### Кнопки на главной панели инструментов

| Имя свойства        | Тип     | Описание                | Внешний вид                                                                               |
| ------------------- | ------- | ----------------------- | ----------------------------------------------------------------------------------------- |
| HideToolBar         | Boolean | Вся панель инструментов |                                                                                           |
| HideToolNavi        | Boolean | Навигатор               | ![](<../../../.gitbook/assets/image (1084)>)                                              |
| HideToolLang        | Boolean | Языки                   | ![](<../../../.gitbook/assets/image (1085)>) ![](<../../../.gitbook/assets/image (1086)>) |
| HideToolSet         | Boolean | Галочки                 | ![](<../../../.gitbook/assets/image (1087)>)                                              |
| HideToolCalc        | Boolean | Калькулятор             | ![](<../../../.gitbook/assets/image (1088)>)                                              |
| HideToolMsg         | Boolean | Сообщения               | ![](<../../../.gitbook/assets/image (1089)>)                                              |
| HideToolSys         | Boolean | Второй клиент           |                                                                                           |
| HideToolInf         | Boolean | Имя сервера             | ![](<../../../.gitbook/assets/image (1090)>)                                              |
| HideToolOrder       | Boolean | Авто-заявка             |                                                                                           |
| BG\_FILTER\_SECTION | Boolean | Управление NRSET        |                                                                                           |
| DivVisible          | Boolean | Выбор филиала           | ![](<../../../.gitbook/assets/image (1091)>)                                              |
| FMEnabled           | Boolean | Управление F/M          | ![](<../../../.gitbook/assets/image (1092)>)                                              |
| FOnlyEnabled        | Boolean | Красная кнопка F/M      | ![](<../../../.gitbook/assets/image (1093)>)                                              |

***

### Информация на строке состояния

| Имя свойства  | Тип     | Описание             | Внешний вид                                  |
| ------------- | ------- | -------------------- | -------------------------------------------- |
| HideStatusBar | Boolean | Вся строка состояния | ![](<../../../.gitbook/assets/image (1094)>) |
| HideMemory    | Boolean | Индикатор памяти     | ![](<../../../.gitbook/assets/image (1095)>) |

***

### Кнопки на панели управления выбранным документом

| Имя свойства     | Тип     | Описание                             | Внешний вид                                                                                |
| ---------------- | ------- | ------------------------------------ | ------------------------------------------------------------------------------------------ |
| HideDocsEditare  | Boolean | Кнопка редактирования документа      | ![](<../../../.gitbook/assets/image (1096)>)                                               |
| HideDocsLich     | Boolean | Две кнопки удаления проводок         | ![](<../../../.gitbook/assets/image (1097)>) ![](<../../../.gitbook/assets/image (1098)>)  |
| HideDocsDublare  | Boolean | Кнопка дублирования документа        | ![](<../../../.gitbook/assets/image (1099)>)                                               |
| HideDocsDeriva   | Boolean | Кнопка "Документ на основании"       | ![](<../../../.gitbook/assets/image (1100)>)                                               |
| HideDocsTotals   | Boolean | Кнопка просмотра итогов              | ![](<../../../.gitbook/assets/image (1101)>), ![](<../../../.gitbook/assets/image (1102)>) |
| HideDocsWizard   | Boolean | Кнопка мастера (по умолчанию скрыта) |                                                                                            |
| HideDocsSpec     | Boolean | Кнопка Special Actions               | ![](<../../../.gitbook/assets/image (1103)>)                                               |
| HideDocsActive   | Boolean | Кнопка активации/дезактивации        | ![](<../../../.gitbook/assets/image (1104)>)                                               |
| HideDocsFact     | Boolean | Кнопка окна фактуры                  | ![](<../../../.gitbook/assets/image (1105)>)                                               |
| HideDocsSold     | Boolean | Кнопка окна остатков                 | ![](<../../../.gitbook/assets/image (1106)>)                                               |
| HideDocsBarCode  | Boolean | Кнопка окна считывателя штрих кодов  |                                                                                            |
| HideDocsDesign   | Boolean | Кнопка настройки дизайна CST         | ![](<../../../.gitbook/assets/image (1107)>)                                               |
| HideDocsLang     | Boolean | Кнопка настройки переводов           | ![](<../../../.gitbook/assets/image (1108)>)                                               |
| HideDocsHeadLine | Boolean | Цветная полоса над документом        | ![](<../../../.gitbook/assets/image (1109)>)                                               |

***

### Ярлычки вкладок документа

| Имя свойства         | Тип     | Описание             | Внешний вид                                  |
| -------------------- | ------- | -------------------- | -------------------------------------------- |
| HideDocsTabCM        | Boolean | Вкладка "Проводки"   | ![](<../../../.gitbook/assets/image (1110)>) |
| HideDocsTabMain      | Boolean | Вкладка "Специфика"  |                                              |
| HideDocsTabAdd       | Boolean | Вкладка "Информация" | ![](<../../../.gitbook/assets/image (1111)>) |
| HideDocsTabObj       | Boolean | Вкладка "Объект"     | ![](<../../../.gitbook/assets/image (1112)>) |
| HideDocsTabLog       | Boolean | Вкладка "История"    | ![](<../../../.gitbook/assets/image (1113)>) |
| HideDocsTabXL        | Boolean | Вкладка "Excel"      | ![](<../../../.gitbook/assets/image (1114)>) |
| UseCMX (секция Docs) | Boolean | Вкладка CMX          |                                              |

***

Если нужно, могу преобразовать каждую группу в отдельную страницу или добавить описания значений по умолчанию.
