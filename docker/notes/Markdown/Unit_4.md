**L36：Building a Dockerfile**

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