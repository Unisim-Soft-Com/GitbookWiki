# Глобальные настройки

Способы задания глобальных настроек

* File: Файл "startup.ini" — текстовый файл в каталоге запуска программы. Имеет самый низкий приоритет, но некоторые параметры можно задать только в этом файле. Если в каталоге WINDOWS существует файл "un4.ini", то он будет использован вместо файла "startup.ini" в каталоге запуска программы.
* Sys: Раздел "System settings" — группа секций администратора, в которой задаются настройки программы, общие для всех пользователей и групп. По умолчанию используется секция "General". Имеет более высокий приоритет. Многие параметры можно задать только здесь.
* Grp: Секция группы пользователей — секция администратора, где обычно задаются атрибуты прав пользователей. Имеет еще более высокий приоритет.
* Usr: Секция пользователя — секция администратора, где описываются атрибуты пользователя системы. Имеет самый высокий приоритет среди постоянных способов задания.
* Mnu: Меню программы — во время выполнения программы можно менять некоторые параметры. Имеет наивысший приоритет, но время действия настроек ограничено сеансом.

Полный список всех глобальных настроек Ниже сгруппированы параметры по смысловым разделам. Ссылки на исходные якоря сохранены без изменений.

Language

* Language — String. Язык интерфейса задается либо цифрой (0,1,2), либо буквой (E, M, R). Язык окна регистрации задается только методом File. Если язык не задан ни одним из методов, система переводов выключается на весь сеанс работы. Удобно ввести это свойство в Администраторе как список значений: \[ZZZ] Language=2 .type.Language=Integer .listValue.Language=0,1,2 .listTextValue.Language=English,Moldavian,Russian Ссылка: [Language](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_Language)

Загрузка настроек, дизайнов, переводов и т.п.

* LogParams (Boolean) — режим записи в текстовый файл всех считываемых настроек (до и после обработки и фильтрации). Ссылка: [LogParams](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LogParams)
* NewDesignMethod (Boolean, default true) — режим быстрой загрузки настроек и дизайнов (использование хранимых процедур и меток времени). Требуется новый пакет ORACLE UN$USERPARAMS. Ссылка: [NewDesignMethod](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_NewDesignMethod)
* UsePackedIni (Boolean) — режим загрузки настроек в запакованном виде. Требуется новый пакет ORACLE UN$USERPARAMS и запущенный сервер упаковки PackSrv. Ссылка: [UsePackedIni](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_UsePackedIni)
* TardyLoading (Boolean) — отложенная загрузка настроек (напр., настройки отчетов загружаются только при первом открытии менеджера отчетов). Ссылка: [TardyLoading](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_TardyLoading)
* UseLocalCache (Boolean) — использование файлового кеша для сохранения настроек и дизайнов. Ссылка: [UseLocalCache](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_UseLocalCache)
* GridPropCacheLimit (Integer) — максимальный размер кеша дизайнов в памяти (единица = один тип документа, один узел дерева отчетов, одна форма или справочник). Ссылка: [GridPropCacheLimit](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_GridPropCacheLimit)
* RepairGridDesign (Boolean) — автокоррекция загружаемых дизайнов (иногда нужна при работе с ORACLE 9i). Ссылка: [RepairGridDesign](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_RepairGridDesign)
* LangDontLoad (Boolean) — не загружать переводы из ORACLE (для уменьшения трафика). Ссылка: [LangDontLoad](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LangDontLoad)
* LoadCaptionsSep (Boolean) — раздельная загрузка переводов заголовков столбцов и дизайнов (совместимость с предыдущими версиями). Ссылка: [LoadCaptionsSep](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LoadCaptionsSep)

Ограничение прав пользователей (параметры, анализируются только секции пользователей и групп)

