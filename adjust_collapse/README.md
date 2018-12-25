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

若僅只修改 Sidebar 的收疊，修改 ```function collapse_cache_token``` 新增 ```$t_data``` array 至 202 行：

```
new old
197 197        if( !is_null( $t_token ) ) {
198 198                $t_data = json_decode( $t_token, true );
199 199        } else {
200 200                $t_data = array();
201 201                $t_data['filter'] = false;
202     +              $t_data['sidebar'] = true;
203 202        }

```

重啟服務

```
systemctl restart httpd
```

**See also**

* <a href="https://mantisbt.org/forums/viewtopic.php?t=308">'Collapsed by default' in collapse_api + minor improvements</a>
* <a href="https://www.mantisbt.org/forums/viewtopic.php?t=25298">Filter box collapsed by default?</a>