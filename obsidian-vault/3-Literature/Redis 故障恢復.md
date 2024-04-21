#redis #output #permanent 
## 設計結構

### [[主從模式 Master-Salve]]
### [[哨兵模式 Sentinel]]

---
## 設定方式

### Master-Salve
在一台主機中
1. 將 redis.conf 複製成三份
2. 修改 redis.conf 指定 working directory
3. 修改 redis.conf 服務聲明 replica-announce-ip 