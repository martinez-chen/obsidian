### 全量同步

[[主從模式 Master-Salve]] 第一次同步是全量同步

![[全量同步.png]]

- Replication Id：是數據集的標記，id一致表示同一數據集，每一個master都有唯一的id，replica(slave)則會繼承master節點的id。
- offset：偏移量，隨著紀錄的repl_baklog中的數據增多而變大，replica(slave)完成同步時也會記錄當前同步的offset。如果replica(slave)的offset小於master的offset，說明replica的數據落後於master，需要更新。

💡 master 透過replication id 判斷 replica(slave)是否第一次來做數據同步，而非offset，故
	1.1 psync replicationId offset
	1.3 return replicationId offset


### 增量同步

![[增量同步.png]]

💡 repl_baklog大小有上限，master與slave之間的差距不可大過紀錄上限。 如果slave斷開時間過久導致數據被覆蓋，只能再次全量同步不可增量同步