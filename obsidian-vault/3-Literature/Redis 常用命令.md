#redis #output #permanent 

## 通用命令
部分數據類型的，都可以使用的指令．

Redis的key的格式： `[項目]:[業務名]:[類型]:[id]`

| 命令          | 描述                                         |
| ----------- | ------------------------------------------ |
| SET         | 添加或者修改已經存在的一個String類型的鍵值對                  |
| GET         | 根據key獲取String類型的value                      |
| MSET        | 批量添加多個String類型的鍵值對                         |
| MGET        | 根據多個key獲取多個String類型的value                  |
| INCR        | 讓一個整數型的key自增1                              |
| INCRBY      | 讓一個整數型的key自增並指定步長，例如：incrby num 2 讓num值自增2 |
| INCRBYFLOAT | 讓一個浮點類型的数字自增並指定步長                          |
| SETNX       | 添加一個String類型的鍵值對，前提是這個key不存在，否則不執行         |
| SETEX       | 添加一個String類型的鍵值對，並且指定有效期                   |

---
## Hash類型
Hash類型，也叫散列，其value是無序字典，類似於Java中的HashMap結構
可以value中的每個字段獨立儲存，也可以對單個字段做CRUD

  

| 命令                   | 描述                                           |
| -------------------- | -------------------------------------------- |
| HSET key field balue | 添加或者修改已經存在的一個hash類型key的field的值               |
| HGET key field       | 獲取hash類型key的field的值                          |
| HMSET                | 批量添加多個hash類型key的field的值                      |
| HMGET                | 獲取多個hash類型key的field的值                        |
| HGETALL              | 獲取一個hash類型key的所有field和所有的value               |
| HKEYS                | 獲取一個hash類型key的所有field                        |
| HVALS                | 獲取一個hash類型key的所有value                        |
| HINCRBY              | 讓一個整數型的value自增並指定步長，例如：incrby num 2 讓num值自增2 |
| HSETNX               | 添加一個hash類型的key的field的值，前提是這個field不存在，否則不執行   |

---
## List類型

List類型類似於Java中的LinkedList，可以看作雙向鏈表結構，可以正向檢索也可以反向檢索．
特徵與LinkList類似：
- 有序
- 元素可以重複
- 插入刪除快
- 查詢速度一般

| 命令                   | 描述                                       |
| -------------------- | ---------------------------------------- |
| LPUSH key element    | 向列表左側插入一個或多個元素                           |
| LPOP key             | 移除並返回列表最左側元素，若沒有則回傳nil                   |
| RPUSH key element    | 向列表右側插入一個或多個元素                           |
| RPOP key             | 移除並返回列表最右側元素，若沒有則回傳nil                   |
| LRANGE key start end | 返回一段標示範圍內的元素                             |
| BLPOP/BRPOP          | 與LPOP．RPOP類似，不過在沒有元素的時候會等待指定時間，不會馬上回傳nil |
|                      |                                          |

- 思考

> 如何用List結構模擬堆疊?
> - 入口和出口在同一邊

> 如何用List結構模擬隊列?
> - 入口和出口在不同邊

> 如何用List結構模擬阻塞隊列?
> - 入口和出口在不同邊
> - 出口使用BLPOP或BRPOP

  
---
## Set類型

Set結構與Java中的HashSet類似，可以視為value為null的HashMap，
因為是一個Hash表，有以下特徵：
- 無序
- 元素不可重複
- 查詢快
- 支援交集．聯集．差集等功能

| 指令                   | 描述              |
| -------------------- | --------------- |
| SADD key member      | 向set添加一個或多個元素   |
| SREM key member      | 移除set中的指定元素     |
| SCARD key            | 返回set中的元素個數     |
| SISMEMBER key member | 判斷一個元素是否存在於set中 |
| SMEMBER key          | 返回set中所有的元素     |
| SINTER key1 key2     | 求key1和key2的交集   |
| SDIFF key1 key2      | 求key1和key2的差集   |
| SUNION key1 key2     | 求key1和key2的聯集   |

---
## SortedSet類型

SortedSet類型是一個可排序的set集合，與Java中的TreeSet類似，但底層結構差距很大，SortedSet中的每個元素都需要有一個score屬性，
可以基於score屬性對元素排序，底層實現的是一個**跳表(SkipList)**加hash表．
SortedSet有以下特性：
- 可排序
- 元素不可重複
- 查詢速度快
因SortedSet的可排序特性，經常被用在排行榜的功能

| 指令                         | 描述                                                    |
| ---------------------------- | ------------------------------------------------------- |
| ZADD key score member        | 向sorted set添加一個或多個元素，若已存在則更新其score值 |
| ZREM key member              | 移除sorted set中的指定元素                              |
| ZSCORE key member            | 獲取sorted set中指定元素的score值                       |
| ZRANK key member             | 獲取sorted set中指定元素的排名                          |
| ZCARD key                    | 返回sorted set中的元素個數                              |
| ZCOUNT key min max           | 統計score值在給定範圍內的元素個數                       |
| ZINCRBY key increment member | 讓sorted set中的指定元素自增，步長為指定的increment值   |
| ZRANGE key min max           | 按照score排序後，獲取指定排名範圍內的元素               |
| ZRANGEBYSCORE key min max    | 按照score排序後，獲取指定score範圍內的元素              |
| ZINTER/ZDIFF/ZUNION          | 交集．差集．聯集                                        |
