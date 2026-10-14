# Создание СПРАВОЧНИКОВ

Для примера создадим специальный справочник типа P TVR для торговли, т.е. дизайн этого справочника будет отличатся от стандартного vms\_univers и настроен на другую вьюху.

Отрыть конфигуратор, выбрать раздел Univ List -> Univ group -> UnivTip\_P и продублируем любой узел.

Выбрать любой узел в группе UnivTip\_P, щелкаем по нему правой кнопкой мыши, в контекстном меню выбираем Data->Export->Node, далее щелкаем правой кнопкой мыши по UnivTip\_P и в контекстном меню выбираем Data ->Import->New SubNode.

![](<../../../../../.gitbook/assets/image (1196)>)

В новом узле задаем свойства:

Caption: UnivList P:TVR:Trade

Section: UNIVLIST : P : TRADE

имя в Caption задает по правилу, UnivList Тип:Атрибут(GR1):ID (значение ID придумывается по смыслу использования справочника), (можно задать любое имя).

имя Section задается как 'UNIVLIST:Тип:ID' (можно задать любое имя секции).

У узла задаем свойства (список минимальных свойств):

**Имя свойства**

**Тип**

**Описание**

**Значение для примера**

Active

Boolean

true

Caption

String

Справочник для торговли

Gr1

String

TVR

ID

String

Trade

SagiEditQuery

Boolean

true

Чтобы справочник выпадал в UNA по Alt+D

![](<../../../../../.gitbook/assets/image (1197)>)

[PreviousНастройка UnivList](./) [NextНастройка UnivList из нескольких типов](../nastroika-univlist-iz-neskolkikh-tipov.md)

Last updated 1 year ago
