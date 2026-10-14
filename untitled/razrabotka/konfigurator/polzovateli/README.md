# Пользователи

В программе существует несколько групп пользователей с разными правами доступа, которые можно редактировать. В зависимости от группы пользователь получает соответствующий набор прав. Управление группами и правами выполняет системный администратор либо программист по согласованию с администрацией компании‑клиента.

Администратор имеет полный доступ ко всем разделам программы, может изменять настройки, создавать и удалять пользователей, назначать права и изменять их свойства.

Ниже приведены свойства, необходимые для создания и настройки учетных записей пользователей. Свойства разделены на обязательные и дополнительные. В примерах также указаны типы и примерные значения.

## Обязательные свойства

<table><thead><tr><th width="209.22216796875" align="center">Название свойства</th><th align="right">Тип</th><th>Описание</th><th>Значение для примера</th></tr></thead><tbody><tr><td align="center">Enabled</td><td align="right">Boolean</td><td>true — учетная запись активна (видима приложению Universal Accounting). false — объект игнорируется.</td><td>true</td></tr><tr><td align="center">ID</td><td align="right">Integer</td><td>Идентификационный номер пользователя (соответствует значению поля [UserID] таблицы документов).</td><td>1001</td></tr><tr><td align="center">UserName</td><td align="right">String</td><td>Логин пользователя. Вводится в поле UserID при запуске приложения Universal Accounting.</td><td>petrov</td></tr><tr><td align="center">Encoded</td><td align="right">Integer</td><td>(Авто) Закодированный пароль пользователя.</td><td></td></tr><tr><td align="center">PassDate</td><td align="right">Date</td><td>(Авто) После определения пароля автоматически проставляется дата.</td><td></td></tr></tbody></table>

## Дополнительные свойства

> Примечание: список очень длиний; приведены названия, типы, краткое описание и примерные значения там, где они указаны в исходном тексте.

