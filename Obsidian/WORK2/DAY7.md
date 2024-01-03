# 搭建Nginx集群

例如,如下模拟,在window下的Nginx将来自客户端的请求反向代理到虚拟机的Openresty中的Nginx集群中进行业务处理

```Nginx
upstream nginx-cluster{
        server 127.0.0.1:8081;
    }
location /api {
            proxy_pass http://nginx-cluster;
        }
```

**/api 拦截请求
proxy_pass 反向代理到集群
server (集群ip)(端口)**

### 虚拟机集群配置


>![[Pasted image 20231221204947.png]]

# OpenResty请求参数解析
>![[Pasted image 20231221213705.png]]

先尝试向Tomcat发出请求
==由于Nginx部署在虚拟机,W11和虚拟机的ip不一致,我们可以做如下操作==
>![[Pasted image 20231221215236.png]]

## 封装get请求工具类


>![[Pasted image 20231221215743.png]]

==引用工具类==
```lua
local common = require('common')
local read_http = common.read_http
```

## 序列化与反序列化数据

>![[Pasted image 20231222132832.png]]

# Redis 缓存预热

>![[Pasted image 20231222133735.png]]

其中,用`RedisHander`继承`InitializingBean`
需要实现`afterPropertiesSet()`方法
作用是,在初始化Bean后和依赖注入后,执行该方法,实现业务功能


# OpenResty的Redis模块

>![[Pasted image 20231222141352.png]]

`red.set_timeouts()`的三个参数含义
**连接超时**：指尝试连接到Redis服务器的最长时间。
**读取超时**：指从Redis服务器读取数据的最长时间。
**写入超时**：指向Redis服务器写入数据的最长时间。


# Nginx本地缓存

>![[Pasted image 20231222142704.png]]












