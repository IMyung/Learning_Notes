**L24：What is a DataBase**

```SQL
SHOW DATABASES;

// 顯示所有 DB
```

```SQL
CREATE DATABASE DB_Nmae;

// 創建一個 DB
```
* 指令不區分大小寫，但習慣都是大寫
* 創建名稱按一般程序命名規範
* SQL 指令結尾都有分號 ;

---

**L26：Dropping Databases**

```SQL
DROP DATABASE DB_Nmae;

// 刪除一個 DB
```

---

**L28：Using Databases**

```SQL
USE DB_Nmae;

// 選擇要使用哪個 DB
```

```SQL
SELECT database();

// 顯示當前使用的 DB 是哪一個
```
* null 代表目前沒有指向任一個 DB

---

**L30：Introduction to tables**

```
A database is just a bunch of tables

* each row is a data
* each column is mata data 
```
* <font color="#FF0000">注意</font>：這個定義是指在 relational database 的情況

---

**L31：The basic Datatypes**

* 若 column 沒有限制資料儲存型態，容易造成儲存格式混亂
  如：age 欄位當中，可以儲存 10 ，也可能會儲存 "ten"
  <br/>
* 資料格式有多種，用到時再查詢要用什麼型態的即可

---

**L35：The basic Datatypes**

```SQL
CREATE TABLE table_name (
    column_name data_type ,
    column_name data_type
);
```
* 使用 ( ) 包住欄位參數，不是花括號 { }
* 欄位之間，分隔只用逗號 , 

---

**L36：How do we know it works?**

```SQL
SHOW TABLES;

// 顯示當前 DB 當中的表格 
```

```SQL
SHOW COLUMNS FROM table_name;

// 顯示該 table 當中的 columns 
```

```SQL
DESC table_name;

// 同上面指令的效果
```

---

**L39：Dropping table**

```SQL
DROP TABLE table_name;

// 刪除該 table
```