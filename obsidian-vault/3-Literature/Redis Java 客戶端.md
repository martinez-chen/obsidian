#output #redis  #permanent 

Redis 官方推荐的 Java 客户端有Jedis、lettuce 和 Redisson

## Jedis
Jedis 是老牌的 Redis 的 Java 實現客戶端，提供了比較全面的 Redis 命令的支持，其官方網址是：[https://github.com/redis/jedis](https://github.com/redis/jedis)

- 優點：
	 
    支持全面的 Redis 操作特性（可以理解為API比較全面）。
    
- 缺點：
    
    使用阻塞的 I/O，且其方法調用都是同步的，程序流需要等到 sockets 處理完 I/O 才能執行，不支持異步； Jedis 客戶端實例不是線程安全的，所以需要通過連接池來使用 Jedis。

---
## lettuce

是一種可擴展的線程安全的 Redis 客戶端，支持異步模式。如果避免阻塞和事務操作，如BLPOP和MULTI/EXEC，多個線程就可以共享一個連接。lettuce 底層基於 Netty，支持高級的 Redis 特性，比如哨兵，集群，管道，自動重新連接和Redis數據模型。lettuce 的官網地址是：[https://lettuce.io/](https://lettuce.io/)

- 優點：
    
    支持同步異步通信模式； Lettuce 的 API 是線程安全的，如果不是執行阻塞和事務操作，如BLPOP和MULTI/EXEC，多個線程就可以共享一個連接。

---

## Redision
Redisson 是一個在 Redis 的基礎上實現的 Java 駐內存數據網格（In-Memory Data Grid）。它不僅提供了一系列的分佈式的 Java 常用對象，還提供了許多分佈式服務。其中包括( BitSet, Set, Multimap, SortedSet, Map, List, Queue, BlockingQueue, Deque, BlockingDeque, Semaphore, Lock, AtomicLong, CountDownLatch, Publish / Subscribe, Bloom filter, Remote service, Spring cache, Executor service, Live Object service, Scheduler service) Redisson 提供了使用Redis 的最簡單和最便捷的方法。Redisson 的宗旨是促進使用者對Redis的關注分離（Separation of Concern），從而讓使用者能夠將精力更集中地放在處理業務邏輯上。Redisson的官方網址是：[https://redisson.org/](https://redisson.org/)

- 優點：
    
    使用者對 Redis 的關注分離，可以類比 Spring 框架，這些框架搭建了應用程序的基礎框架和功能，提升開發效率，讓開發者有更多的時間來關注業務邏輯； 提供很多分佈式相關操作服務，例如，分佈式鎖，分佈式集合，可通過Redis支持延遲隊列等。
    
- 缺點：
    
    Redisson 對字符串的操作支持比較差。

---

## RedisTemplate

- 優點：
    
    redisTemplate的好处就是基于springBoot自动装配的原理，使得整合redis时比较简单。
    
- 缺點：
    
    效能差。
    

可透過調整序列化器，達成自動序列化，預設為JdkSerializationRedisSerializer，底層為ObjectOutputStream，浪費空間且難以閱讀。

使用GenericJackson2JsonRedisSerializer則會存入序列化型別可直接完成轉型，但浪費效能及空間。

---
## 使用建議

結論：lettuce + Redisson

Jedis 和 lettuce 是比較純粹的 Redis 客戶端，幾乎沒提供什麼高級功能。Jedis 的性能比較差，所以如果你不需要使用 Redis 的高級功能的話，優先推薦使用 lettuce。

Redisson 的優勢是提供了很多開箱即用的 Redis 高級功能，如果你的應用中需要使用到 Redis 的高級功能，建議使用 Redisson。具體 Redisson 的高級功能可以參考：[https://redisson.org/](https://redisson.org/)