* ADMIN (Integer) — ненулевое значение даёт права администратора. Ссылка: [ADMIN](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_ADMIN)
* AllowGridDesign (Boolean) — разрешить изменение дизайнов для неадминистраторов. Ссылка: [AllowGridDesign](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_AllowGridDesign)
* DesignGroup (Integer) — номер группы дизайнов (ненулевое значение позволяет иметь персональные дизайны, переводы и т.п.). Администратор может менять во время выполнения. Ссылка: [DesignGroup](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_DesignGroup)
* LACSetupBlockSections (String) — список секций форм и справочников, которые пользователю видеть запрещено. Ссылка: [LACSetupBlockSections](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LACSetupBlockSections)
* LACSetupBlockReports (String) — список секций отчетов, которые пользователю видеть запрещено. Ссылка: [LACSetupBlockReports](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LACSetupBlockReports)
* LACSetupBlockObjects (String) — список объектов, с которыми пользователю работать запрещено. Ссылка: [LACSetupBlockObjects](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LACSetupBlockObjects)
* LACSectionsSelectedOnly (Boolean) — интерпретировать LACSetupBlockSections как список разрешённых секций. Ссылка: [LACSectionsSelectedOnly](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LACSectionsSelectedOnly)
* LACReportsSelectedOnly (Boolean) — интерпретировать LACSetupBlockReports как список разрешённых секций. Ссылка: [LACReportsSelectedOnly](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LACReportsSelectedOnly)
* LACObjectsSelectedOnly (Boolean) — интерпретировать LACSetupBlockObjects как список разрешённых секций. Ссылка: [LACObjectsSelectedOnly](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LACObjectsSelectedOnly)
* seqNRMANDisableChanges (Boolean) — запретить пользователю изменять поле NRMANUAL. Ссылка: [seqNRMANDisableChanges](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_seqNRMANDisableChanges)
* GlobalPeriodStart / GlobalPeriodEnd (String) — общие даты начала/конца периода редактирования документов (допускаются SQL-выражения). Ссылки: [GlobalPeriodStart](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_GlobalPeriodStart), [GlobalPeriodEnd](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_GlobalPeriodEnd)
* PeriodStart / PeriodEnd (String) — частные даты начала/конца периода редактирования документов (допускаются SQL-выражения). Если отсутствуют, используется GlobalPeriod\*. Ссылки: [PeriodStart](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_PeriodStart), [PeriodEnd](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_PeriodEnd)
* Docs view mode (Integer) — 2 = только свои документы; 1 = только документы своей группы; 0 = все документы. Удобно ввести как список значений: \[ZZZ] Docs view mode=0 .type.Docs view mode=Integer .listValue.Docs view mode=0,1,2 .listTextValue.Docs view mode="All documents","All group documents","Private documents" Ссылка: [Docs view mode](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_Docs_view_mode)
* Docs edit mode (Integer) — 2 = редактирование только своих документов (или у которых USERID пуст), 1 = только группы (или USERID пуст), 0 = все. Аналогично удобно ввести в виде списка значений. Ссылка: [Docs edit mode](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_Docs_edit_mode)
* UserGroupList (String) — список кодов пользователей (через запятую), составляющих группу для Docs view/edit mode. Ссылка: [UserGroupList](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_UserGroupList)

Настройки форм и справочников системы

* NewSyntax (Boolean) — в названиях секций справочников вместо '\_' использовать '#' (решётка). В этом режиме дизайны гридов справочников сохраняются под именем секции, что позволяет переносить их с секцией методом "Экспорт в XML". Ссылка: [NewSyntax](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_NewSyntax)
* HideMenuDict (Boolean, default true) — отображение меню "Справочники". Ссылка: [HideMenuDict](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_HideMenuDict)
* HideMenuReps (Boolean, default true) — отображение меню "Отчеты". Ссылка: [HideMenuReps](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_HideMenuReps)
* HideMenuForms (Boolean, default true) — отображение меню "Формы". Ссылка: [HideMenuForms](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_HideMenuForms)

Панели инструментов

