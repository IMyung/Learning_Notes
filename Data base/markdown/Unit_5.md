**L67：Intro to CRUD**

C：Create
R：Read
U：Update
D：Delete

* 增刪改查
* 前面章節已提及 create 的部分

---

**L71：Official intro to SELECT**
```SQL
SELECT * FROM table_name;
```

```SQL
SELECT col_1 , ... FROM table_name;
```

* SELECT FROM 負責取出符合欄位條件的全部資料
* 星號 * 代表全部的欄位
* 欄位顯示順序可以按照需求顯示

---

**L73：Intro to WHERE**

```SQL
SELECT col_1 , ... FROM table_name WHERE condition;
```

* WHERE 根據 SELECT FROM 取出全部資料
  再從這堆資料再篩選出「是要怎樣條件」的資料
  <br/>
* 並沒有僅限用於 SELECT FROM 
  也可以用於其他的指令，用來篩選
  <br/>
* <font color="#FF0000">注意</font>：
  當搜索採用字串比對時，不區分字母大小！
  也意指像是處理 email 存在性時就不用考慮大小寫區別

---

**L74-7：小練習**

---

**L78：Intro to Aliasis**

```SQL
SELECT col_1 AS alias_name FROM table_name;
```

@import "../img/5_78_1.png"

會更改欄位「顯示時的名稱」

---

**L80：The UPDATE command**

```SQL
UPDATE table_name SET changed_col = value
WHERE condition ;
```
* UPDATE 符合某個條件的一些資料
  <br/>
* <font color="#FF0000"><b>Good Habbit</b></font>
  在進行任何的資料更動前，如 UPDATE、DELETE 前
  最好先行利用等價的 SELECT FROM WHERE 
  查看反饋的資料是不是就是那些符合條件要被更改的資料！

---

**L81-4：小練習**

---

**L85：Intro to DELETE**

```SQL
DELETE FROM table_name WHERE condition;

// 刪除某筆資料
```

```SQL
DELETE FROM table_name;

// 刪除整個 table
```

* 和 DROP 不同在於：DROP 會連整個表格都刪除
  但是 DELETE 只會把內部 entries 刪除，但表格還是存在

---

**L81-4：小練習**

---