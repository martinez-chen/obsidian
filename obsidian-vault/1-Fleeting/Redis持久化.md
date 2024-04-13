#fleeting #redis 

## RDB

全名為Redis Database Backup file(Redis數據備份文件)，也被稱為數據快照，簡單來說就是把記憶體內的所有數據紀錄到硬碟中，當Redis故障重啟後，從硬碟讀取快照文件，恢復數據。

```
>redis-cli 
>save # 由redis main process執行，會阻塞其於的process。預設就有，關閉服務時執行 >bgsave # 建立其他process於背景執行，異步作業
```
可以在redis.conf內找到，格式如下
```
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
