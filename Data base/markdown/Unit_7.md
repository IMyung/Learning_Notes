**L101：Running SQL file**

@import "../img/7_101_1.png"

* 若只在 terminal 下達指令
  則很容易在指令分段輸入時，不小心打錯進而改不了
  如上例中 name 理應為 varchar ，卻不小心輸入成 INT 型態
  <br/>
  
@import "../img/7_101_2.png"
* 因此採用在 SQL file 撰寫指令
  source指令來讀取.sql檔的方式最為彈性


---

**L71：Official intro to SELECT**
```SQL