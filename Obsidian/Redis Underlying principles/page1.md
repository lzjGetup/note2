
# Redis底层数据类型

**SDS（Simple Dynamic String）**：简单动态字符串，是 Redis 用来表示字符串值的抽象数据结构。SDS 除了保存字符串内容外，还记录了字符串长度、可用空间长度等信息，使得对字符串的操作更为高效。

**IntSet（整数集合）**：用于保存整数值的数据结构，它可以在特定条件下将小整数编码成整数集合对象，从而节省内存。

**压缩列表（ziplist）**：是 Redis 用来表示列表和哈希表的底层实现之一。它通过将多个小数据结构紧凑地存储在一起，以节省内存空间。

**跳跃表（skiplist）**：用于有序集合的底层实现，它通过多层次的链表结构实现了快速的查找和插入操作，是一种高效的数据结构。

**哈希表（dict）**：用于实现 Redis 的键值对存储结构，它通过哈希算法将键映射到对应的值，实现了快速的查找和插入操作。

**对象（object）**：Redis 的所有数据结构都是以对象的形式存在的，包括字符串对象、列表对象、哈希对象等。对象包含了类型、编码、值等信息，是 Redis 数据操作的基础。



# 动态字符串SDS

>![[Pasted image 20231223093119.png]]

>![[Pasted image 20231223093659.png]]


# IntSet
>![[Pasted image 20231223094230.png]]

>![[Pasted image 20231223101229.png]]

>![[Pasted image 20231223101623.png]]


# Dict

>![[Pasted image 20231223104224.png]]

>![[Pasted image 20231223104450.png]]

==当哈希表中的元素增加或者减少时,哈希表会进行扩容或收缩,使得哈希碰撞和内存节省达到平衡==

>![[Pasted image 20231223105612.png]]

>![[Pasted image 20231223110413.png]]

![[Pasted image 20231223111232.png]]


# ZipList

>![[Pasted image 20231223112716.png]]

>![[Pasted image 20231223112749.png]]


>![[Pasted image 20231223115155.png]]


>![[Pasted image 20231223115505.png]]
>

>![[Pasted image 20231223120148.png]]


![[Pasted image 20231223132353.png]]


# QuickList

>![[Pasted image 20231223133241.png]]

>![[Pasted image 20231223133614.png]]

![[Pasted image 20231223133938.png]]


# SkipList

>![[Pasted image 20231223134925.png]]


>![[Pasted image 20231223135456.png]]

>![[Pasted image 20231223135508.png]]

# RedisObject

>![[Pasted image 20231223140335.png]]


>![[Pasted image 20231223140456.png]]

>![[Pasted image 20231223140756.png]]


# 详析五种数据类型

![[Pasted image 20231223142434.png]]



>![[Pasted image 20231223142358.png]]


>![[Pasted image 20231223193345.png]]

>![[Pasted image 20231223193455.png]]

>![[Pasted image 20231223194338.png]]


>![[Pasted image 20231223194820.png]]


==Zset内部存储结构之一,属于HT+ZipList相结合的方式,较消耗内存;因此,当元素比较少时,Zset一般只采用ZipList的底层数据结构==


>![[Pasted image 20231223195903.png]]


>![[Pasted image 20231223202205.png]]

>![[Pasted image 20231223204136.png]]