| Название свойства          |     Тип | Описание                                                                                                              | Значение для примера                                          |
| -------------------------- | ------: | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| Admin                      |  String | Если значение = 1, то пользователь обладает правами администратора.                                                   | 1                                                             |
| AllowGridDesign            | Boolean | Разрешить изменение дизайнов (для не‑админов, которым нужно менять дизайны).                                          | true                                                          |
| AutoFreeMemory             | Boolean | Выгрузка неиспользуемых DLL/BPL из памяти.                                                                            | true                                                          |
| Familia Numele Prenumele   |  String | Фамилия, имя, отчество (информативное поле).                                                                          | Петров Иван Сергеевич                                         |
| ConfirmExit                | Boolean |                                                                                                                       | false                                                         |
| InitSQL                    |    Memo | Права, прописанные программно в коде программы.                                                                       | (см. ниже)                                                    |
| LACSetupBlockSections      |  String | Список журналов/справочников, находящихся на верхней функциональной панели; объекты, скрытые от группы пользователей. | J\_MATERIAL ,J\_CONFIRMAR E, ...                              |
| LACSetupBlockSections\_old |  String |                                                                                                                       | 0:0:ActeOrdere,0:1:ActeOrdere, f\_ruta\_agent,f\_ruta\_client |
| PeriodStart                |  String | Период, с которого пользователь имеет право видеть документы. Допускается SQL-выражение.                              | 01.01.2012                                                    |
| PeriodEnd                  |  String | Частная дата окончания периода редактирования документов.                                                             | 01.12.2012                                                    |
| PeriodFinish               |  String | Период окончания, с которого пользователь не имеет право видеть документы.                                            | 01.12.2012                                                    |
| PassAttempts               | Integer | Количество попыток ввода неправильного пароля.                                                                        | 5                                                             |
| LACReportsSelectedOnly     | Boolean | Интерпретировать LacSetupBlockReports как список разрешенных секций.                                                  | true                                                          |
| LACSetupBlockReports       |  String | Список секций отчетов, которые пользователю видеть запрещено.                                                         | R\_MATERIAL                                                   |
| LACSetupBlockObjects       |  String | Список объектов, с которыми пользователю работать запрещено.                                                          | NRSET                                                         |
| LACSectionsSelectedOnly    | Boolean | Интерпретировать LACSetupBlockSections как список разрешенных секций.                                                 | true                                                          |
| LACObjectsSelectedOnly     | Boolean | Интерпретировать LACSetupBlockObjects как список разрешенных секций.                                                  | true                                                          |
| Language                   |  String | Язык интерфейса. 0 — англ., 1 — рум., 2 — рус. По умолчанию 1 (рум.).                                                 | 2                                                             |
| DataEmpty                  | Boolean | Если True — игнорируется значение по умолчанию поля \[Дата] при вводе документов.                                     | false                                                         |
| DesignGroup                | Integer | Номер группы дизайнов (позволяет иметь персональные дизайны, переводы и т.п.).                                        |                                                               |
| Password                   |  String | Пароль пользователя. Вводится в поле Password при запуске приложения Universal Accounting.                            |                                                               |
| seqNRMANDisableChanges     | Boolean | Запретить пользователю изменять поле NRMANUAL.                                                                        | true                                                          |
| DEF\_JOURNAL               |  String | Журнал (фильтр на документы), устанавливаемый по умолчанию.                                                           | J\_BANK                                                       |
| Docs View Mode             |  String | 0 — All documents; 1 — All group documents; 2 — Private documents.                                                    | 2                                                             |
| Docs edit mode             | Integer | 0 — All documents; 1 — All group documents; 2 — Private documents.                                                    | 2                                                             |
| DivVisible                 | Boolean |                                                                                                                       | false                                                         |
| GridPropCacheLimit         | Integer | Размер кеша дизайнов (единица: тип документа/узел/форма/справочник).                                                  | 100                                                           |
| GridDisableNumberSearch    | Boolean | Режим текстового поиска даже в числовых полях грида.                                                                  | true                                                          |
| RepairGridDesign           | Boolean | Автокоррекция загружаемых дизайнов (для ORACLE 9i).                                                                   | true                                                          |
| RepDataStart               |  String | Дата начала периода просмотра данных в отчетах. Если отсутствует — используется PeriodStart.                          |                                                               |
| RepDataEnd                 |  String | Дата окончания периода просмотра данных в отчетах. Если отсутствует — используется PeriodEnd.                         |                                                               |
| ReportTreeSorting          | Boolean | Сортировка узлов дерева отчетов по алфавиту.                                                                          | true                                                          |
| StartupReportNode          |  String | Стартовый узел для дерева отчетов.                                                                                    |                                                               |
| RepTestRecordCount         | Boolean | Проверять количество записей отчета (F1Reports).                                                                      | true                                                          |
| RepDeleteTempTables        | Boolean | Удалять временные таблицы ORACLE после построения отчета.                                                             | true                                                          |
| LangDontLoad               | Boolean | Не загружать переводы из ORACLE (для уменьшения трафика).                                                             | true                                                          |
| LoadCaptionsSep            | Boolean | Раздельная загрузка переводов заголовков столбцов и дизайнов.                                                         | true                                                          |
| UserGroupList              |  String | Список кодов пользователей (через запятую), составляющих группу (для Docs View/Docs edit mode).                       | 1,2,3,4,7,15                                                  |
| UseDotInCont               | Boolean | Использовать точку в значении счета (формат 99.99).                                                                   | true                                                          |
| UseSmartTab                | Boolean | "Умный" Tab — переход по полям окна.                                                                                  | true                                                          |
| UseSpeedSearch             | Boolean | Быстрый поиск в выпадающих справочниках.                                                                              | true                                                          |
| UseSmartEnter              | Boolean | "Умный" Enter на цифровой клавиатуре: переход к следующему полю/вставка новой записи.                                 | true                                                          |
| UseSmartEnterNotebook      | Boolean |                                                                                                                       | true                                                          |
| UnivListReadOnly           | Boolean |                                                                                                                       | false                                                         |
| SmartEnterLikeTab          | Boolean |                                                                                                                       | true                                                          |
| USER\_SC                   | Integer | Код пользователя из универс. Получение: sys\_context('envun4','param\_user\_sc')                                      | 25820                                                         |
| UseCMX                     | Boolean |                                                                                                                       | false                                                         |
| PassUnique                 | Boolean | Разрешено ли повторять пароль для пользователя/ей.                                                                    | false                                                         |
| ToolBarFormSections        |  String | Пример 2‑уровневого меню форм (включая переводы).                                                                     | \*Producte,F\_PROD\_GR,...                                    |
| ToolBarFormSections\_      |  String |                                                                                                                       | \*Producte,F\_PROD\_GR,...                                    |
| ToolBarFormSections\_\_    |  String |                                                                                                                       | F\_PROD\_GR,F\_PRODUCTS,...                                   |
| TBDocCmd                   | Boolean |                                                                                                                       | true                                                          |
| TBForms                    | Boolean |                                                                                                                       | false                                                         |
| HideErrorLevel             | Integer | 2 — все ошибки показываются в статус баре; 1 — все, кроме msg.                                                        | 2                                                             |
| HideMenuDict               | Boolean | Отображение меню "Справочники" (по умолчанию включено).                                                               | true                                                          |
| HideMenuReps               | Boolean | Отображение меню "Отчеты".                                                                                            | true                                                          |
| HideMenuForms              | Boolean | Отображение меню "Формы".                                                                                             | true                                                          |
| ViewFromToday              | Integer | Ограничение периода (смещение дней назад от текущей даты).                                                            |                                                               |
| ViewBegin                  |  String | Минимальная дата отображения документов.                                                                              |                                                               |
| ViewEnd                    |  String | Максимальная дата отображения документов.                                                                             |                                                               |
| LastRecord                 | Boolean | При открытии журнала переходить к последнему видимому документу.                                                      | true                                                          |
| ORDER BY                   |  String | Порядок сортировки документов (список полей, через запятую).                                                          |                                                               |
| OraLoaderModeDML           | Boolean | Использовать DML при загрузке данных из текстового файла/BDE.                                                         | true                                                          |
| DataAutomat                | Boolean | Автозаполнение даты документов на основании предыдущего документа.                                                    | true                                                          |
| DataCurrent                | Boolean | Автозаполнение даты документов на основании текущей даты.                                                             | true                                                          |
| DataEmpty                  | Boolean | Отменить автозаполнение поля DATAMANUAL для пользователя.                                                             | true                                                          |
| PXCMSimpleEditing          | Boolean | Режим быстрой правки проводок документов версии PX.                                                                   | true                                                          |
| Backup                     | Boolean | Сохранение документов в архив перед удалением.                                                                        | true                                                          |
| XDEF\_BGFILTER             |  String | Начальное значение фильтра по NrSet (список кодов или \*).                                                            | 1,2,3,1226                                                    |
| XDEF\_NRSET                |  String | NrSet по умолчанию.                                                                                                   |                                                               |
| XDEF\_NRSET\_VIEW          |  String | Список кодов NrSet, которыми ограничиваются права пользователя.                                                       |                                                               |
| HideNrsetFilter            | Boolean | Скрыть фильтр по NrSet.                                                                                               | true                                                          |
| \_\_XDEF\_NRSET            | Integer |                                                                                                                       | 201                                                           |

