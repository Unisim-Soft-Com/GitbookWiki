# Кнопка

### Чтобы открыть карточку (cartela) по нажатию кнопки и передать в нее параметр (nrdoc)

https://unisim-soft.gitbook.io/wiki/razrabotka/obekty-una/panel/knopka#chtoby-otkryt-kartochku-cartela-po-nazhatiyu-knopki-i-peredat-v-nee-parametr-nrdoc-neobkhodimo-v-svo

В свойстве Params кнопки пропишите:

```
TargetType=cartela
TargetSection=ATTR_ORD_ADD
nrdoc=_nrdoc
MainTA=1
```

Пояснение: по кнопке открывается карточка, имя секции которой = ATTR\_ORD\_ADD. В форму передаётся параметр nrdoc, значение которого берётся из запроса для панели, на которой расположена кнопка.

***

### Чтобы открыть форму по нажатию кнопки

https://unisim-soft.gitbook.io/wiki/razrabotka/obekty-una/panel/knopka#chtoby-otkryt-formu-po-nazhatiyu-knopki-neobkhodimo-v-svoistve-params-knopki-propisat

В свойстве Params кнопки пропишите:

```
TargetType=form
TargetSection=FRM_IMP_ORD_ADD
```

Пояснение: по нажатию кнопки открывается форма с именем секции = FRM\_IMP\_ORD\_ADD.

***

### Чтобы выполнить действие по нажатию кнопки

https://unisim-soft.gitbook.io/wiki/razrabotka/obekty-una/panel/knopka#chtoby-vypolnit-deistvie-po-nazhatiyu-knopki-neobkhodimo-v-svoistve-params-knopki-propisat

В свойстве Params кнопки пропишите:

```
TargetType=doc.action
action_id=1
```

Пояснение: по нажатию кнопки выполняется действие с id=1.
