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
  + 根據上述，課堂把規模縮小變成
    一個 Node server 容器，對上一個 Redis 容器進行存儲
  <br/>
* <font color="#FF0000"><b>目的：</b></font>主要是要製造出兩個容器有通信的行為

---

**L50：Assembling a Dockerfile**

和前面章節一樣，編寫一個 Dockerfile 
image 內部包還 index.html 和 package.json

---

**L51：Introducind docker compose**

@import "../img/5_51_1.png"

1. 透過 L50 的 Dockerfile 建構出 image 執行後
   發現需要 redis 依賴（左邊視窗）
   <br/>
2. 若改成先 docker run redis（右邊視窗）
   再運行 node image 也沒改善
   <br/>
3. 其原因在於<font color="#FF0000"><b>容器之間並沒有自動進行通信的能力</b></font>
   

* 解決方法
  + Use docker cli's networking features
    非常的麻煩
    1. 配置麻煩
    2. 每次重啟容器等都要進行重新配置
    3. 講師說從沒看過有人用 CLI 內建功能解決
  <br/>
  + docker compose
<br/>
```Docker
Docker Compose
```
1. Separate CLI that gets installed along with Docker
2. Used to start up multiple Docker containers at the same time
3. Automates some of the long-winded（囉唆） arguments we were passing to 'docker run'

* 自動化一些撰寫的長篇 Docker CLI 指令
* 非常容易的在同時間多重啟動諸多容器
* 並且自動的把他們串連起來形成一個網路

---

**L52：Introducind docker compose**


  <br/>

@import "../img/5_52_1.png"

```docker
docker-compose.yml


1. 同 docker build 要撰寫 Dockerfile
   但是此處並不只是僅僅只要把指令貼進去該檔案
   而是一樣要用特別的語法去撰寫 YML 檔案
   
2. 撰寫好後，丟給 docker-compose CLI 去執行
```

@import "../img/5_52_2.png"
@import "../img/5_52_3.png"

```docker
撰寫範例

version：3    # 聲明要使用哪個版本的 docker-compose

services：    # 此字眼大量地被使用在 docker，表明 type of container
  redis-server：
    image： 'redis'
  node-app：
    build： .
    ports：
      - "8081：8081"
```

---

**L53：Networking with docker-compose**

@import "../img/5_53_1.png"

* 根據上一節撰寫的，容器之間就已經能夠通信了
  不需要再特別聲明例如兩個容器之間哪個端口映射哪個端口
  <br/>
* 但還是得設定要怎麼從 NodeJS 本身連線到 Redis
  所以得更改 index.js 當中的 redis.createClient 內部新增 host
  + 一般來說，host都是 resdis http URL
  + 因為這裡是應用在 docker，所以可以撰寫 .yml 當中宣告的 services 名稱，也就是 redis-serer
  + docker 會自行判斷，並幫助跳轉 http request
  + 可以彈性設定端口

---

**L54：Docker compose commands**

@import "../img/5_54_1.png"

```docker
docker-compose up
# 等同 docker run image
# Create and start containers

docker-compose up --build
# 等同 docker build .  +  docker run image
```

```docker
1. 輸出首行：
   Creating network "unit_5_default" with the default driver
   代表 docker compose 替我們建立了內部連線的網絡

2. 可以在中間的位置看到兩個綠色字體的 done
   代表兩個服務已經被正常的啟動了

3. 後段是此兩個容器的運行輸出
```

---

**L55：Stopping docker compose containers**

```docker
docker run -d image_name
# -d 表示該容器在背景執行
```

此處出現的問題：
同時起那麼多容器，要一個個手動複製 image id 並關閉很費時
於是有了下列兩個指令

```docker
docker-compose up -d
# 背景啟動多個容器

docker-compose down
# 同時關閉多個容器
```

---

**L56：Container Maintenance with Compose**

@import "../img/5_56_1.png"

此章節故意修改 index.js ，製造 server 端死機
會發現只剩 redis 容器還在運作，NodeJS 容器進入 exit 狀態

---

**L57：Automatic Container Restarts**

@import "../img/5_57_1.png"
@import "../img/5_57_2.png"

* 添加 restart : res_policy 到 tml 中
* 要注意，no 是有含 ""
  因為 yml 檔案中有和其他預設名衝突

---

**L58：Container Status with Docker Compose**

```docker
docker-compose ps

# 列出所有 docker compose 的狀態
```
<font color="#FF0000"><b>注意</b></font>
docker-compose ps 的狀態查找
必須在含有 docker-compose.yml 作為 reference 
才能知道是哪些容器被群起
否則會出現找不到 .yml 檔的錯誤