# Инструкция по фокусам

Для того чтобы при открытии документа был сфокусирован какой-либо Control, необходимо в конфигураторе добавить свойство FocusControl и его название (тип свойства по умолчанию String). Сохраняем изменения с помощью галочки:

![](<../.gitbook/assets/image (391)>)

"Commit".

![](<../.gitbook/assets/image (392)>)

{% stepper %}
{% step %}
### Обновление настроек (F5) и подтверждение

В программе нажимаем горячую клавишу F5 для обновления настроек. В появившемся окне нажимаем кнопку "Yes":

![](<../.gitbook/assets/image (393)>)

Подтверждение:

![](<../.gitbook/assets/image (394)>)

После успешного обновления настроек нажимаем "OK":

![](<../.gitbook/assets/image (395)>)

Окно документа в режиме редактирования:

![](<../.gitbook/assets/image (396)>)
{% endstep %}

{% step %}
### Проверка фокуса на Control'е

После открытия документа на редактирование, фокус находится на Control'e UnDBEdit1.

![](<../.gitbook/assets/image (397)>)

Чтобы при открытии документа фокусировался другой Control, измените его имя в конфигураторе и повторите сохранение/обновление настроек. Примеры изменения имени и результата:

* Переименовали в UnDBEdit2 — после сохранения и обновления фокус на UnDBEdit2:

![](<../.gitbook/assets/image (398)>)

![](<../.gitbook/assets/image (399)>)

* Далее при изменении на UnDBEdit3 — фокус на UnDBEdit3:

![](<../.gitbook/assets/image (400)>)

![](<../.gitbook/assets/image (401)>)
{% endstep %}

{% step %}
### Доступ к дизайну Header и просмотр имён Control

Для перехода в дизайн Header'a нажимаем колесико мыши или с зажатым Ctrl — правой кнопкой мыши и в появившемся списке выбираем "Design".

![](<../.gitbook/assets/image (402)>)

Здесь можно посмотреть имена объектов Control, которые уже созданы:

![](<../.gitbook/assets/image (403)>)
{% endstep %}

{% step %}
### Примеры: фокус на различных типах Control

* Чтобы при открытии документа фокусировался DBMemo1 — записываем его имя в конфигураторе, сохраняем, обновляем настройки — фокус на DBMemo1:

![](<../.gitbook/assets/image (404)>)

![](<../.gitbook/assets/image (405)>)

* Для DBCheckBox1 — аналогично:

![](<../.gitbook/assets/image (406)>)

![](<../.gitbook/assets/image (407)>)

* Также можно фокусироваться на грид. Документ-пример имеет 3 грида: gr21a — первый грид. При нажатии на каждом гриде горячих клавиш Alt+D сверху можно посмотреть идентификатор:

Первый грид:

![](<../.gitbook/assets/image (408)>)

![](<../.gitbook/assets/image (409)>)

Второй грид:

![](<../.gitbook/assets/image (410)>)

![](<../.gitbook/assets/image (411)>)

Третий грид:

![](<../.gitbook/assets/image (412)>)

![](<../.gitbook/assets/image (413)>)

Примеры установки свойства focuscontrol для выбора грида:

* focuscontrol = gr21a (первый грид) — после сохранения/обновления фокус на первом гриде:

![](<../.gitbook/assets/image (414)>)

![](<../.gitbook/assets/image (415)>)

* focuscontrol = имя второго грида — фокус на втором гриде:

![](<../.gitbook/assets/image (416)>)

![](<../.gitbook/assets/image (417)>)

* focuscontrol = имя третьего грида — фокус на третьем гриде:

![](<../.gitbook/assets/image (418)>)

![](<../.gitbook/assets/image (419)>)
{% endstep %}
{% endstepper %}

Список объектов Control, имена которых можно записывать в свойстве FocusControl в конфигураторе.

Имя Control’a — Свойство в конфигураторе — Внешний вид:

* Edit1

![](<../.gitbook/assets/image (420)>)

![](<../.gitbook/assets/image (421)>)

* DBEdit1

![](<../.gitbook/assets/image (422)>)

![](<../.gitbook/assets/image (423)>)

* UnDBEdit1

![](<../.gitbook/assets/image (424)>)

![](<../.gitbook/assets/image (425)>)

* UnScList1

![](<../.gitbook/assets/image (426)>)

![](<../.gitbook/assets/image (427)>)

* CheckBox1

![](<../.gitbook/assets/image (428)>)

![](<../.gitbook/assets/image (429)>)

* DBCheckBox1

![](<../.gitbook/assets/image (430)>)

![](<../.gitbook/assets/image (431)>)

* DateEdit1 / DBDateEdit1 / DateTimeEdit1 / DBDateTimeEdit1

![](<../.gitbook/assets/image (432)>)

![](<../.gitbook/assets/image (433)>)

![](<../.gitbook/assets/image (434)>)

![](<../.gitbook/assets/image (435)>)

* RadioGroup1 / DBRadioGroup1

![](<../.gitbook/assets/image (436)>)

![](<../.gitbook/assets/image (437)>)

* Memo1 / DBMemo1

![](<../.gitbook/assets/image (438)>)

![](<../.gitbook/assets/image (439)>)

* Button1

![](<../.gitbook/assets/image (440)>)

![](<../.gitbook/assets/image (441)>)

* DBImage1 (пустой / с картинкой)

![](<../.gitbook/assets/image (442)>)

![](<../.gitbook/assets/image (443)>)

***

Если нужно, могу преобразовать этот материал в отдельные шаги с заголовками для каждой операции (например: "Добавление свойства", "Сохранение и Commit", "Обновление настроек", "Настройка FocusControl для грида/Контрола"), или собрать таблицу со списком допустимых имён Control для вставки в свойство FocusControl.
