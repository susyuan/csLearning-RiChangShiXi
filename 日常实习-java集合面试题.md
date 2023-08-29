# 日常实习-java集合面试题



# ArrayList

## 讲一讲arraylist

底层是object数组，相当于动态数组，容量能动态增长；

默认**初始容量10**

会自动扩容，扩容变为1.5倍

## ArrayList和LinkedList的区别

1. **线程安全：**都无法保证线程安全
2. **底层数据结构：**Object数组  和双向循环链表数据结构
3. **插入和删除元素是否受元素位置影响**：略
4. **是否支持快速随机访问：**arraylist支持随机访问
5. **内存空间占用：**一个会浪费尾部的空间 一个每个节点都消耗更多的空间存后继前驱



1.arrayList和LinkedList在实现层面和使用场景有什么差别？

2.arrayList为什么**查询的时候比较快？****支持随机访问**

3.arrayList和LinkedList**扩容**上面有什么差别？ 一个需要复制原数组 

## 本身支持数组，为什么还要用ArrayList和LinkedList？

1. 更多内置方法
2. 支持**动态扩容**
3. linkedlist用于链表的存储

## 源码

## 初始化容量 扩容机制

1. 首先，add方法添加前 调用方法 **判断是否够容量** ensureaCap 传入min+1
2. 计算容量 返回**默认容量和mincap**的最大值
3. 如果容量满足就直接添加 否则调用**grow方法扩容**
4. grow 扩容为原来1.5倍，然后复制原来的数组到新的空间



添加前确保容量够，如果容量不够mincap-length 用grow函数扩容

```java
 int newCapacity = oldCapacity + (oldCapacity >> 1);
```

默认情况下，新的容量会是原容量的1.5倍。

扩容过程：计算出新的**扩容数组的size后实例化**，并将**原有数组内容复制**到新数组中去。

# HashSet

不能添加相同元素  根据hashcode+equals 判断元素是否相同

放入自己创建的类，类里面要重写这两个方法hashcode+equals

重写equals要重写hashcode；

相同对象要有相同的散列码

# LinkeList

## --底层

双向链表

# （重点）HashMap

## 介绍HashMap

HashMap基于Map接口实现，存储键值对，是非线程安全的

可以存储**null键值**，null作为键只能出现一次

默认初始化大小**16**，每次扩容为原来2倍，总是使用2的幂作为哈希表大小

Hash数组存储  **Node节点**，Node节点实现了Entry接口 本质上是键值对

这个数组里可以存储元素的位置被称为“桶（bucket）”，每个 bucket 都有其指定索引，系统可以根据其索引快速访问该 bucket 里存储的元素。 

无论何时，HashMap 的每个“桶”只存储一个元素（也就是一个 Entry）

## Hashmap原理（底层数据结构）（底层源码）

存储时通过key.hashcode处理后得到hash值，再hash&(length-1)得到位置

1.8之前由**数组+链表**组成，链表是为了解决哈希冲突

1.8是 **数组+链表+红黑树**组成；链表红黑树一定条件转换

- 当链表**超过** 8 且数据总量超过 **64** 才会转红黑树。
- 将链表转换成红黑树前会判断，如果当前数组的**长度小于 64**，那么会选择先进行数组扩容，而不是转换为红黑树，以减少搜索时间。

## （关键）put方法流程

三个版本图

版本1

![image-20230720145229290](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307201452338.png)

javaguide流程

![ ](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202308031112367.png)

![image-20230825153241466](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202308251532533.png)

## 讲讲HashMap的扩容

HashMap 在容量超过**负载因子**所定义的容量之后，就会扩容。

threshold是HashMap所能容纳键值对的最大值。threshold = length * Load factor。 默认Load factor是 0.75



Java 里的数组是无法自动扩容的，方法是将 HashMap 的大小扩大为原来数组的**两倍**，并将原来的对象放入新的数组中。

**resize方法**

1.7 初始化新的更大容量的数组，然后 重新计算hash值，转移数据 修改threshold

## HashMap中key的存储索引是怎么计算的？

key得到hashcode值，根据hashcode计算hash值，再取模

## 解决hash冲突的方案

**开放地址法**，一旦产生了冲突（该地址已有其它元素），就按某种规则去寻找另一空地址

> 线性探测法 +i
>
> 平方探测法  +-i^2

再哈希法，冲突时用不同哈希函数

**链地址法**，哈希值相同的元素用一个链表连起来

HashMap采用 链地址法

## key可以为空吗

可以 但只能有一个

## hashmap的容量为什么设置为2^n？

hashmap 的哈希函数 的值范围很大，hash函数的结果要对数组长度**取模**，而二进制&比取模%效率更高  (length-1)&hash == hash %length的前提是length是2^n

## hashmap从哪个版本用红黑树？为什么改用红黑树？

