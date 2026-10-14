# Перевод статьи utl\_http-and-ssl.php

Источник: http://www.oracle-base.com/articles/misc/utl\_http-and-ssl.php

Пример процедуры для выполнения HTTP/HTTPS-запросов:

{% code title="show_html_from_url.sql" %}
```sql
CREATE OR REPLACE PROCEDURE show_html_from_url (p_url  IN  VARCHAR2) AS
  l_http_request   UTL_HTTP.req;
  l_http_response  UTL_HTTP.resp;
  l_text           VARCHAR2(32767);
BEGIN
  -- Make a HTTP request and get the response.
  l_http_request  := UTL_HTTP.begin_request(p_url);
  l_http_response := UTL_HTTP.get_response(l_http_request);
  -- Loop through the response.
  BEGIN
    LOOP
      UTL_HTTP.read_text(l_http_response, l_text, 32766);
      DBMS_OUTPUT.put_line (l_text);
    END LOOP;
  EXCEPTION
    WHEN UTL_HTTP.end_of_body THEN
      UTL_HTTP.end_response(l_http_response);
  END;
EXCEPTION
  WHEN OTHERS THEN
    UTL_HTTP.end_response(l_http_response);
    RAISE;
END show_html_from_url;
/
```
{% endcode %}

При попытке выполнить HTTPS-запрос:

```sql
EXEC show_html_from_url('https://gb.redhat.com/');
```

может возникнуть ошибка:

ORA-29024: Certificate validation failure.

В этом случае необходимо добавить сертификат(s) в Oracle Wallet. Ниже — пример последовательности действий.

{% stepper %}
{% step %}
### 1. Экспорт сертификатов сайта

Используя браузер (например, Mozilla Firefox), экспортируйте сертификаты для сайта gb.redhat.com в файлы. Сохраните корневой и промежуточные сертификаты в отдельных файлах (например, BaltimoreCyberTrustRoot.crt и CybertrustPublicSureServerSVCA.crt).
{% endstep %}

{% step %}
### 2. Создайте папку для Wallet

Создайте директорию, где будет храниться wallet:

```bash
mkdir -p /u01/app/oracle/admin/DB11G/wallet
```
{% endstep %}

{% step %}
### 3. Создайте новый Oracle Wallet

Создайте wallet с паролем и включите auto\_login (чтобы Oracle мог использовать wallet без ввода пароля):

```bash
orapki wallet create -wallet /u01/app/oracle/admin/DB11G/wallet -pwd WalletPasswd123 -auto_login
```
{% endstep %}

{% step %}
### 4. Добавьте в wallet экспортированные сертификаты

Добавьте каждый сохранённый сертификат как trusted\_cert:

```bash
orapki wallet add -wallet /u01/app/oracle/admin/DB11G/wallet -trusted_cert -cert "/host/BaltimoreCyberTrustRoot.crt" -pwd WalletPasswd123

orapki wallet add -wallet /u01/app/oracle/admin/DB11G/wallet -trusted_cert -cert "/host/CybertrustPublicSureServerSVCA.crt" -pwd WalletPasswd123
```
{% endstep %}

{% step %}
### 5. Укажите wallet для UTL\_HTTP и протестируйте

В сессии Oracle укажите путь к wallet и пароль:

```sql
EXEC UTL_HTTP.set_wallet('file:/u01/app/oracle/admin/DB11G/wallet', 'WalletPasswd123');
```

Затем выполните процедуру снова:

```sql
EXEC show_html_from_url('https://gb.redhat.com/');
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Если вы используете auto\_login при создании wallet, при указании wallet в UTL\_HTTP можно передать пустой пароль (или тот же пароль). Но обычно указывают путь в формате 'file:/path/to/wallet' и пароль, который вы установили при создании.
{% endhint %}
