**L25**

```
custom docker image 
```
@import "/img/3_1.png"

docker image：需要
---

**L13**

```
docker ps [option]
```
* default ：    顯示運行中容器
* [ option ] 
  +  -a , --all ： 顯示運行、停止的容器 <br /><br />

* <font color="#dd0000">Note</font>
    會時常利用此指令查看 container ID
    以便下達指令對「特定容器」作用

---

**L14**

docker ps 當中 status，如 exit
容器是怎麼進到這一步運行狀態的？在此了解容器的生命週期<br /><br />

docker run 是執行了 creating ＆ running 動作
```
docker run   -- 拆解 -->   docker create   +   docker start
```  

* docker create < image名稱 > [ option ]：
  + 用於在容器啟動前進行必要設置
    僅把 FS snapshot 放進容器的硬盤區當中，不啟動容器
  + [ option ]：想要覆寫的 startup command<br/><br/>

* docker start [ option ] < container ID > ：
  執行 image 當中的 startup command，真正啟動容器
  + [ option ]： -a
    顯示執行容器過程中所有顯示的 output<br/><br/>

  + start 指令「預設不顯示」任何 output 
  +  run  指令是「預設顯示」任何 output

@import "/img/2_14.png"

---

**L15**

啟動過後的 docker 進入到 exit 狀態還能夠再重啟

<font color="#dd0000">Note</font>：但是不可以再次 override 已經填寫上的 startup command
  
@import "/img/2_15.png"

---

**L16**

```
docker system prune
```
刪除所有的 images 和 containers

---

**L17**


```
docker logs < container ID >
```
若在執行 docker start 時忘記添加 -a 顯示 output 內容
而而本身該容器執行時間又非常的長，重啟的代價會很大的話
那麼可以使用 logs 來提取過去所有顯示記錄

* <font color="#dd0000">Note</font>：
  + 常用來 debug 除錯
  + logs 指令並不是重新執行容器而是提取 log，執行代價低

---

**L18**

```
docker stop < container ID >
```

```
docker kill < container ID >
```

執行容器，執行狀態一直處於 running
可以使用這兩個指令對其進行終止 exit

* 兩者差異
  stop：給予容器中的主進程時間（10s）進行資料備份並終止
  kill：直接終止容器的運行<br /><br />

* 流程：
  stop 會發出 SIGTERM( terminate signal )告知容器主進程終止
  kill 則是發出 SIGKILL
  @import "/img/2_18.png"

---

**L19**

@import "/img/2_19_1.png" 
<br /><br />

@import "/img/2_19_2.png"
<br />
課程當中引用 redis 作為例子 
<font color="#00BB00">// redis 也分 server , cli 架構</font><br />


容器運行時，是執行 stratup command：redis-server 啟動 redis 服務器端
而 redis-cli 客戶端啟動指令想要執行時，被容器隔離在外部
所以要想一個辦法讓容器能運行除了 sratup command 以外的第二個指令，例如 redis-cli，才能讓程序正確運行

---

**L20**

```
docker exec -it < container ID > < command >
```
* default ：Execute an additional command in a container
  + command：Command that want to be executed insdie container
  + <font color="#dd0000">重要</font>
  -it： allow as to provide input to the container
  如果沒有這個指令，那麼無法從外部進行 input 行為

@import "/img/2_20.png"

---

**L21**

@import "/img/2_21_1.png"
<br/>

容器其實也就是運行在 linux 虛擬機上的進程
該些進程都會有三個溝通管道：STDIN、STDOUT、STDERR<br/><br/>

上章節提到的 -it 其實是兩個 flag 的合併寫法： -i -t
其中 -i 代表的就是把 terminal 和 STDIN 管道對接起來
而 -t 則是讓顯示更加的美觀一些（如下例沒有 -t，則沒有輸入提示符號）

@import "/img/2_21_2.png"

---

**L22**

```
docker exec -it < container ID > sh
```

exec 指令只能一次性的透過 STDIN 管道對容器下指令
那麼若要下多個指令的話，那麼重複性的 exec 下指令很冗餘
因此若容器內部「有提供 shell」便可以進入，下多個額外運行指令

@import "/img/2_22.png"

---

**L23**

```
docker run -it < image_name > sh
```

會時常以 run 指令，加上 -it 標籤執行
一般若要運行軟件服務，都會在容器內部包含 shell 以方便調試

---

**L24**

@import "/img/2_24.png"

容器之間的流通是完全隔離的
例如：不同容器之間的 file sys 不共享