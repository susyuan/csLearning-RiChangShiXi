# 日常实习-java并发面试题

7.18搜集完毕 整理完 还有些没答案

# 多线程基础

## 什么是进程

进程 

1是程序的**动态执行**过程，一个程序运行就是**进程创建运行到消亡**的过程

2是资源分配的独立实体

3进程有独立的地址空间

4进程访问别的进程的变量需要进程间通信

## 为什么要多线程

1一个进程要执行多个任务，

2程序要实现一些需要等待的任务  用户输入

## 线程和进程区别

一个进程中可以有多个线程

根本：进程是操作系统**资源分配**的基本单位，而线程是**处理器任务调度和执行**的基本单位

开销：进程切换开销大，有独立的代码和数据空间；线程有自己独立的运行栈和PC

内存分配：同一进程的线程共享本进程的地址空间和资源，而进程之间的地址空间和资源是相互独立的

## 线程之间怎么共享资源

volatile修饰变量

保证了不同线程对这个变量进行操作时的可见性，即一个线程修改了某个变量的值，这新值对其他线程来说是立即可见的。

## 多线程创建方式

四种

## 如何启动线程

调用线程的start方法，会执行重写的run方法

## 线程生命周期（线程状态及切换

new runnanbe（start()后） running blocked dead

五种状态

![image-20230718225250980](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307182252034.png)

## 上下文切换有啥操作

1. 时间片用完 CPU调度

2. 中断处理 请求IO操作

3. 某种原因阻塞

4. 某种原因主动放弃CPU

5. 线程执行结束

6. 出现异常终止


## 几种方式实现加锁

Reentralock

synchronized

## 同步异步区别

- **同步**：发出一个调用之后，在没有得到结果之前， 该调用就不可以返回，一直等待。
- **异步**：调用在发出之后，不用等待返回结果，该调用直接返回。

## 线程不安全

多线程访问同一份数据，可能导致**数据混乱错误**

## 多线程怎么实现同步？

lock 

syn

## 几种方式实现加锁？

lock 

syn

## 死锁的必要条件

- 互斥条件；
- 持有并等待条件；
- 不可剥夺条件；
- 环路等待条件；

## 乐观锁 悲观锁

乐观锁总是假设最好的情况，认为共享资源的访问不会出问题，不用加锁，只是提交修改的时候验证是否被其他线程修改

1.高并发性能梗好

2.频繁冲突，会频繁重试

悲观锁假设最坏情况，认为每次访问都会有问题，每次加锁，共享资源只能一个线程使用，其他线程阻塞；

1.高并发的场景下，激烈的锁竞争会造成线程阻塞，大量阻塞线程会导致系统的上下文切换，增加系统的性能开销。

2.死锁

乐观锁一般用**版本号orCAS**实现

## 进程级别锁解决什么问题

## 分布式锁解什么问题

##  可重入锁 

线程可以**再次获取自己的内部锁**，获取某个对象锁后，可以再次获取这个对象的锁

 syn和lock都是可重入锁

##  公平锁和非公平锁

公平：锁释放后，先申请的线程先得到锁，性能较差

非公平，锁释放后，后申请的线程可能会先得到锁

## --volatile如何保证变量可见性

将变量声明为 **`volatile`** ，这就指示 JVM，这个变量是共享且不稳定的，每次使用它都到主存中进行读取。

# 常见对比

## sleep 和 wait 方法

相同点: 都能让进程阻塞（暂停线程的执行）

不同

1.方法声明位置：thread是thread类声明sleep  object类声明wait

2.方法调用位置：sleep 任何地方调用 wait要在同步代码块/同步方法下

3.释放锁：sleep不会释放锁\wait会释放锁

4.用途`wait()` 通常被用于线程间交互/通信，`sleep()`通常被用于暂停执行。

5.线程如何苏醒：`wait()` 方法被调用后，线程不会自动苏醒，需要别的线程调用同一个对象上的 `notify()`或者 `notifyAll()` 方法。`sleep()`方法执行完成后，线程会自动苏醒，或者也可以使用 `wait(long timeout)` 超时后线程会自动苏醒。

## Runnable和callable的区别；

