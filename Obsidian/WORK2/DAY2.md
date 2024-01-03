# 全局ID生成器
>![[Pasted image 20231028212734.png]]

>![[Pasted image 20231028223012.png]]

# 超卖问题

==多线程并发执行时发生==
>![[Pasted image 20231029120028.png]]

==乐观锁==
*版本号法*:用版本号对应记录当前查询的数据,再次修改时,倘若版本不一致,则不修改.
*CAS法*:在数据set更新操作前,先进行比较,在考虑是否更新.

==单机模式下,对创建优惠券订单方法执行前加锁,并让spring管理事务==
```java
Long userId = UserHolder.getUser().getId();  
    synchronized (userId.toString().intern()) {  
        //获取事务代理对象  
        IVoucherOrderService proxy = (IVoucherOrderService) AopContext.currentProxy();  
        return proxy.createVoucherOrder(voucherId);  
    }
```

# 分布式锁
==概念==
满足分布式系统或集群模式下多进程可见并且互斥的锁
>![[Pasted image 20231029161133.png]]


## 存在的问题
>![[Pasted image 20231029170638.png]]

*某些进程由于阻塞,导致锁被超时释放;从而其他进程获取锁,当进程一阻塞结束时,又释放了别的进程的锁,导致锁再次被获取.*
## 改进方案
>![[Pasted image 20231029172409.png]]


# Redis里的lua脚本
>![[Pasted image 20231030185906.png]]

![[Pasted image 20231030191952.png]]

>![[Pasted image 20231030193930.png]]

## 仍存在的问题
>![[Pasted image 20231030194437.png]]

# 基于Redisson获取分布式锁
>![[Pasted image 20231030200849.png]]

>![[Pasted image 20231030200908.png]]





