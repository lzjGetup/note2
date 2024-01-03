# RDB
>![[Pasted image 20231219124754.png]]

>![[Pasted image 20231219143331.png]]

>![[Pasted image 20231219150113.png]]

# AOF
![[Pasted image 20231219150449.png]]

![[Pasted image 20231219150506.png]]
![[Pasted image 20231219150708.png]]
![[Pasted image 20231219151159.png]]

![[Pasted image 20231219151600.png]]


# Redis主从集群
### 搭建简略过程

#### 集群结构:
**修改redis.conf文件**:
1. 修改每个结点的端口
2. 开启RDB模式(数据快照) --save 3600 1
3. 关闭AOF模式  --appendonly no

**设置主从关系**:
永久:
在redis.conf中添加一行配置：```slaveof <masterip> <masterport>```
暂时:
使用redis-cli客户端连接到redis服务，执行**slaveof**命令（重启后失效）
  ```sh
  slaveof <masterip> <masterport>
  ```
**注意**:在5.0以后新增命令replicaof，与salveof效果一致


#### 哨兵模式:
##### 配置:
==sentinel.conf==
```ini
port 27001
sentinel announce-ip 192.168.150.101 
sentinel monitor mymaster 192.168.150.101 7001 2 
sentinel down-after-milliseconds mymaster 5000
sentinel failover-timeout mymaster 60000
dir "/tmp/s1"
```

**port** 27001：这一行指定了Redis Sentinel的端口号，即Sentinel服务将在27001端口上监听来自客户端的连接。
**sentinel announce-ip** 192.168.150.101：这一行声明了master主机的IP地址为192.168.150.101。这个配置项用于告知其他Sentinel和Redis实例关于master主机的IP地址。
**sentinel monitor mymaster** 192.168.150.101 7001 2：这一行指示Sentinel监控一个名为mymaster的Redis实例。它告诉Sentinel在IP地址为192.168.150.101、端口号为7001的Redis实例上监控名为mymaster的主服务器。数字2表示在判断主服务器不可达后，Sentinel需要多少个Sentinel同意才能进行故障转移。
**sentinel down-after-milliseconds** mymaster 5000：这一行指定了在多少毫秒之后Sentinel认为主服务器不可达。在这里，它设置为5000毫秒（即5秒）。
**sentinel failover-timeout** mymaster 60000：这一行指定了在多少毫秒之后Sentinel可以开始执行故障转移。在这里，它设置为60000毫秒（即60秒）。
dir "/tmp/s1"：这一行指定了Sentinel的工作目录，即"/tmp/s1"。这个目录将用于存储Sentinel的运行时数据。

##### 启动:
```sh
# 启动哨兵
redis-sentinel [配置文件的路径]/sentinel.conf
```



## Redis分片集群

### 修改配置文件
**在/tmp下准备一个新的redis.conf文件，内容如下：**
```ini
port 6379
# 开启集群功能
cluster-enabled yes
# 集群的配置文件名称，不需要我们创建，由redis自己维护
cluster-config-file /tmp/6379/nodes.conf
# 节点心跳失败的超时时间
cluster-node-timeout 5000
# 持久化文件存放目录
dir /tmp/6379
# 绑定地址
bind 0.0.0.0
# 让redis后台运行
daemonize yes
# 注册的实例ip
replica-announce-ip 192.168.150.101
# 保护模式
protected-mode no
# 数据库数量
databases 1
# 日志
logfile /tmp/6379/run.log
```

### 创建集群
==Redis5.0之后==
```sh
redis-cli --cluster create --cluster-replicas 1 192.168.150.101:7001 192.168.150.101:7002 192.168.150.101:7003 192.168.150.101:8001 192.168.150.101:8002 192.168.150.101:8003
```

命令说明：
- `redis-cli --cluster`或者`./redis-trib.rb`：代表集群操作命令
- `create`：代表是创建集群
- `--replicas 1`或者`--cluster-replicas 1` ：指定集群中每个master的副本个数为1，此时`节点总数 ÷ (replicas + 1)` 得到的就是master的数量。因此节点列表中的前n个就是master，其它节点都是slave节点，随机分配到不同master

==查看集群状态==

```sh
redis-cli -p 7001 cluster nodes
```

集群操作时，登录客户端,需要给`redis-cli`加上`-c`参数才可以：

```sh
redis-cli -c -p 7001
```



==已知搭建了三个redis服务器==
>![[Pasted image 20231219152950.png]]

# 主从数据同步原理
>![[Pasted image 20231219154021.png]]

>![[Pasted image 20231219154427.png]]

# 全量同步过程

>![[Pasted image 20231219154838.png]]


# 增量同步

>![[Pasted image 20231219183929.png]]

>![[Pasted image 20231219184656.png]]

# Redis哨兵
>![[Pasted image 20231219184947.png]]

>![[Pasted image 20231219185138.png]]

==Master宕机情况下,如何选举slave==

>![[Pasted image 20231219185409.png]]

>![[Pasted image 20231219185554.png]]

==哨兵配置文件详解==
>![[Pasted image 20231219190101.png]]

## redisTemplate
>![[Pasted image 20231219190922.png]]

>![[Pasted image 20231219191809.png]]


==具体内容:==
[springboot下的哨兵配置](https://www.bilibili.com/video/BV1cr4y1671t?p=107&spm_id_from=pageDriver&vd_source=c9f01c4138ffca623361215fe6c00336)

# Redis分片集群

>![[Pasted image 20231219201031.png]]

>![[Pasted image 20231219201121.png]]

# 手动故障转移
==实现数据迁移==


>![[Pasted image 20231221100547.png]]


# RedisTemplate实现分片集群

>![[Pasted image 20231221100858.png]]
