1.接口需要实现的方法不同 run call

2.Runnable接口的run0方法不能指定返回值，而Callable接口的call0方法是允许我们指定返回值的，返回值类型是一个泛型。我们可以futrueTask.get0方法获取到线程执行结果，但是注意此方法会阻塞主线程执行，直到子线程任务执行完成并返回结果。

3.Runnable接口的run0方法不能**抛出异常**，只能在方法内部处理;而Callable接口的call0方法是允许我们抛出异常的;



## synchronized和volatile的区别

volatile是线程同步的轻量级实现，只能作用于变量，syn可以代码块/方法

volatile可以保证数据**可见性**不能保证**原子性**  syn都能保证

volatile 解决变量多个线程可见性；syn解决多个线程访问资源的同步性

# 线程池

## 线程池的理解

是池化技术，资源复用的设计思想，类似数据库连接池，复用线程资源

好处

- **降低资源消耗**。通过重复利用已创建的线程降低**线程创建和销毁**造成的消耗。
- **提高响应速度**。不需要等到线程创建就能立即执行任务。
- **提高线程的可管理性**，通过线程池统一分配管理线程，避免无休止创建线程

## 线程池好处

- **降低资源消耗**。通过重复利用已创建的线程降低**线程创建和销毁**造成的消耗。
- **提高响应速度**。不需要等到线程创建就能立即执行任务。
- **提高线程的可管理性**，通过线程池统一分配管理线程，避免无休止创建线程

## 可以直接用sdk提供的创建线程池的方法吗？

fixe和single 无界队列 队列中可能堆积大量请求

cache 没有限制最大线程数量，可能创造大量线程来处理任务

schedule可能堆积大量请求 无界延迟队列

threadpoolexecutor更可能避免资源耗尽，且掌控粒度更细致

（不可以，从掌控粒度粗，自定义线程池可以重写钩子函数方法解答）

## 怎么创建一个线程池？

1ThreadPoolExecutor 构造函数创建

2 Executor框架工具类 Executors创建 有多种类型的线程池

## 哪几种常见线程池

> newCachedThreadPool
>
> newFixedThreadPool
>
> newSingleThreadPool
>
> newScheduleThreadPool

**fixed**threadpool 固定线程数量的线程池 核心和最大都是固定值

**single**threadexecutor 一个线程的线程池 

cached~ 可根据实际情况调整 没有限制最大线程数量，阻塞队列不存储元素

scheduled~  给定的延迟后**运行任务或定期执行任务**

## 线程池参数 7

7个 

核心线程数corePoolsize：核心线程大小，线程池一直运行，核心线程就不会停止。

最大线程数maximumpoolsize。

阻塞队列：用来储存等待**执行任务**的队列

拒绝策略：当提交的任务过多而不能及时处理时，我们可以定制策略来处理任务

- **Abort**Policy ： 线程任务丢弃报错。默认饱和策略。
- **Discard**Policy ： 线程任务直接丢弃不报错。
- **DiscardOldest**Policy ： 将workQueue队首任务丢弃，将最新线程任务重新加入队列执行。
- **CallerRuns**Policy ：线程池之外的线程直接调用run方法执行。

空闲等待时间

线程制造工厂

时间单位

## 线程池阻塞队列 3

1. LinkedBlockingQueue无界队列 不会被放满  fixed和single使用
2. `SynchronousQueue`（同步队列） 不存储元素  cached使用
3. delayedworkqueue 延迟阻塞队列 按延迟的时间长短排序，   scheduledthreadpool使用

## 阻塞队列与非阻塞队列对比

## 如何设计线程数量corepoolsize

线程数过大 争取CPU资源 频繁切换

过小会导致大量任务在队列中排队

**CPU密集型  N+1**  N是CPU核心数 多一个线程防止其他原因导致任务暂停带来的影响

**I/O密集型 2N** 多配置线程，CPU空闲可供其他线程使用

## 线程池执行流程

即 线程池处理任务的流程

![图解线程池实现原理](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307182157900.png)

1.线程池执行execute/submit方法向线程池添加任务，当任务小于核心线程数corePoolSize，线程池
中可以创建新的线程。

