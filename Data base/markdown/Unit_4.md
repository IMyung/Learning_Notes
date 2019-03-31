**L44：Inserting Data**

```SQL
INSERT INTO table_name(column_name) 
VALUES (datas);
```
* 插入順序沒有差異，只要值有對應到就可以
* VALUES：單字後面有 s 記得要加
---

**L46：Super quick intro to SELECT**
```SQL
SELECT * FROM table_name;

查看表格所有內容
```
---

**L48：Multiple insert**
```SQL
INSERT INTO table_name(column_name) 
VALUES (datas) ,
       (datas) ;
```

---

**L48：Multiple insert**
```SQL
INSERT INTO table_name(column_name) 
VALUES (datas) ,
       (datas) ;
```

---

**L55：MySQL Warnings**

```SQL
SHOW WARNINGS;

// 顯示上一個指令的 WARNINGS
```
@import "../img/4_55_1.png"

* 若輸入過程中不符合變數規範，如 first_name 長度過長
  MySQL 會提示 Warning，但是並不會終止執行流程
  並且回頭去查看 table 會發現字串被截斷
  + 另個例子
    若例子改為 "I am age num" 輸入型態為 INT 的 age
    則顯示實際資料會發現 MySQL 把它變成了 0 值

---

**L57：NULL and NOT NULL**

@import "../img/4_57_1.png"

@import "../img/4_57_2.png"

* DESC table_name 查看 metadata
  會發現有一個 null 的欄位
  代表的是該欄位「若 INSERT 時沒有輸入資料」是可行的
  那麼會把該值預設為後方 default 所顯示的數值，在此是 NULL
  <br/>
* 因此在 CREATE TABLE 時若不想要出現 NULL value
  那麼得在需要定義的 metadata 後方加上 NOT NULL 強迫輸入數值

---

**L57：NULL and NOT NULL**

```SQL
CREATE TABLE t_name (
    col1 data_type NOT NULL
);

// 設定該參數不接受 null 值
```

@import "../img/4_57_1.png"

@import "../img/4_57_2.png"

@import "../img/4_57_3.png"

* 圖一：
  DESC table_name 查看 metadata
  會發現有一個 null 的欄位
  代表的是該欄位「若 INSERT 時沒有輸入資料」是可行的
  那麼會把該值預設為後方 default 所顯示的數值，在此是 null 值
  <br/>
* 圖二：
  因此在 CREATE TABLE 時若不想要出現 NULL value
  那麼得在需要定義的 metadata 後方加上 NOT NULL
  <br/>
* 圖三：
  有設定 NOT NULL 的 metadata
  若在 INSERT 時沒有輸入，其值會變系統對該型態預設的初值
  eg：INT 預設為 0，而不會是出現無法進行處理的 null 值

---

**L59：Setting default value**

```SQL
CREATE TABLE t_name (
    col1 data_type DEFAULT default_vlaue
);

// 設定 default value 
```

@import "../img/4_59_1.png"

@import "../img/4_59_2.png"

* 圖一
  更改預設的初值
  <br/>
* 圖二
  但若今天都有了 DEFAULT ，那麼加上 NOT NULL 的意義何在？
  主要是在於若用 NOT NULL 指名不接受 null 值，並後續使用 default 值
  若是沒有加上 NOT NULL 則代表可以控制是否要加入 null 值
  <br/>

---

**L61：A primer on primary keys**

```SQL
CREATE TABLE t_name (
    pri_col_name data_type NOT NULL AUTO_INCREMENT,
    PRIMARY KEY(pri_col_name)
);

// 設置 primary key
```

@import "../img/4_61_1.png"

* 資料當中可能常常會出現數值皆完全相同
  例如可能有相同歲數，且年齡也相同的人
  所以應該用另外一個能識別唯一方式來辨別
  也就是採用 PRIMARY KEY
  <br/>
* AUTO_INCREMENT
  讓 ID 值自行增長，不需要在 INSERT 時手動增長
  <br/>