#redis #output #permanent 
### Default 
---
```bash
redis-server
```

### Use Setting
---
must-have
```vim
# 允許訪問的地址，默認是127.0.0.1，會導致只能在本地訪問。修改為0.0.0.0則可以在任意IP訪問，生產環境不要設置為0.0.0.0  
bind 0.0.0.0  
# 守護進程，修改為yes后即可後台運行  
daemonize yes   
# 密碼，設置后訪問Redis必須輸入密碼  
requirepass 11223344
```

usually
```vim
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

start
```bash
redis-server redis.conf
```
stop
```bash
kill -15 pid

redis-cli -a pwd shutdown
```
### Auto Start up
---
建立一個系統服務文件
```bash
vi /etc/systemd/system/redis.service
```


```vi
[Unit]
Description=redis-server  
After=network.target   

[Service]
Type=forking
ExecStart=/usr/local/bin/redis-server /usr/local/src/redis-6.2.6/redis.conf  
PrivateTmp=true   
 
[Install]
WantedBy=multi-user.target
```

重載系統服務

```bash
systemctl daemon-reload
```

系統操作 redis

```bash
## 啟動 redis
systemctl start redis

## 停止 redis
systemctl stop redis

## 重啟 redis
systemctl restart redis

## 查看 redis
systemctl status redis
```

啟用開機自動啟動
```bash
systemctl enable redis
```