# Redis Setting

## Start up

### Default start up

redis 目錄下直接執行
```
redis-server
```

### 設定檔啟動

---

先調整設定檔
```
# 允許訪問的地址，默認是127.0.0.1，會導致只能在本地訪問。修改為0.0.0.0則可以在任意IP訪問，生產環境不要設置為0.0.0.0  
bind 0.0.0.0  
# 守護進程，修改為yes后即可後台運行  
daemonize yes   
# 密碼，設置后訪問Redis必須輸入密碼  
requirepass 11223344
```

Redis其他常用配置
```
# 監聽的端口  
port 6379  
# 工作目錄，默認是當前目錄，也就是運行redis-server時的命令，日誌、持久化等文件會保存在這個目錄  
dir .  
# 數據庫數量，設置為1，代表只使用1個庫，默認有16個庫，編號0~15  
databases 1  
# 設置redis能夠使用的最大內存  
maxmemory 512mb  
# 日誌文件，默認為空，不記錄日誌，可以指定日誌文件名  
logfile "redis.log"
```