2.当任务大于核心线程数corePoolSize，就向阻塞队列添加任务。

3.如果阻塞队列已满，需要通过比较参数maximumPoolSize，在线程池创建新的线程，当线程数量
大于maximumPoolSize，说明当前设置线程池中线程已经处理不了了，就会执行饱和策略。

##  线程池提交execute和submit有什么区别

execute用于提交**不返回结果**的任务

submit是提交有返回结果的任务 返回future类型对象，通过future的get获取返回值

## ==线程池异常怎么处理==



## 饱和策略4

如果当前同时运行的线程数量达到最大线程数量并且队列也已经被放满了任务时

1. abortpolicy 默认的策略 拒绝新任务 **抛出异常**
2. callerrunspolicy 调用自己的线程运行任务用，也就是**直接在调用`execute`方法的线程**中运行(`run`)被拒绝的任务
3. discard~ 对该任务不处理 直接丢掉**不报错**
4. discardoldest~丢弃**最早的未处理**的任务

# JMM

## 简单说一下java内存模型JMM

java内存模型和java运行时内存区域不是一个概念

---

Java 内存模型(Java Memory Mode)是一种规范，用于描述 Java 虚拟机 （JVM)中多线程情况下，线程之间如何协同工作，如何共享数据，并保证多线程的操作在各个线程之间的可见性、有序性和原子性。

具体定义如下:

- 所有的变量都存储在**主内存(Main Memory)**中。
- 每个线程都有一个私有的本地内存(Local Memory)，本地内存中存了该线程以读/写共享变量的拷贝副本
- 线程对变量的所有操作都必须在**本地内存**中进行，而不能直接读写主内存。
- 不同的线程之间无法直接访问对方本地内存中的变量，线程间共享变量时，通过**主内存**来实现通信、协作和传递信息。

Java内存模型的抽象图:

![JMM(Java 内存模型)](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307171612471.png)

主内存作用存储所有共享变量，供线程进行读取

线程从主内存读取x 会在自己的工作内存存储一个x变量副本  

线程a更新x=1 放入主内存  线程b读取主内存x=1 修改为x=2 放入主内存继续供其他线程读取

java是共享内存并发模型， 解决**消息同步和线程通信**问题

![image-20230717160909189](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307171609255.png)

私有的不会有共享问题  栈的变量不会共享 不受到内存模型影响

堆变量有内存可见性问题

JMM定义**线程和主内存的抽象关系**

## Java内存区域和JAVA内存模型区别

- JVM 内存结构和 Java 虚拟机的运行时区域相关，定义了 JVM 在运行时如何分区存储程序数据，就比如说堆主要用于存放对象实例。
- Java 内存模型和 Java 的并发编程相关，抽象了线程和主内存之间的关系就比如说线程之间的共享变量必须存储在主内存中，规定了从 Java 源代码到 CPU 可执行指令的这个转化过程要遵守哪些和并发相关的原则和规范，其主要目的是为了简化多线程编程，增强程序可移植性的。





# CAS

## 了解CAS吗（说说CAS

> 记住 V A B

CAS是比较和交换，通过处理器指令来保证操作原子性 包含三个操作数

V变量内存地址

A旧值

B准备设置的新址

V=A 才会更新B

## CAS原理及应用场景

cas用来保证堆共享数据操作的**原子性**

## CAS缺陷

ABA  中途变成B又改回A；添加版本号 每次更新追加版本号， 版本号和数据一致才更新数据

循环时间长开销大：长时间不成功会有很大开销

只能保证一个共享变量的原子操作：多个变量不行

## ABA问题及解决方案

 每次更新追加版本号， 版本号和数据一致才更新数据





# 并发集合（见集合篇）



## concurrentHashMap底层数据结构



## 1.8concurrenthashmap怎么实现



## ConcurrentHashMap是怎么保证线程安全的，底层时是使用什么手段加锁？ -->如果要做并发度优化的话，你会怎么考虑？



## CurrentHashMap 1.8版本put的过程



# Lock接口

## 实现类

## ReentrantLock的实现原理

这里似乎想问的是AQS）

