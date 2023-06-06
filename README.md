# page

6.6notes

* [ ] 动态添加属性文档撰写 3h
* [ ] gitbook135撰写 3h
* [ ] 更新简历 1h

## 线程

<details>

<summary>有哪几种创建线程执行任务？</summary>

```
// 继承Thread类，重写run方法
// 实现Runnable接口，实现run方法
// 实现Callable接口，实现call方法，传入FutureTask类，可以获取线程返回值
// 线程池创建

线程状态：
NEW 
RUNNABLE
BLOCKED
WAITING
TIMED_WAITING
TERMINATED
```

</details>

<details>

<summary>为什么不建议使用工具类Excutors创建线程？</summary>

<pre><code>Executors.newSingleThreadExecutor();
Executors.newFixedThreadPool();
<strong>Executors.newCachedThreadPool();
</strong><strong>参数是写死的,线程无限，队列无限,会造成OOM
</strong><strong>底层都是new ThreadPoolExecutor(int corePoolSize,
</strong>                              int maximumPoolSize,
                              long keepAliveTime,
                              TimeUnit unit,
                              BlockingQueue&#x3C;Runnable> workQueue,
                              ThreadFactory threadFactory,
                              RejectedExecutionHandler handler)构造
</code></pre>

</details>

<details>

<summary>线程池有哪几种状态？</summary>

```
// ThreadPoolExecutor线程池执行类
runState is stored in the high-order bits
private static final int RUNNING 正常运行 ;//既能接受新任务也能处理队列中的任务
private static final int SHUTDOWN  正在关闭状态;//调用shutdown方法
private static final int STOP 正常停止状态;//调用shutdownnow方法
private static final int TIDYING ;//
private static final int TERMINATED;//调用terminated()方法
```

</details>

<details>

<summary>Synchronized和ReentrantLock区别？</summary>

```
synchronized:
关键字，非公平锁，自动加锁与释放锁，锁的是对象，底层有锁升级过程

ReentrantLock：
类，公平锁与非公平锁，手动加锁与释放锁，state标识锁的状态，没有锁升级过程
```

</details>

<details>

<summary>ThreadLocal应用场景？</summary>

线程本地存储机制，将数据缓存在某个线程内部，该线程能在任意时刻任意方法获取缓存的数据。同一个线程内数据传递机制。

经典应用场景是连接管理，一个线程持有一个连接，连接对象可以在不同方法直接进行传递。线程之间不共享同一个连接。

<pre><code><strong>ThreadLocal底层由ThreadLocalMap实现。
</strong><strong>每个Thread对象都存在一个ThreadLocalMap
</strong><strong>Map的key为ThreadLocal对象，value为需要缓存的值
</strong><strong>若线程池中使用ThreadLocal会造成内存泄漏。因为ThreadLocal对象使用完，
</strong><strong>应该把设置的keyvalue回收。但线程池线程不会回收，而线程对象通过强引用指向Map
</strong><strong>map也通过强引用指向entry对象。线程不被回收，entry对象也不会回收，会出现内存泄
</strong><strong>解决办法：使用完threadlocal后手动调用remove方法，手动清除entry对象。
</strong><strong>
</strong></code></pre>

</details>

<details>

<summary>ReentrantLock公平锁和非公平锁底层？</summary>

底层实现使用AQS进行排队

区别在于线程使用lock方法加锁时。

</details>

<details>

<summary>Sychronized的锁升级过程？</summary>

偏向锁

轻量级锁

重量级锁

自旋锁

</details>

<details>

<summary>线程安全的理解？</summary>

一段代码在多个线程同时执行的情况下，是否得到正确的结果。

</details>

<details>

<summary>守护线程的理解？</summary>

用户线程和守护线程

普通线程运行完就会关闭。

守护线程是JVM的后台线程。其他普通线程全部关闭后，守护线程才会关闭。垃圾回收线程也是守护线程。

</details>

<details>