* TBIconStyle (Integer 0..3) — положение значка относительно пункта меню: 0: значки не выводятся (только надписи); 1: надписи не выводятся (только значки); 2: значки слева от надписей; 3: значки над надписями. Удобно ввести как список: \[ZZZ] TBIconStyle=0 .type.TBIconStyle=Integer .listValue.TBIconStyle=0,1,2,3 .listTextValue.TBIconStyle="Captions only","Icons only","Icons and Captions","Icons above Captions" Ссылка: [TBIconStyle](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_TBIconStyle)
* TBIconSize (Integer 0..2) — размер значков: 0: мелкие; 1: средние; 2: крупные. Удобно ввести как список: \[ZZZ] TBIconSize=0 .type.TBIconSize=Integer .listValue.TBIconSize=0,1,2 .listTextValue.TBIconSize="Small Icons","Meduim Icons","Large Icons" Ссылка: [TBIconSize](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_TBIconSize)
* TBPeriod (Boolean) — отображать панель периодов. Ссылка: [TBPeriod](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_TBPeriod)
* TBWindowList (Boolean) — отображать панель открытых окон. Ссылка: [TBWindowList](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_TBWindowList)

Стартовая форма, фильтр по NrSet и т.п.

* AutoShowForm (String) — имя секции формы, которую показывать сразу после запуска программы. Не обрабатывается, если указан BG\_FILTER\_SECTION. Ссылка: [AutoShowForm](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_AutoShowForm)
* BG\_FILTER\_SECTION (String) — если непустой, сразу после запуска открывается окно установки фильтра по NrSet либо (при непустом XDEF\_BGFILTER) фильтр устанавливается автоматически и форма не показывается. Ссылка: [BG\_FILTER\_SECTION](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_BG_FILTER_SECTION)
* XDEF\_BGFILTER (String) — начальное значение фильтра по NrSet: перечисление кодов позиций фильтра через запятую или '\*' для включения всех. Ссылка: [XDEF\_BGFILTER](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_XDEF_BGFILTER)
* XDEF\_NRSET (String) — начальное значение NrSet по умолчанию. Ссылка: [XDEF\_NRSET](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_XDEF_NRSET)
* XDEF\_NRSET\_VIEW (String) — список кодов NrSet, которыми ограничиваются права пользователя. Ссылка: [XDEF\_NRSET\_VIEW](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_XDEF_NRSET_VIEW)
* HideNrsetFilter (Boolean) — не отображать установленный фильтр по NrSet. Ссылка: [HideNrsetFilter](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_HideNrsetFilter)

Настройки окна регистра документов (в разделе "System settings" секция "Docs")

* ViewFromToday (Integer) — ограничение периода отображаемых документов как смещение на указанное число дней назад от текущей даты. Ссылка: [ViewFromToday](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_ViewFromToday)
* ViewBegin (String) — минимальная дата отображаемых документов. Ссылка: [ViewBegin](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_ViewBegin)
* ViewEnd (String) — максимальная дата отображаемых документов. Ссылка: [ViewEnd](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_ViewEnd)
* DEF\_JOURNAL (String) — имя секции журнала, который надо открывать сразу после запуска. Ссылка: [DEF\_JOURNAL](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_DEF_JOURNAL)
* LastRecord (Boolean) — при открытии журнала переходить на последний видимый документ. Ссылка: [LastRecord](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LastRecord)
* ORDER BY (String) — порядок сортировки документов (список имен полей, разделённых запятыми). Ссылка: [ORDER BY](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_ORDER_BY)
* DataAutomat (Boolean) — автозаполнение даты документов на основании даты предыдущего документа. Ссылка: [DataAutomat](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_DataAutomat)
* DataCurrent (Boolean) — автозаполнение даты документов на основании текущей даты. Ссылка: [DataCurrent](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_DataCurrent)
* DataEmpty (Boolean) — отменить автозаполнение поля DATAMANUAL для пользователя (отмена глобальных DataAutomat и DataCurrent). Ссылка: [DataEmpty](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_DataEmpty)
* ColorDisabledDocs (Integer, default clAqua) — цвет неактивных документов. Ссылка: [ColorDisabledDocs](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_ColorDisabledDocs)
* DefaultModule (String) — значение поля TIP по умолчанию. Ссылка: [DefaultModule](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_DefaultModule)
* DefValuta (String) — значение поля VALUTA по умолчанию. Ссылка: [DefValuta](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_DefValuta)
* PXCompatibile (Boolean) — режим использования документов версии PX. Ссылка: [PXCompatibile](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_PXCompatibile)
* PXCMSimpleEditing (Boolean) — режим быстрой правки проводок документов версии PX. Ссылка: [PXCMSimpleEditing](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_PXCMSimpleEditing)
* Backup (Boolean) — режим сохранения документов в архиве перед удалением. Ссылка: [Backup](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_Backup)
* OnDeleteCMName (String) — объект, из которого будут удаляться проводки в документе. (упоминание в разделе параметров)

