#permanent  #redis #output 

## RDB

全名為Redis Database Backup file(Redis數據備份文件)，也被稱為數據快照，簡單來說就是把記憶體內的所有數據紀錄到硬碟中，當Redis故障重啟後，從硬碟讀取快照文件，恢復數據。

```
>redis-cli 
>save # 由redis main process執行，會阻塞其於的process。預設就有，關閉服務時執行 >bgsave # 建立其他process於背景執行，異步作業
```
可以在redis.conf內找到，格式如下
```vim
# 900秒內，若至少一個key被修改，則執行bgsave，如果是save "" 則表示禁用 
save 900 1 
save 300 10 
save 60 10000 

# 是否壓縮，不建議開啟，壓縮也會消耗cpu，硬碟的話不值錢 
rdbcompression yes 

# RDB 文件名稱 
dbfilename dump.rdb 

# 文件保存的路徑目錄 
dir ./
```

---

## AOF
全名為 Append Only File (追加文件) 。 Redis處裡的每一個寫命令都會記錄在AOF文件，可以看做是命令日誌文件。

AOF預設是關閉的，需要修改 redis.conf 設定來開啟
```vim
#是否開啟AOF功能，預設是no 
appendonly yes 

# AOF文件的名稱 
appendfilename "appendonly.aof"

# 表示每執行一次寫命令，立即記錄到aof文件 
appendfsync always 

# 寫命令執行完先放到AOF緩衝區，然後表示每隔1秒將緩衝區數據寫到AOF文件，是默認方案 
appendfsync everysec

# 寫命令執行完先放入AOF緩衝區，然後由操作系統決定何時將緩衝區內容寫回硬碟 
appendfsync no
```

因是紀錄命令，AOF文件會比RDB文件大許多，且AOF會記錄同一個key的多次寫操作，但只有最後一次的寫操作才有意義。 透過執行 bgrewriteaof 命令，可以讓AOF文件執行重寫功能，用最少命令達到相同效果。

Redis觸發閾值時自動 rewrite aof文件，閾值也能在redis.conf中設定
```vim
# AOF文件比上次文件 增長超過多少百分比時觸發 
auto-aof-rewrite-percentage 100 

# AOF 文件下限多少以上觸發 
auto-aof-rewrite-min-size 64mb
```


|         | RDB                    | AOF                               |     |
| ------- | ---------------------- | --------------------------------- | --- |
| 持久化方式   | 定時對整個記憶體做快照            | 紀錄每一次執行的命令                        |     |
| 數據完整性   | 不完整，兩次備份之間會丟失資料        | 相對完整，取決於硬碟刷新策略                    |     |
| 文件大小    | 會有壓縮，文件體積小             | 記錄命令，文件體積大                        |     |
| 當機恢復速度  | 很快                     | 快                                 |     |
| 數據恢復優先級 | 低，因為完整性不如AOF           | 高，因為完整性更高                         |     |
| 系統資源佔用  | 高，大量CPU和記憶體消耗          | 低，主要是硬碟IO資源 但AOF重寫時會佔用大量CPU和記憶體資源 |     |
| 使用場景    | 可以容忍數分鐘的數據丟失，追求更快的啟動速度 | 對數據安全性要求較高常見                      |     |
