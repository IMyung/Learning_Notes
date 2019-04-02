遠端操作

本地檔案庫連結遠端檔案庫
1. 有現有本地端檔案庫，需要和遠端進行連結
   ```
   git remote add origin url
   ``` 
   * origin：預設遠端代號名稱
   * url：檔案庫路徑。可以是網址或磁碟路徑

   ```git
   git remote show origin

   # 顯示遠端檔案庫的訊息
   ``` 

   ```git
   git ls-remote url

   # 顯示遠端分支
   ```

   ```git
   git fetch

   # 把遠端 commit 紀錄抓下來到本地
   # 不會重設工作目錄、改變Head和分支位置
   ```
2. 沒有本地端，從遠端拷貝下來
