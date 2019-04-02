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
   
   # 注意</font>：bulid 後面有點 .
   ```

---

**L37、8**

範例檔：Sample code in Unit 4
包含一個 index.js 和 package.jason

package.jason：列出運行該 project 所需要的依賴軟件

---

**L39：A few planned errors**

```Dockerfile
FROM alpine

RUN npm install

CMD ["npm","start"]

# 範例 Dockerfile
# 故意產生錯誤，從中學習怎麼製作 Dockerfile
```
<br/>

---

**L40：Base image issues**

@import "../img/4_40_1.png"

* <font color="#FF0000"><b>Err 1</b></font>
  + 安裝 alpine 後，欲執行 NodeJS 的包管理器 NPM 無法執行
  + 因為 alpine 是一個輕量級的 OS ，預設時並沒有預裝 NodeJS 或 NPM
  <br/>
* <font color="#0000FF"><b>Sol 1</b></font>
  + 於 RUN 當中自行安裝這兩個依賴軟件
  + 安裝含有預裝 NodeJS 或 NPM 的 base image
    + 課堂範例選擇以此方法進行
      因此到 DockerHub 上頭尋找可用的 image
    + 可以透過 full description 來判斷
<br/>

---

**L41：A few missing files**

@import "../img/4_41_1.png"

@import "../img/4_41_2.png"

* <font color="#FF0000"><b>Err 2</b></font>
  沒有找到運行該專案所需要的 package.json 依賴文檔
  + 其實是有正確執行 npm install 
    出錯原因是因為 package.json 存在於容器之外
    容器找不到存在於 Host sys 上的容器「外部」檔案

---

**L42：Copying build files**

```Dockerfile
COPY  ./  ./

# ./ 為當前目錄文件夾
```

```Dockerfile
FROM alpine

COPY  ./  ./      #<------  在 RUN npm install 之前進行
RUN npm install

CMD ["npm","start"]
```
* 把文件從當前 Host 目錄，拷貝到容器當前目錄 
  + 處於和 Dockerfile 同根目錄的 index.js 和 package.json 會被拷貝進容器中

---

**L43：Container port mapping**

@import "../img/4_43_1.png"

<font color="#FF0000"><b>Err 3</b></font>
容器雖正常創建了並且監聽 8080 端口
但實際執行卻沒有任何的反應

@import "../img/4_43_2.png"

* <font color="#0000FF"><b>Sol 3</b></font>
  預設上，外部的端口並沒有映射到內部端口的能力
  + 但預設上內部是能夠任意訪問外部的
    如 install 時能抓外部的 package

```Dockerfile
docker run -p HOST_port:Container_port image_name

# Routing imcomimg requests to this port on local host 
# to the port inside the container
```

* 不論是外部還是內部的 port 皆可以變換
  並非兩者一定要相同或完全不改能成其他 port value

---

**L44：Specifying a working dir**

@import "../img/4_44_1.png"

* 當進到該容器內部時
  會發現當初在 Dockerfile 中 COPY 步驟所拷貝的文件
  散落在 alpine 操作系統當中的根目錄底下十分混亂！

```Dockerfile
WORKDIR path

# 覆蓋掉系統預設執行路徑，更改成此
```
```Dockerfile
FROM alpine

WORKDIR /usr/app      #<------  從此指令之後，預設路徑皆會更改成此
COPY  ./  ./          #<------  ./ 根目錄是 /usr/app
RUN npm install

CMD ["npm","start"]
```
@import "../img/4_44_2.png"

* 進入容器時的預設根目錄也會變成此，不再是系統預設根目錄

---

**L45：Unnecessary rebuilds**

@import "../img/4_45_1.png"

僅僅只是更改了自己檔案的源代碼
卻也造成了整體 docker image 在建構的過程中重新建構
造成不必要的重複性安裝

---

**L46：Minimizing cache busting and rebuild**

```Dockerfile  
COPY  ./  ./          #<------  拆解此步驟
```
```Dockerfile
FROM alpine

WORKDIR /usr/app      
COPY  ./packages.json  ./          #<------ 
RUN npm install
COPY ./ ./                         #<------

CMD ["npm","start"]

# npm install 會對 package.json 產生改動依賴
# 而一般改動都是改動 index.html，而不是依賴安裝文檔 packages.json
# 這樣的 COPY 拆法就不會影響到 npm install 重複執行
# 就會使 image building 的執行速度大幅提高
```
     

