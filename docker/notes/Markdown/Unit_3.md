**L27：Creating Dcoker image**

@import "../img/3_27_1.png"

* 整體創建流程：
  + docker file 為一份內含許多行調配指令的文本
    內部的調配將影響容器的運行行為
  + 文本創建之後會傳送給 docker CLI
  + CLI 又會傳送給 Daemon
  + Daemon 實際的根據指令去創建容器<br/><br/>

@import "../img/3_27_2.png"

* Dockerfile 撰寫流程：
  + 定義一個 base image
  + 下指令安裝額外的程序
  + 定義一個 default startup command<br/><br/>

---

**L28：Building a Dockerfile**

// 課程以建立手把手建立 redis image 為例

* **Dockerfile 創建流程：**
1. IDE 當中創建名為 Dockerfile 的文件
   <font color="#FF0000">注意</font>：D 要大寫，沒有任何副檔名後綴
   <br/>
2. 撰寫 Dockerfile
   ```Dockerfile
   # 使用現有的 docker image 作為 base image
   FROM alpine

   # 下載和安裝依賴
   RUN apk add --update redis

   # 設定預設指令
   CMD ["redis-server"]
   ```
    
3. 到 terminal 執行 docker build
   ```Dockerfile
   docker build .
   
   注意</font>：bulid 後面有點 .
   ```

---

**L30：What is base image**

@import "../img/3_30_1.png" 
<br/>
@import "../img/3_30_2.png"

* ```Dockerfile
  FROM alpine

  需要有一個 base image 提供基礎的運行服務
  就好似上述安裝 chrome 前需要有 OS 一樣
  ``` 

* ```Dockerfile
  RUN apk add --update redis

  安裝實際需要建構的套件集，此例的 redis 程序
  其中 apk 並不是 docker 當中的指令，而是 alpine 內建
  代表的是提供安裝的語法，讓 alpine 下載安裝 redis 
  ``` 

* ```Dockerfile
  CMD ["redis-server"]

  設定 default startup command
  ``` 

---

**L31：The build process in detail**

@import "../img/3_31_1.png"

* docker build 底層運行流程
1. ```Dockerfile
   docker build .  // 把 Dockerfile 提交給 docker  CLI
   ```
2. ```
   Step 1/3：
   base image 的處理
   和一般 image 處理流程一樣，若 local cache 有就直接使用，沒的的話會從 DockerHub 上面下載
   ```
3. ```
   Step 2/3：
   1. 在執行 RUN 指令後面的參數（參數就是要被運行的真實指令）之前
      會去看 FROM 指令所輸出的 image ，並根據此 image 產生一個臨時容器

   2. 運行該參數指令，apk add --update redis，讓臨時容器內部去下載和安裝 redis 程序
      // 也就是截圖中的 fetching 和 excuting 過程
  
   3. 進行此臨時容器的 FS 快照，製作成一個 image
      // 也就是 8dea7ee781b8

   4. 停止運行該臨時容器
   ```   
4. ```
   Step 3/3：
   1. 查看 RUN 指令所輸出的 image ，並產生臨時容器

   2. 把 CMD 指令當中的指令參數寫到容器中，但不會真實運行！
  
   3. 進行此臨時容器的 FS 快照，製作成一個 image
      // 也就是 3a05785284e4

   4. 停止運行該臨時容器
   ```
