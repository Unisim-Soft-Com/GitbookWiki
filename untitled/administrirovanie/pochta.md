# Почта

Для отправки почты по SSL можно установить stunnel и создать конфигурационный файл:

{% code title="/usr/local/etc/stunnel/stunnel.conf" %}
```ini
client = yes
[ssmtp]
accept = 465
connect = smtp.gmail.com:465
```
{% endcode %}

Файл службы: /etc/init.d/ (см. [stunnel](https://yadi.sk/i/lvB2f17G3WnsAj)).

{% hint style="info" %}
Также для отправки почты необходимо настроить права ACL:\
https://bsoft.gitbook.io/wiki/administrirovanie/nastroika-oracle/prava-dostupa-acl
{% endhint %}
