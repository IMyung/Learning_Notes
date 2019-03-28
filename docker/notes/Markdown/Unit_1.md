L1
why use docker ?
Docker 讓安裝和運行軟件這件事情簡化，不需要擔心步驟或依賴


L2
what is docker ?
Docker is a platform or ecosystem around creating and running containers.

> > docker run redis

1. docker CLI 會到 dockerHub 下載一個叫 image 的檔案
//這個檔案會包含所有的依賴及設定以達到運行一個特定功能的程序，像這邊的例子就是 redis

2. 那麼就可以用 image 創建叫 container 的東西
container：instance of an image run a program
// 也可以理解為就是一個擁有自己硬體資源的隔離區


L3
/* 
    上節課嘗試解釋 what is docker 但沒有一個很好的解釋，只知道有 image、container
    為了了解更多細節，這節課先了解一下整體骨架
*/

Docker client： 也稱 docker CLI。用戶下達指令的地方
Docker server： 也稱 docker daemon。是真正和 image、container 交互的地方


L4
// MAC docker 安裝
本節重點：
    安裝完後可以用 docker version 驗證
    會出現 client 端和 daemon 端的版本資訊


L5、6、7
// Win docker 安裝


L8：什麼是 image
>> docker run hello-world
// 執行完的第一行有 Unable to find image 'hello-world:latest' locally

深入了解這個指令背後的運行機制
1. docker CLI 接收使用者指令，並負責和 docker daemon 進行交互

2. docker daemon 這時想要把 'hello-world' 這個 container 給運行起來
   會先從「本地」image cache 當中尋找是否有此 image，沒有的話就會接 3.

3. docker daemon 再到「遠端」的 docker Hub 倉庫尋找對應的 image

4. 若有此 image ， docker daemon 會把它下載回「本地」的 image cache

5. docker daemon 會把此 image 加載到 MEM 變成 container ，運行 container 的程序

// 所以這也是上面 unable find 的由來
// 若再次執行同一個指令，就不會出現 unable find 的提示了 


L9：什麼是 container
要了解容器，必須先了解 OS 底層

程序是透過 sys call 和 kernel 交互請求資源
若現在有兩個程序對環境有不同的要求，例如一個要裝 python2，另個要 python3
那麼為了不能出錯，就得區分 SW1 和 SW_2 在硬碟對於軟件的需求尋址的概念

1. namespacing： Isolating resources per process(or group of processes)
   // 不見得只能用在硬件隔離，網路、Hostname 等都可以

2. Control group（cgroups）： limit amount of resources used per process

合在一起，就可以使某塊「有限且被隔離的」資源，只被這個 container 使用

Q:所以 image 和 container 的連接是什麼？
A:
    image 裡面實際包含
     - FS snapshot（檔案總管快照）
     - Startup command （預設啟動指令）

    a. 容器當中的運行 kernel 會規劃出一個只能被該容器讀取的硬盤
       其內容物僅僅只有存放從 image 當中取出的 FS 快照

    b. image 當中的 startup command 被執行

    c. kernel 從硬盤中取出需要被預設指令執行的程式
       放在 running processing 當中執行


L10：
namespacing ＆ Control group 是專屬 linux kernel 的封裝技術
所以得運行 Linux 虛擬機，也就是 docker for mac/win 軟件
裡面所包含的 linux kernel 會限制容器的資源存取與隔離等