## lock锁怎么实现等待可中断 可重入

# ThreadLocal

## 谈一下ThreadLocal；如何实现

ThreadLoacal是**线程本地变量**， 访问ThreadLocal变量的每个线程都会有这个**变量的一个本地拷贝**，多线程操作这个变量实际上是操作自己本地内存的副本；起到隔离作用，避免线程安全问题  即  **数据隔离**



应用：

使用：可以尝试使用ThreadLocal替代Session的使用，当用户要访问需要授权的接口的时候，可以现在拦截器中将用户的Token存入ThreadLocal中；之后在本次访问中任何需要用户用户信息的都可以直接冲ThreadLocal中拿取数据。

一般会生成静态字段

~~~java
static ThreadLocal<String> localName = new ThreadLocal();
localName.set("张三");
String name = localName.get();
localName.remove();
~~~

set

get

remove （不是必须 会自动回收

---

核心机制（原理）

- Thread类有ThreadLocalMap，每个线程都有自己ThreadLocalMap， 内部维护Entry数组，key是threadLocal本身，value是ThreadLocal的泛型值![ThreadLocal 数据结构](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307201030416.png)

- 每个线程在往ThreadLocal里设置值的时候，都是往自己的ThreadLocalMap里存，读也是以某个ThreadLocal作为引用，在自己的map里找对应的key，从而实现了线程隔离。
- 每个线程在往`ThreadLocal`里放值的时候，都会往自己的`ThreadLocalMap`里存，读也是以`ThreadLocal`作为引用，在自己的`map`里找对应的`key`，从而实现了**线程隔离**。
- `ThreadLocalMap`有点类似`HashMap`的结构，只是`HashMap`是由**数组+链表**实现的，而`ThreadLocalMap`中并没有**链表**结构。

(我从本质map、内存泄漏两方面谈起)

## 为什么产生内存泄漏

引用类型：

1.强引用：垃圾回收器绝不回收

2.软引用：内存空间不够就会回收

3.弱引用：垃圾回收器发现弱引用的对象就回收（只要垃圾回收机制一运行，不管JVM的内存空间是否充足，都会回收该对象占用的内存

4.虚引用：和没有引用一样，任何时候都能被回收

---

ThreadLocalMap的key是弱引用，value是强引用，key容易被回收，造成key没了value还在，因为tLmap生命周期和Thread是一样的，不做任何措施的话，value不会被垃圾回收，  

(weakReference 弱引用，使用线程池一般才会引起。强引用不会被gc回收)

## 如何解决内存泄漏

使用完threadlocal方法后手动调用remove方法

## threadlocal怎么修改获取数据

set方法修改

get方法获取

## local底层原理 用的什么数据结构

ThreadLocalMap

## ThreadLocal子线程能不能拿到父线程的值

拿不到，ThreadLocal线程隔离

# synchronized

## 底层实现原理

**1同步代码块**

 实现通过monitorenter和monitorexit指令，指明代码块开始和结束的位置，执行enter指令时线程试图获取锁 monitor对象，monitor对象位于java对象对象头中

内部有个**计数器** 计数器为0则获取锁对象成功

**2同步方法**

syn方法使用**ACC_synchronized**标识，表明这是一个同步方法，JVM识别后会进行同步调用

如果是实例方法，JVM 会尝试获取实例对象的锁。如果是静态方法，JVM 会尝试获取当前 class 的锁。



## 如何保证原子性



## `synchronized`可以作用在哪？

静态方法

非静态方法

代码块

## `synchronized`加在方法上，静态方法和非静态方法有什么区别？

静态：当前class的锁

非静态：当前对象实例的锁

## 除了syn还了解哪些锁

ReentrantLock

## 和lock锁区别 及使用区别 及性能

相同 都解决线程安全

不同

1.syn自动释放同步监视器 lock接口要手动释放/开启锁

2.lock可以实现更多功能，

3.syn可以给方法./代码块加索  lock只能给代码块加索

## 和ReentrantLock

synchronized 依赖于 JVM 而 ReentrantLock 依赖于 API

reentrantlock实现更多功能，公平锁or非公平锁

优先使用syn 

## syn做了哪些优化（锁升级

