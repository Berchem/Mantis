修改上傳檔案的大小限制，至少有兩個設定檔要改。

<table>
  <tr>
    <td>1. PHP </td>
    <td>/etc/php.ini</td>
    <td>required</td>
  </tr>
  <tr>
    <td>2. Mantis </td>
    <td>/var/www/html/mantis/config/config_inc.php</td>
    <td>required</td>
  </tr>
  <tr>
    <td>3. MariaDB </td>
    <td>/etc/my.cnf</td>
    <td>optional</td>
  </tr>
</table>

**假設修改上傳大小為 20 MB**

**1.** 修改 PHP 設定檔。

編輯 ```/etc/php.ini```

```
vim /etc/php.ini
```

修改貼文大小與上傳檔案大小

```
...
post_max_size = 20M
...
upload_max_filesize = 20M
...
```

**2.** 修改 Mantis 設定檔，預設是上傳到 MariaDB，也可選擇上傳到 server disk。

編輯 ```/var/www/html/config/config_inc.php```

```
vim /var/www/html/config/config_inc.php
```

**2.1.** 使用 MariaDB 儲存，增加設定

```
$g_allow_file_upload = ON;
$g_file_upload_method = DATABASE;
$g_max_file_size = 20971520; # 20 MB = 20 * 1024 * 1024
```

**2.2.** 或使用硬碟儲存，增加設定

```
$g_allow_file_upload = ON;
$g_file_upload_method = DISK;
$g_max_file_size = 20971520; # 20 MB = 20 * 1024 * 1024
$g_absolute_path_default_upload_folder = '/var/www/html/mantis/upload';
```

創建上傳資料夾

```
mkdir /var/www/html/mantis/upload
chown -R apache:apache /var/www/html/mantis/upload
```

**3.** 根據 **2.** 若上傳至 MariaDB，則需要修改 MariaDB 設定檔。

編輯 MariaDB 設定檔 ```/etc/my.cnf```

```
vim /etc/my.cnf
```

修改允許的封包大小

```
max_allowed_packet=20M
```

重啟服務

```
systemctl restart mysqld
systemctl restart httpd
```


**See also**

* <a href="https://mantisbt.org/forums/viewtopic.php?t=25233">32MB file uploads - how? - Mantis Bug Tracker - Forums</a>
* <a href="https://www.mantisbt.org/forums/viewtopic.php?t=764">Max file upload problem - Mantis Bug Tracker - Forums</a>
* <a href="https://www.mantisbt.org/forums/viewtopic.php?f=3&t=23465">Upload Files to Disk - Mantis Bug Tracker - Forums</a>