# Импорт данных

{% stepper %}
{% step %}
### В программе toad создаем соединение со схемой Dev@oratest или используем уже существующее.

В верхней строке меню найдите Database и выберите Database -> Import -> Import Utility Wizard.

![](<../../.gitbook/assets/image (322)>)
{% endstep %}

{% step %}
### Выберите Импорт таблицы (Import tables) из следующих опций и нажмите Далее.

![](<../../.gitbook/assets/image (323)>)
{% endstep %}

{% step %}
### В поле From user введите название схемы, с которой был сделан экспорт.

![](<../../.gitbook/assets/image (324)>)
{% endstep %}

{% step %}
### Выбрать в Export file name файл с расширением .DMP

![](<../../.gitbook/assets/image (325)>)
{% endstep %}

{% step %}
### Нажать на кнопку импорта и затем кнопку "Готово" (Finish)

![](<../../.gitbook/assets/image (326)>)

После импорта данных создаются таблицы для дальнейшего использования.
{% endstep %}
{% endstepper %}
