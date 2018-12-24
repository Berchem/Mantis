藉由 dirty change 調整 Mantis 收疊版型。

編輯 ```/var/www/html/mantis/core/collapse_api.php```

```
vim /var/www/html/mantis/core/collapse_api.php
```

修改 ```function is_collapsed```中的邏輯判斷，原始程式如下：

```
function is_collapsed( $p_block ) {
        global $g_collapse_cache_token;

        if( !isset( $g_collapse_cache_token[$p_block] ) ) {
                return false;
        }
        return( true == $g_collapse_cache_token[$p_block] );
}
```

修改為：

```
function is_collapsed( $p_block ) {
        global $g_collapse_cache_token;

        if( !isset( $g_collapse_cache_token[$p_block] ) ) {
                return true;
        }
        return( true == $g_collapse_cache_token[$p_block] );
}
```

重啟服務

```
systemctl restart httpd
```

**See also**

* <a href="https://mantisbt.org/forums/viewtopic.php?t=308">'Collapsed by default' in collapse_api + minor improvements</a>
* <a href="https://www.mantisbt.org/forums/viewtopic.php?t=25298">Filter box collapsed by default?</a>