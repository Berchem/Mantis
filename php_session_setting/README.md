由於 PHP 的 Session 設定，會存取瀏覽器的快取與 cookie，當在回報議題時，如果掛載時間過久，或是遷移資料庫等動作，HTTP form 會送出 CSRF token 給伺服器，導致這個錯誤發生。可在 ```/var/www/html/config/config_inc.php``` 加入下列設定並重新啟動 apache。

```
$g_form_security_validation = OFF
```

**See also**

* <a href="https://mantisbt.org/bugs/view.php?id=12381">0012381: APPLICATION ERROR #2800</a>
* <a href="https://www.mantisbt.org/forums/viewtopic.php?f=2&t=19578">APPLICATION ERROR #2800 - Mantis Bug Tracker - Forums</a>