Параметры панелей инструментов:

| Название     |     Тип | Описание                                                                                                                                | Пример |
| ------------ | ------: | --------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| TBIconStyle  | Integer | Положение значков относительно пункта меню: 0 — не выводить; 1 — только значки; 2 — значки слева от надписей; 3 — значки над надписями. | 3      |
| TBIconSize   | Integer | Размер значков в главном меню: 0 — мелкие; 1 — средние; 2 — крупные.                                                                    | 2      |
| TBPeriod     | Boolean | Отображать панель ввода периодов.                                                                                                       | true   |
| TBWindowList | Boolean | Отображать панель открытых окон.                                                                                                        | true   |

Множество дополнительных флагов для скрытия элементов интерфейса (HideDocPreview, HideDocsActive, HideDocsBarCode, HideDocsDesign, ..., HideToolSys и др.) — большинство имеют тип Boolean и в примерах часто выставлены в true/false (см. исходный список).

Некоторые другие параметры и значения (часть с инструментами/панелями/скрытием меню):

| Название            |     Тип | Пример                               |
| ------------------- | ------: | ------------------------------------ |
| GotoDocumentEditing | Boolean | true                                 |
| HideMenu            | Boolean | true (скрытие пункта меню "Журналы") |
| HideMenuJrnlStd     | Boolean | true                                 |
| TBJournals          | Boolean | true                                 |
| BG\_FILTER\_SECTION |  String | 1                                    |
| HideDocGrid         | Boolean | false                                |
| HideNrsetFilte      | Boolean | false                                |
| HideToolbar         | Boolean | false                                |

InitSQL — примеры

```pascal
begin:res:=2; envun4.EnvSetValue ('restricted_syss_tip','tip in (''R'') and cod in (502,18,61)'); envun4.EnvSetValue('restricted_syss_tip', 'tip in (''S'') and cod in (14)');end;
```

и

```pascal
begin :res:=2; Bg_Policy.INITFILTER_NRSET_TREE ('ID IN (1,2,3)');end;
```

***

## Действия над учетными записями в конфигураторе UniConf

Свойства, установленные для группы пользователей, распространяются на всех пользователей группы.

* Создание учетной записи пользователя:\
  https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/polzovateli/sozdanie-uchetnoi-zapisi-polzovatelya

Иногда полезно временно получить права админа под текущим пользователем — комбинация клавиш Ctrl+F12. Запрашиваемый пароль настраивается в Settings -> General свойством Tmpadminpass.

| Название свойства |    Тип | Описание                                                   | Пример |
| ----------------- | -----: | ---------------------------------------------------------- | ------ |
| Tmpadminpass      | String | Временные права админа под текущим пользователем (пароль). | aaa    |

Дополнительные настройки доступа и подсказки:

* Настройка ограничения доступа на изменение универсального справочника:\
  https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/polzovateli/nastroika-ogranicheniya-dostupa-na-izmenenie-universalnogo-spravochnika
* Настройка ограничения доступа к проводкам (tmdb\_cm):\
  https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/polzovateli/nastroika-ogranicheniya-dostupa-k-provodkam

Подсказки / полезные ссылки:

<details>

<summary>Полезные подсказки и материалы</summary>

* Как скрыть пароль:\
  https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/polzovateli/kak-skryt-parol
* Настройка прав на редактирование справочников UNIVERS:\
  https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/polzovateli/nastroika-ogranicheniya-dostupa-na-izmenenie-universalnogo-spravochnika
* Настройка прав на редактирование справочников SYSS:\
  https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/spravochniki/syss/cherez-vremennuyu-tablicu-tms\_syss\_unlock
* Интерфейс:\
  https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/polzovateli/interfeis
* Ограничения паролей пользователей:\
  https://unisim-soft.gitbook.io/wiki/razrabotka/konfigurator/polzovateli/ogranichenie-parolei-polzovatelei

</details>

Последнее обновление исходного материала: 1 year ago.
