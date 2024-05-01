#redis #output #fleeting  
## 設計結構

### [[主從模式 Master-Salve]]
### [[哨兵模式 Sentinel]]
### [[分片集群 Cluster Shard]]


---
## 設定方式

### Master-Salve
在一台主機中啟動三個實例，需準備三份不同設定文件和目錄
1. 將 redis.conf 複製成三份，放在三個不同的目錄下
2. 修改 redis.conf 指定 working directory
3. 修改 redis.conf 服務聲明 replica-announce-ip  {ip address}
4. 開啟主從關係
	- 永久- 修改 redis.conf
	- 臨時- 使用 redis-cli 輸入執行
``` 
 replicaof <masterip> <masterport>
```

### Sentinel
在一台主機中啟動三個監控實例，需準備三份不同設定文件和目錄
1. 分別在三個目錄下建立 sentinel.conf
2. 修改 sentinel.conf
 ```
   port 27001 
   sentinel announce-ip 192.168.xxx.xxx #宣告自己的IP 
   sentinel monitor mymaster 192.168.xxx.xxx 7001 2 
   sentinel down-after-milliseconds mymaster 5000 
   sentinel failover-timeout mymaster 60000 dir "/tmp/s1" #工作目錄
```

說明：
- `port 27001`：當前sentinel的埠
- `sentinel monitor mymaster 192.168.xxx.xxx 7001 2` ：指定主節點訊息
    - `mymaster`：主節點名稱，自訂
    - `192.168.xxx.xxx 7001`：主節點的IP和埠