Настройки окна менеджера отчетов

* RepDataStart / RepDataEnd (String) — дата начала/конца периода просмотра данных в отчётах (допускается SQL-выражение). Если отсутствуют, используются PeriodStart / PeriodEnd. Ссылки: [RepDataStart](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_RepDataStart), [RepDataEnd](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_RepDataEnd)
* RepTemplatesPath (String, example m:\templates.ora) — каталог размещения файлов шаблонов для построения отчётов. Ссылка: [RepTemplatesPath](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_RepTemplatesPath)
* RepTreeFromSysS (Boolean) — добавлять в дерево отчётов список отчётов из системного справочника (SysS). Ссылка: [RepTreeFromSysS](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_RepTreeFromSysS)
* ReportTreeSorting (Boolean) — сортировка узлов дерева отчётов по алфавиту. Ссылка: [ReportTreeSorting](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_ReportTreeSorting)
* StartupReportNode (String) — имя секции отчёта, на котором позиционировать дерево отчётов при открытии менеджера. Ссылка: [StartupReportNode](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_StartupReportNode)
* RepTestRecordCount (Boolean, default true) — режим проверки количества записей в наборе данных отчёта (для F1Reports): при очень большом количестве записей выдаётся предупреждение; пределы: Master/Detail = 1000, только Master = 10000. Ссылка: [RepTestRecordCount](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_RepTestRecordCount)
* RepDeleteTempTables (Boolean, default true) — удалять временные таблицы ORACLE после построения отчёта (можно выключить). Ссылка: [RepDeleteTempTables](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_RepDeleteTempTables)

Разные настройки