偏向锁 -> 轻量级锁 -> 重量级

偏向锁 在同一个线程获取的时候使用，第一次时社区锁对象的threadid=该线程id

不同线程获取就会变为轻量级锁 依靠CAS实现

重量级锁 操作系统实现  在轻量级锁CAS获取锁对象多次失败后



# AQS

## AQS是什么

> 资料：
>
> 1.【什么是AQS？2023Java面试题300集：阿里面试题！】https://www.bilibili.com/video/BV1h24y1W7gP?vd_source=622bb4e754ae1317fdc61d020ba5c5a9
>
> 2.javaguide AQS详解
>
> 3.[从ReentrantLock的实现看AQS的原理及应用 - 美团技术团队 (meituan.com)](https://tech.meituan.com/2019/12/05/aqs-theory-and-apply.html)
>
> 4.[Java并发之AQS详解 - waterystone - 博客园 (cnblogs.com)](https://www.cnblogs.com/waterystone/p/4920797.html)

AQS即 `AbstractQueuedSynchronizer`,即抽象队列同步器。

这个类在`java.util.concurrent.locks`包下面

AQS是一个抽象类，主要用来构建锁和同步器，需要被继承。

~~~java
public abstract class AbstractQueauedSynchronizer extends AbstractOwnableSynchronizer implements java.io.Serializable {
}

~~~

AQS 为构建锁和同步器提供了一些通用功能的实现，因此，使用 AQS 能简单且高效地构造出应用广泛的大量的同步器

>  比如我们提到的 `ReentrantLock`，`Semaphore`，其他的诸如 `ReentrantReadWriteLock`，`SynchronousQueue`等等皆是基于 AQS 的



![img](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202308022314486.png)

## AQS原理

> 在面试中被问到并发知识的时候，大多都会被问到“请你说一下自己对于 AQS 原理的理解”。下面给大家一个示例供大家参考，面试不是背题，大家一定要加入自己的思想，即使加入不了自己的思想也要保证自己能够通俗的讲出来而不是背出来。

### AQS核心思想

核心思想 分为 空闲和被占用两部分

如果被请求的共享资源空闲，则将当前请求资源的线程设置为有效的工作线程，并且将共享资源设置为**锁定状态。**

如果被请求的共享资源被占用，那么就需要一套线程阻塞等待以及被唤醒时锁分配的机制，这个机制 AQS 是基于 **CLH 锁** （Craig, Landin, and Hagersten locks） 实现的

下图是CLH队列结构

![CLH 队列](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202308022318962.png)

AQS主要特点

1.使用 **int 成员变量 `state` 表示同步状态**

> `state` 变量由 `volatile` 修饰，用于展示当前临界资源的获锁情况。
>
> ~~~java
> // 共享变量，使用volatile修饰保证线程可见性
> private volatile int state;
> ~~~
>
> 

2.通过内置的 **FIFO 线程等待/等待队列** 来完成获取资源线程的排队工作。



ReentrantLock为例看AQS实现：

`ReentrantLock` 的内部维护了一个 `state` 变量，用来表示锁的占用状态。

`state` 的初始值为 0，表示锁处于未锁定状态。

当线程 A 调用 `lock()` 方法时，会尝试通过 `tryAcquire()` 方法独占该锁，并让 `state` 的值加 1。

如果成功了，那么线程 A 就获取到了锁。

如果失败了，那么线程 A 就会被加入到一个等待队列（CLH 队列）中，直到其他线程释放该锁。

假设线程 A 获取锁成功了，释放锁之前，A 线程自己是可以重复获取此锁的（`state` 会累加）。这就是可重入性的体现：一个线程可以多次获取同一个锁而不会被阻塞。

但是，这也意味着，一个线程必须释放与获取的次数相同的锁，才能让 `state` 的值回到 0，也就是让锁恢复到未锁定状态。只有这样，其他等待的线程才能有机会获取该锁。



下图为AQS独占模式 获取锁举例；关键在于判断state的值

![AQS 独占模式获取锁](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202308022322928.png)



### AQS资源共享方式

两种  1独占exclusive  2排他share



### 自定义同步器