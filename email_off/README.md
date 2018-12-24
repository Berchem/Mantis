當專案、議題、關聯性、使用者越來越多時，Mantis 的表現會變慢許多。

其中一個解決方法是關閉郵件通知。

編輯 ```/var/www/html/mantis/config/config_inc.php```

```
vim /var/www/html/mantis/config/config_inc.php
```

增加設定

```
$g_enable_email_notification = OFF;
```

重啟服務

```
systemctl restart httpd
```

**See also**

* <a href="https://mantisbt.org/bugs/view.php?id=21751&nbn=5">0021751: Mantis is very slow - MantisBT</a>