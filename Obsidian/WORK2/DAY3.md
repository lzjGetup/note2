# 可重入锁的实现流程
>![[Pasted image 20231031185000.png]]
# Redission分布式锁原理
>![[Pasted image 20231031191747.png]]

>![[Pasted image 20231031192015.png]]

>![[Pasted image 20231031201418.png]]

# 消息队列
>![[Pasted image 20231102111520.png]]
## 基于list
>![[Pasted image 20231102111737.png]]

>![[Pasted image 20231102112129.png]]

## 基于PubSub
>![[Pasted image 20231102112534.png]]

>![[Pasted image 20231102112935.png]]

## 基于Stream
>![[Pasted image 20231102114233.png]]


`XADD s1 * name ling`
s1为消息队列名
name ling 为key-value 实体


>![[Pasted image 20231102114450.png]]

## 消费者组
>![[Pasted image 20231102115220.png]]

>![[Pasted image 20231102132051.png]]


`XGROUP CREATE s1 g1 0`
s1为消息队列名
g1为消费组名


>![[Pasted image 20231102150938.png]]

`XREADGROUP GROUP g1 c3 COUNT 1 BLOCK 2000 STREAMS s1 >`
g1:消费组名
c3:消费者名
2000:阻塞等待时间
s1:消息队列源


`XGROUP CREATE stream g1 0 MKSTREAM `
该命令可以实现创建消费者组的同时,倘若未创建stream消息队列,同时会创建消息队列.


>![[Pasted image 20231102154202.png]]

>![[Pasted image 20231102154309.png]]








