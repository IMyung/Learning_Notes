**L43：CSS 三個存放方法**

* inline：
  非常不推薦！直接寫在某標籤 <> 內部，結構十分僵化不易更改
  另外是也會造成 html 結構和 css 的修飾混亂在同一個頁面當中<br/><br/>

* head 當中的 < style >  < /style >：
  ```js
  <head>
        < style type = "text/css" >
            selector {
                property : value;
            }
        </style>
  </head>
  ```

  + 結構比 inline 清晰，但一般使用 html、css 檔案分離的設計
  + < style >：補上 type = "text/css" 是宣告文件型態
  + 修飾句子的末尾記得要加上分號 ; <br/><br/>

* external： 
  把 css 要修飾的內容獨立在多個 .css 檔案後
  利用 < link > 標籤當中的 href 屬性進行外部引入
  ```js
  <head>
        <link rel="stylesheet" type="text/css" href="...">
  </head>
  ```

---

**L45：CSS property：color**

* 一般不會直接使用顏色名字，如：red、blue
  且通常在幫別人接案設計時，都會有指定的色系表現
  // 顏色展示參考：http://colours.neilorangepeel.com/<br/><br/>

* Hexdecimal color
  ```js
  selector {
        color : #XXXXXX;
  }
  ```
  + 井字號 # 加上 6 位數 16 進制顏色字串
  + 由左到右為 RGB 色，如：FF0000 為 red
  + 可以利用 color picker 進行顏色挑選<br/><br/>

* RGB
  ```js
  selector {
        color : rgb( 255 , 100 , 99 );
  }
  ```
  + 數值大小：0 - 255<br/><br/>

* RGBA
  ```js
  selector {
        color : rgb( 255 , 100 , 99 , .6 );
  }
  ```
  + 前面ㄧ樣為 RGB ，最後 alpha 為濃淡程度
  + 數值大小： 淺 0.0 - 1.0 濃

---

**L46：CSS property：background、border**

* 
  ```js
  selector {
        background : rgb( 255 , 100 , 99 );
  }
  ```
  ```js
  selector {
        background : url(...)
  }
  ```
  + 利用顏色進行背景更改
  + 利用圖片進行更改<br/><br/>

* ```js
  selector {
        border-color : rgb( ... );
        border-width : ...px;
        border-style : ...;
  }
  ```
  ```js
    selector {
        border： ...px style color;
  }
  ```
  + 邊框設定
  + px（pixel）和前面的數字中間不能有空隙

---

**L48：CSS selectors**

* ```js
    # id_name { ... }
  ```

* ```js
    . class_name { ... }
  ```

* ```js
    element_name { ... }
  ```
  + id_selector：針對特定單一
  + class_selector：綁定成同類型的
  + element_selector：同種標籤的

---

**L50：CSS advanced selector**

額外介紹其他常用的 selector 
// 30 CSS selectors（ 參考 ）：https://goo.gl/J84euG

* ```js
    * { ... }
  ```
  + *Star selector*
  + 圈選該頁面所有元素<br/><br/>

* ```js
    e1 e2 e3 { ... }

  e：代表標籤名
  其中右標籤為左標籤的子標籤
  ```
  + *Descendant selector*
  + 巢狀寫法
    因為標籤寫法本身可以多層次巢狀
    所以也得有多層次指定特定元素才行 <br/><br/>

* ```js
    n1 + n2 { ... }

  n：同層級的標籤
  ```
  + *Adjacent selector*
  + 同層級的標籤才可以使用此圈選法
    意思為緊跟在 n1 標籤後面的 n2 標籤要進行套用 <br/><br/>

  + eg
    @import "../img/5_50.gif"
    <br/><br/>

* ```js
    element[attribute] { ... }
  ```

  ```js
    element[attribute = "value"] { ... }
  ```
  + *Attribute selector*
  + 對含有「某個屬性」的某個標籤進行套用
  + 對含有「某個屬性值」的「某個屬性」的某個標籤進行套用
  + eg
    < input type="checkbox"> 
    type 會有很多種，如 checkbox
    那麼只想對有 type 這個屬性且值為 checkbox 的 input 標籤進行更改
    那麼其他的 input 類型就不會受到套用影響<br/><br/>

* ```js
    type:nth-of-type( number ) { ... }
  ```
  + *n-th of type*
  + 對所有某標籤的第 n 個元素進行套用


---

**L52：CSS Specificity**
* ```js
  優先級套用的順序性

  ID > class > tag > body
  ```
  + Specificity Calculator（ 優先級計算器，參考 ）：https://specificity.keegan.st/