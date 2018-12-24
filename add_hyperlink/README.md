若要從 Mantis 的檢視問題頁面，轉入單一議題回報頁面，需點選 **id** 欄位進入。而**摘要**欄位則通常是議題的名稱或簡述，從使用者的角度來說，點選名稱上的超連結，較符合一般使用者之體驗。

在 Mantis 2.18.0 我們可以藉由髒寫 (dirty change) 的方式快速修改。

編輯 ```/var/www/html/mantis/core/columns_api.php```

```
vim /var/www/html/mantis/core/columns_api.php
```

原始程式：

```
function print_column_summary( BugData $p_bug, $p_columns_target = COLUMNS_TARGET_VIEW_PAGE ) {
        if( $p_columns_target == COLUMNS_TARGET_CSV_PAGE ) {
                $t_summary = string_attribute( $p_bug->summary );
        } else {
                $t_summary = string_display_line_links( $p_bug->summary );
        }
        echo '<td class="column-summary">' . $t_summary . '</td>';
}
```

修改 ```function print_column_summary``` 中的 ```echo '<td class="column-summary">' . $t_summary . '</td>';```，加入超連接敘述。

```
function print_column_summary( BugData $p_bug, $p_columns_target = COLUMNS_TARGET_VIEW_PAGE ) {
        if( $p_columns_target == COLUMNS_TARGET_CSV_PAGE ) {
                $t_summary = string_attribute( $p_bug->summary );
        } else {
                $t_summary = string_display_line_links( $p_bug->summary );
        }
        echo '<td class="column-summary"><a href="view.php?id=' . $p_bug->id . '">' . $t_summary . '</a></td>';
}
```

重啟服務

```
systemctl restart httpd
```

**See also**

* <a href="https://mantisbt.org/forums/viewtopic.php?t=24165">How to make summary description as a link to bug id?</a>