# Oracle Wallet

Ссылка на источник: http://www.oracle-base.com/articles/misc/utl\_http-and-ssl.php

Частичный перевод статьи: https://unisim-soft.gitbook.io/wiki/administrirovanie/nastroika-oracle/oracle-wallet/perevod-stati-utl\_http-and-ssl.php

Описание утилиты для управления Oracle wallets: http://docs.oracle.com/cd/E11882\_01/network.112/e10746/asoappf.htm#ASOAG9830

Пример настройки Oracle Wallets для HTTPS запросов (для серв. trassir).

{% stepper %}
{% step %}
### Выгрузка сертификатов из Mozilla

Заходим в меню Настройки → Дополнительные → вкладка Сертификаты.\
Далее нажимаем кнопку "Просмотр сертификатов" и на вкладке "Серверы" выбираем нужные сертификаты (пример на скриншоте).

![](<../../../.gitbook/assets/image (302)>)

Экспортировать нужно оба сертификата, которые относятся к серверу trassir (тип файла выбираем "Все").\
Полученные файлы сертификатов разместить в каталоге Linux, доступном для чтения пользователю oracle, например:

/share/un4/cert/
{% endstep %}

{% step %}
### Создание wallet и добавление сертификатов

Сертификаты можно добавить к существующему wallet или создать новый wallet и добавить туда сертификаты.

Создаём каталог для wallet (пример):

```bash
mkdir -p /u01/app/oracle/admin/orcl/wallet
```

Создаём wallet в имеющейся папке:

```bash
$ORACLE_HOME/bin/orapki wallet create -wallet /u01/app/oracle/admin/orcl/wallet -pwd WalletPasswd123 -auto_login
```

Добавляем сертификаты к существующему wallet:

```bash
$ORACLE_HOME/bin/orapki wallet add -wallet /u01/app/oracle/admin/orcl/wallet -trusted_cert -cert "/share/un4/cert/trasir1.crt" -pwd WalletPasswd123
```
{% endstep %}

{% step %}
### Тестирование нового сертификата (кэширование запроса для получения сертификата)

Для тестирования нового сертификата необходимо вызвать команду `utl_http.set_wallet`.

Пример вызова:

```sql
utl_http.set_wallet('file:/u01/app/oracle/admin/orcl/wallet', 'WalletPasswd123');
```

Обратите внимание: `utl_http.set_wallet` может кешировать старое состояние wallet и в таком случае новые сертификаты не будут применены. Чтобы сбросить кеш, вызовите `utl_http.set_wallet` для несуществующего пути, например:

```sql
utl_http.set_wallet('file:/u01/app/oracle/admin/orcl/wallet12345', 'WalletPasswd123');
```

После этого снова выполните:

```sql
utl_http.set_wallet('file:/u01/app/oracle/admin/orcl/wallet', 'WalletPasswd123');
```

Если `utl_http.set_wallet` выдаёт ошибку "Файл не найден" или "Каталог не найден", необходимо дать права на каталог и файл пользователю oracle.
{% endstep %}

{% step %}
### Примеры для теста запроса

Пример PL/SQL (фрагмент) для тестирования HTTPS-запроса:

```sql
declare
  req  utl_http.req;
begin
  -- Указываем wallet с сертификатом
  utl_http.set_wallet('file:/u01/app/oracle/admin/orcl/wallet', 'WalletPasswd123');
  req := utl_http.begin_request('https://192.168.0.149:8080/login?password=eybcbv');
end;
```

Ещё один пример с вызовом процедуры (из исходного примера):

```sql
begin
  pkg_cctv.trassir_export_process(:p_date);
end;
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Сертификаты можно добавлять в существующий wallet или создавать новый wallet специально для нужного приложения. Не заменяйте пароли и пути — используйте те, что соответствуют вашей среде.
{% endhint %}
