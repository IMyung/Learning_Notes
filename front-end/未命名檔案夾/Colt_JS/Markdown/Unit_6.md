**L57：Text and fonts**

* ```js
  selector {
        font-family : font;
  }
  ```
  + 設定字型
  + 瀏覽器字體可用性參考：https://goo.gl/FfXqJh
  + < p > 假文句產生器：https://goo.gl/8VBnvZ
  <br/><br/>

* ```js
  selector {
        font-size : ...unit;
  }

  注意： unit 和數字間不能有空隙
  ```
  + 設定字體大小
  + px 
  + <font color="#FF0000"><b>em 動態大小字體</b></font>
    + 當前區段字體大小的 n 倍
    + 下圖示範 em 的使用
      因此範例中的 To do List 為 body 的預設大小
      p 為預設字體大小的兩倍，而 span 又是 p 的兩倍，動態大小字體<br/>
  + 設計思路
    + 先利用 body 對其設定全域字體大小再設定各個標籤

    @import "../img/6_57_1.png"
    @import "../img/6_57_2.png"<br/><br/>

---

**L58：More text and fonts**

* ```js
  selector {
        font-weight : ...;
  }
  ```
  + 字體粗細度
  + normal、bold....
  + 映射到數字大小：細 100 - 800 粗
  <br/><br/>

* ```js
  selector {
        line-height : ...;
  }
  ```
  + 字段間距
  <br/><br/>

* ```js
  selector {
        text-align : ...;
  }
  ```
  + 字段對齊
  + right、center、right
  <br/><br/>

* ```js
  selector {
        text-decoration : ...;
  }
  ```
  + 劃線
  + underline、strike、line-through
  <br/><br/>

---

**L59：Note about google font**

* google font：https://fonts.google.com/

---

**L59：Note about google font**

* 若採用 L57 提及系統內建字體，會有不一定能使用的問題
  也不見得比較好看以及授權的問題，因此可以採用 google 字體
  <br/>
* google font：https://fonts.google.com/

---

**L61：Introduction to box model**

* In a document, each element is represented as a rectangular box

* In CSS, each of these rectangular boxes is described using the standard box model.
  
* Each box has four edges: the margin edge, border edge, padding edge, and content edge.

@import "../img/6_61_1.png"

// 筆記沒做好，再從頭看

