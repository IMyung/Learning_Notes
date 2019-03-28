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