* GridDisableNumberSearch (Boolean) — текстовый поиск даже в числовых полях грида (вместо числового поиска). Ссылка: [GridDisableNumberSearch](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#__GridDisableNumberSearch)
* UseSmartTab (Boolean) — "умный" Tab: переход от поля к полю по всему активному окну. Ссылка: [UseSmartTab](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_UseSmartTab)
* UseSmartEnter (Boolean) — "умный" Enter на дополнительной клавиатуре: при редактировании таблиц — переход к следующему полю или завершение редактирования и вставка новой записи. Ссылка: [UseSmartEnter](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_UseSmartEnter)
* UseSpeedSearch (Boolean) — быстрый поиск в выпадающих справочниках. Ссылка: [UseSpeedSearch](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_UseSpeedSearch)
* AutoFreeMemory (Boolean) — выгружать неиспользуемые динамические библиотеки (DLL и BPL). Ссылка: [AutoFreeMemory](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_AutoFreeMemory)
* UseDotInCont (Boolean) — использовать точку в значении счета (формат 99.99). Ссылка: [UseDotInCont](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_UseDotInCont)
* ContFormat (String) — формат поля счета. Ссылка: [ContFormat](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_ContFormat)
* LengthCont (Integer, default 4) — длина счета (обычно 4, для бюджетных предприятий — 3). Ссылка: [LengthCont](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LengthCont)
* LengthPachet (Integer, default 2) — длина номера пачки. Ссылка: [LengthPachet](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LengthPachet)
* LengthCont1 (Integer) — длина субсчета. Ссылка: [LengthCont1](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LengthCont1)
* UnivDLL (Integer, default 100) — код DLL карточек универсального справочника. Ссылка: [UnivDLL](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_UnivDLL)
* EnableBDE (Boolean) — при старте инициализировать подсистему BDE (рекомендуется). Ссылка: [EnableBDE](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_EnableBDE)
* NoCheckLocale (Boolean) — при старте не проверять региональные настройки. Ссылка: [NoCheckLocale](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_NoCheckLocale)
* NoCheckFreeSpace (Boolean) — при старте не проверять свободное место на дисках. Ссылка: [NoCheckFreeSpace](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_NoCheckFreeSpace)
* OraLoaderModeDML (Boolean) — использование DML при загрузке данных из текстового файла или таблицы BDE (уменьшает скорость загрузки, но позволяет обойти ограничения). Ссылка: [OraLoaderModeDML](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_OraLoaderModeDML)

Установка соединения

* CheckOraVersion (Boolean) — проверка версии БД (пользовательской схемы и UN4PUBLIC). Если версия ниже требуемой, вход запрещён. Ссылка: [CheckOraVersion](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_CheckOraVersion)
* CheckSecurityMode (Boolean, default true) — режим привязки локального компьютера к имени пользователя (можно выключить). Ссылка: [CheckSecurityMode](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_CheckSecurityMode)
* ShowLogin (Boolean, default true) — показывать окно регистрации (можно отключить, если задать Server, Login и Password). Ссылка: [ShowLogin](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_ShowLogin)
* OraHome (Integer) — выбор ORACLE Client для соединения. Ссылка: [OraHome](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_OraHome)
* Server (String) — сервер ORACLE по умолчанию. Ссылка: [Server](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_Server)
* Login / Password (String) — имя пользователя и пароль по умолчанию. Ссылки: [Login](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_Login), [Password](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_Password)
* OraUserName / OraPassword (String) — имя схемы ORACLE и её пароль по умолчанию. Ссылки: [OraUserName](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_OraUserName), [OraPassword](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_OraPassword)
* WindowsLogon (Boolean) — брать имя пользователя по умолчанию из ОС. Ссылка: [WindowsLogon](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_WindowsLogon)
* LockUserName (Boolean) — запретить изменение имени пользователя (оно должно быть задано заранее). Ссылка: [LockUserName](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LockUserName)
* SetLogo (Integer) — включение режима случайного выбора логотипа на окне регистрации. Ссылка: [SetLogo](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_SetLogo)
* LogoPath (String) — размещение файлов с логотипами для режима SetLogo. Ссылка: [LogoPath](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_LogoPath)

Отладочные возможности

* RunMaximized (Integer, default 1) — запуск программы в полноэкранном режиме (можно отменить). Ссылка: [RunMaximized](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_RunMaximized)
* AutoRunCmd (String) — команда, которую нужно выполнить сразу после запуска. Ссылка: [AutoRunCmd](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_AutoRunCmd)
* AutoLoadScript (String) — файл скрипта, который нужно загрузить сразу после запуска. Ссылка: [AutoLoadScript](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_AutoLoadScript)
* SQLMonitorLog (Boolean) — режим протоколирования обращений к серверу (работает при включённом SQLMonitorActive). Ссылка: [SQLMonitorLog](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_SQLMonitorLog)
* SQLMonitorLogFile (String, default monitor.log) — имя файла протокола обращений к серверу (либо только имя файла, либо полный путь). Ссылка: [SQLMonitorLogFile](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_SQLMonitorLogFile)
* SQLMonitorLogUnique (Boolean) — режим генерации уникального имени файла протокола. Ссылка: [SQLMonitorLogUnique](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_SQLMonitorLogUnique)
* SQLMonitorLogLimit (Integer, default 100) — минимальный размер сообщения, подлежащего протоколированию (отсечение "мусора"). Ссылка: [SQLMonitorLogLimit](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_SQLMonitorLogLimit)
* SQLMonitorActive (Boolean) — включение SQLMonitor (соединение с программой SQLMonitor и протоколирование обращений к серверу). Ссылка: [SQLMonitorActive](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_SQLMonitorActive)
* UseProfiler (Boolean) — режим измерения быстродействия программы. Ссылка: [UseProfiler](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_UseProfiler)
* MeasureTraffic (Boolean) — режим измерения трафика и вывода отладочных сообщений. Ссылка: [MeasureTraffic](file:///D:/UNA/UNA.md-130409-4.1.5.052/un4setup/init.html#_MeasureTraffic)

Примечания

* Во всех приведённых ссылках сохранены оригинальные URL-адреса и якоря.
* Если требуется преобразовать конкретную часть таблицы в машинно-структурированный формат (например, CSV/JSON или отдельные секции ini), укажите формат и желаемую структуру — подготовлю преобразование на основе этих параметров.
