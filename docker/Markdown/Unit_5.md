**L47：APP overview**

@import "../img/5_47_1.png"

* <font color="#0000FF"><b>兩個軟件</b></font>
  Node APP：唯一個服務器，用來接收並回傳請求
  Redis server：In mem 的資料存儲。用來儲存瀏覽數


@import "../img/5_47_2.png"

* <font color="#0000FF"><b>若把兩個軟件包在同個容器</b></font>
  都在同個容器當然是可行的
  但是若規模擴大，一般做法是複製多個相同容器
  這樣造成的問題是，每個容器內部的資料會造成不同步

@import "../img/5_47_3.png"

* <font color="#0000FF"><b>改進：</b></font>
  把多個容器改成只負責 Node server，對同一個 Redis 進行存儲
<br/>

根據上述，課堂把規模縮小變成
一個包含 Node server 的容器，對一個包含 Redis 的容器進行存儲
<font color="#FF0000"><b>目的：</b></font>主要是要製造出兩個容器有通信的行為

---

**L50：Assembling a Dockerfile**

和前面章節一樣，編寫一個 Dockerfile 
image 內部包還 index.html 和 package.json

---

**L51：Introducind docker compose**

@import "../img/5_51_1.png"

1. 透過 L50 的 Dockerfile 建構出 image 執行後，發現需要 redis 依賴
2. 若改成先 docker run redis ，再運行 node image 也沒改善
3. 其原因在於<font color="#FF0000"><b>容器之間並沒有通信的能力</b></font>

* 解決方法
  + Use docker cli's networking features
    // 非常的麻煩，講師說從沒看過有人用 CLI 內建功能解決

  + docker compose
<br/>
```Docker
Docker Compose
```
1. 是一個內建於 Docker 的獨立 CLI
2. 用來同時啟動多個 docker 容器
3. Automates some of the long-winded arguments we were passing to 'docker run'
// 這邊定義沒有講清楚
   只知道能夠自動的起大量容器，減少重複指令
   並且能夠自動串接內部網絡

---

**L52：Introducind docker compose**

@import "../img/5_51_1.png"

    