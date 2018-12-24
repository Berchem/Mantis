Mantis 有許多擴充套件可以自行安裝，到 <a href="https://github.com/mantisbt-plugins">MantisBT Community Plugins</a> 搜尋套件，裡面有豐富的套件安裝與使用說明。一般來說，下載並解壓縮，將 plugin 模組移動到 Mantis 套件目錄後，由系統管理者登入 Mantis，便能夠從網頁後台擴充套件。

安裝步驟：

**1.** 下載：可使用 ```git clone url``` 或是 ```wget url```。

**1.1.** 使用 ```git```

安裝 git

```
yum install git
```

下載套件，以 <a href="https://github.com/mantisbt-plugins/csv-import">Import CSV file</a> 為例：

```
git clone https://github.com/mantisbt-plugins/csv-import.git
```

**1.2.** 使用 ```wget```

安裝 wget

```
yum install wget
```


下載套件，以 <a href="https://github.com/mantisbt-plugins/csv-import">Import CSV file</a> 為例：

```
wget https://github.com/mantisbt-plugins/csv-import/archive/master.zip
```

下載完成後解壓縮。

```
unzip master.zip
```

**2.** 移動 plugin 模組至 Mantis 套件目錄下 ```/var/www/html/mantis/plugins```

注意套件目錄的 folder 結構。有些模組解壓縮後，會產生在子目錄之下，以 <a href="https://github.com/mantisbt-plugins/timetracking">timetracking</a> 為例：

```
timetracking-master/
├── LICENSE.md
├── readme.md
└── TimeTracking
    ├── core
    │   └── timetracking_api.php
    ├── lang
    │   ├── strings_catalan.txt
    │   ├── strings_english.txt
    │   ├── strings_french.txt
    │   ├── strings_german.txt
    │   ├── strings_polish.txt
    │   ├── strings_portuguese_brazil.txt
    │   └── strings_spanish.txt
    ├── pages
    │   ├── add_record.php
    │   ├── config_page.php
    │   ├── config_update.php
    │   ├── delete_record.php
    │   └── show_report.php
    └── TimeTracking.php

```

需修改其目錄層次如下：

```
/var/www/html/mantis/plugins
 └─ 模組名稱
    ├─ php 繼承設定/
    ├─ 相關語言支援/
    ├─ 套件執行頁面/
    └─ 套件安裝與初始化頁面.php
```

以 <a href="https://github.com/mantisbt-plugins/csv-import">Import CSV file</a> 為例，移動模組至 Mantis 套件目錄：

```
mv csv-import-master /var/www/html/mantis/plugins/Csv_import
```

結果如下:

```
/var/www/html/mantis/plugins
 └─ Csv_import 
    ├─ lang/
    ├─ pages/
    ├─ Csv_import.php
    └─ README.md
```

<a href="https://github.com/mantisbt-plugins/csv-import">Import CSV file</a> 這個套件匯入時，會去判斷模組名稱是否符合 (case sensitive)，模組名稱必須是 ```Csv_import```，才能夠在 Mantis 後台管理中匯入。

**3.** 由系管理者帳號登入 Mantis → 管理 → 管理套件 → 安裝套件
