從 OS 登入 MariaDB

```shell
mysql -u mantisAdmin -p
```

修改使用者密碼的指令為：

```mysql
update mantis_user_table set password=md5('新密碼') where username = '使用者名稱';
```

例如：修改使用者 Berchem.Lin 的密碼為 helloWorld。

```mysql
update mantis_user_table set password=md5('helloWorld') where username = 'Berchem.Lin';
```

注意：

請勿使用 *replace*，Mantis 在網頁上創立帳號後，會記錄 cookie string，*cookie_string* 預設為 NULL，如果這個欄位被取代掉，這個帳號登入時，會出現 cookie error。

**See also**

* <a href="https://gist.github.com/anytizer/11420125">Reset user password in Mantis Bug Tracker</a>
