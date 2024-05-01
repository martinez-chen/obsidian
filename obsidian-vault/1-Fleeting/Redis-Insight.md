redis-insight
使用docker安裝後無法連接docker中的redis
可能須建立docker中的network

目前解決方式：使用 docker-compose.yaml 建立 redis-insignt
連接時hostname使用 container name (redis)
```
redisinsight:  
  image: redislabs/redisinsight:latest  
  container_name: redisinsight  
  ports:  
    - "5540:5540"
```