1.8；为了减少查询链表的复杂度；加快查询速度O(logn)

直接用红黑树的话 新增节点的效率变慢

## 为什么HashMap链表转红黑树的阈值为8呢

当元素小于 8 个的时候，此时做查询操作，链表结构已经能保证查询性能。红黑树需要进行左旋，右旋，变色这些操作来保持平衡

泊松分布， 8 个键值对同时存在于同一个桶的概率非常低

8时候 平均查找效率是 3和4

## 红黑树是什么？集合里的红黑树是怎么用的？

红黑树是特殊的平衡二叉树，插入删除比AVL有优势

## 能获得键值都为null

可以

## hashmap多线程使用会有问题吗？有什么问题呢？

三个问题

![image-20230720143556934](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307201435991.png)

多线程环境下**扩容操作可能存在死循环问题**，这是由于当一个桶位中有多个元素需要进行扩容时，多个线程同时对链表进行操作，头插法可能会导致链表中的节点指向错误的位置，从而形成一个环形链表，进而使得查询元素的操作陷入死循环无法结束

多线程的put可能覆盖数据，导致数据丢失

put时超出threshold导致rehash 线程2执行get

## hashmap是线程不安全的，如果想要保证线程安全，需要怎么做？（解决hashmap多线程问题？

（答：使用ConcurrentHashMap）

# （重点）ConcurrentHashMap

## HashMap 和 ConcurrentHashMap 区别

1 线程安全

2一个没锁 一个对每个Node节点加锁

3  ConcurrentHashMap 允许并发扩容，HashMap并发扩容可能导致死循环

## concurrentHashmap 实现原理（两个版本）

**1.7版本**

1.7中，数据分为一段段segment，每一段配一把锁，由segment数组和hashentry数组组成，并发度16，segment类似hashmap数组的结构，一个 `Segment` 数组包含多个 `HashEntry` 组

<img src="https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307312125317.png" alt="image-20230731212530250" style="zoom:50%;" />

1.8 取消segment ，采用Node + CAS + synchronized 类似hashmap1.8的结构 会转变红黑树，锁的粒度更细，只锁定 链表/红黑树的首节点，只要hash值不冲突就不产生并发

<img src="https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307191947667.png" alt="Java8 ConcurrentHashMap 存储结构" style="zoom:50%;" />

## JDK1.7与JDK1.8 中ConcurrentHashMap 的区别？

- 数据结构：取消了Segment分段锁的数据结构，取而代之的是**数组+链表+红黑树**的结构。
- **保证线程安全机制**：JDK1.7采用**Segment的分段锁机制**实现线程安全，其中segment继承自ReentrantLock。JDK1.8 采用**CAS+Synchronized**保证线程安全。
- **锁的粒度**：原来是对需要进行数据操作的Segment加锁，现调整为对每个数组元素加锁（Node）。
- **链表转化为红黑树**:定位结点的hash算法简化会带来弊端,Hash冲突加剧,因此在链表节点数量大于8时，会将链表转化为红黑树进行存储。
- **查询时间复杂度**：从原来的遍历链表O(n)，变成遍历红黑树O(logN)。

1.锁方式

2.链表变红黑树/链表

3.并发度  16的并发度 对 node数组中node节点数量





## 分段锁分了多少段？

16端 segment

## （重点）ConcurrentHashMap put方法流程

put方法加锁， 判断首节点，

![image-20230720151745440](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307201517480.png)



**先来看JDK1.7**
首先，会尝试获取锁，如果获取失败，利用自旋获取锁；如果自旋重试的次数超过 64 次，则改为阻塞
获取锁。
获取到锁后：

1. 将当前 Segment 中的 table 通过 key 的 hashcode 定位到 HashEntry。
2. 遍历该 HashEntry，如果不为空则判断传入的 key 和当前遍历的 key 是否相等，相等则覆盖旧的
value。
3. 不为空则需要新建一个 HashEntry 并加入到 Segment 中，同时会先判断是否需要扩容。
4. 释放 Segment 的锁。

**再来看JDK1.8**(重点)
大致可以分为以下步骤：

1. 根据 key 计算出 **hash值。**
2. 判断是否需要进行**初始化**。
3. 定位到 Node，拿到首节点 f，判断首节点 f：
  1. 如果为 null ，则通过cas的方式尝试添加。
  2. 如果为 `f.hash = MOVED = -1` ，说明其他线程在扩容，参与一起扩容。
  3. 如果都不满足 ，`synchronized `锁住 f 节点，判断是链表还是红黑树，遍历插入。
4. 当在链表长度达到8的时候，数组扩容或者将链表转换为红黑树。

## ConcurrentHashMap是怎么保证线程安全的，底层时是使用什么手段加锁？ -->如果要做并发度优化的话，你会怎么考虑？