<summary>并发，并行，串行理解？</summary>

串行，一个任务执行完，才能执行下一个任务

并行，两个任务同时执行

并发，

</details>

<details>

<summary>线程池的底层？</summary>

底层是队列和线程实现

</details>

<details>

<summary>线程池为什么先添加队列不是先创建最大线程？</summary>



</details>

<details>

<summary>ReentrantLock中tryLock()和lock()方法的区别？</summary>



</details>

<details>

<summary>CountDownLatch和Semaphore的区别和底层原理？</summary>



</details>

<details>

<summary>对AQS的理解？AQS如何实现可重入锁？</summary>



</details>





Tomcat为什么自定义类加载器？

JDK,JRE,JVM区别？

hashCode和equals的关系？

String,StringBuffer,StringBuilder区别？

泛型中extends和super?

\==和equals区别？

重载和重写区别？



## 集合

List和Set区别？

ArrayList和LinkedList区别？

ConcurrentHashMap底层扩容？

jdk1.7到jdk1.8HashMap区别？

HashMap的put()方法？

深拷贝和浅拷贝？

HashMap扩容机制？

CopyOnWriteArray底层？



## jvm

什么是字节码？

异常体系？什么时候抛出异常？什么时候捕获异常？

有哪些类加载器？

类加载器的双亲委派机制？

JVM中线程共享区？

如何排查JVM问题？

一个对象被加载到JVM,再到被GC清除，经历过程？

确认一个对象是垃圾？

垃圾回收算法？

STW?

常用JVM启动参数有？



## Spring

对IOC的理解？Spring容器启动流程？

单例bean和单例模式？

Spring事务传播机制？

Spring中的bean是线程安全的吗?

Spring中的bean创建的生命周期有哪些步骤?

ApplicationContext和BeanFactory区别？

Spring中的事务是如何实现的？

Spring事务什么时候会生效？

Spring用到哪些设计模式？

SpringBoot中常用注解和底层实现？

SpringBoot如何启动Tomcat?

## Mybatis

死锁如何避免？

mybatis优缺点？

Mybatis中#{}和${}区别？

索引基本原理？

索引设计原则？

事务的基本特性和隔离级别？

什么是MVCC？

InnoDB和MyISAM区别？

Explain语句结果各个字段分表表示什么？

索引覆盖是什么？

最左前缀原则？

InnoDB如何实现事务？

B树和B+树区别？为什么mysql使用B+树？

Mysql锁有哪些？如何理解？

什么是RDB和AOF?

## Redis

redis过期键的删除策略？

简述redis事务实现？

redis主从复制的核心原理？

redis有哪些数据结构？分别有哪些应用场景？

redis分布式锁底层实现？

redis集群策略？

缓存穿透，缓存击穿，缓存雪崩是什么？

redis和mysql如何保存数据一致？

redis持久化机制？

redis单线程为什么这么快？

redis事务的实现？

redis看门狗机制？



负载均衡算法？

雪花算法原理？

SpringCloud有哪些常用组件，作用是什么？

如何避免缓存穿透，缓存击穿，缓存雪崩？

缓存过期有哪些策略？

常见缓存淘汰算法？

布隆过滤器原理，优缺点？

什么是服务雪崩？什么是服务限流？

什么是服务熔断？什么是服务降级？区别？

SOA，分布式，微服务区别？集成？

怎么拆分微服务？



## Nacos

配置中心和注册中心

## Nginx

反向代理和负载均衡



## MQ

epoll和poll区别？

TCP的三次握手和四次挥手？

浏览器发出一个请求到收到响应经历了哪些步骤？

跨域请求是什么？有什么问题？怎么解决？

零拷贝？



## 分布式

CAP理论？BASE理论？

什么是RPC?

数据一致性模型有哪些？

分布式ID是什么？有哪些解决方案？

分布式锁的使用场景是什么？有哪些实现方案？

什么是ZAB协议？

为什么Zookeeper可以用来作为注册中心？





















