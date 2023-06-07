# page

6.7notes

gitbook 3h



6.6notes

* [ ] 动态添加属性文档撰写 3h
* [ ] ~~gitbook135撰写 3h~~
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



<pre><code><strong>ThreadLocal local = new ThreadLocal();// 创建一个线程的本地变量
</strong><strong>local.set();
</strong><strong>local.get();
</strong><strong>
</strong><strong>public class Thread{
</strong>    ThreadLocal.ThreadLocalMap threadLocals = null;
<strong>}
</strong>
<strong>ThreadLocal底层由ThreadLocalMap实现。
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

偏向锁：在锁对象的对象头记录当前锁是哪个线程占用，记录线程ID.下次又来获取该锁可直接获取。

轻量级锁：由偏向锁升级，当一个线程获取该锁，这把锁是偏向锁。另一线程来竞争锁，偏向锁会升级为轻量级锁。轻量级锁通过自旋实现，不会阻塞线程。

重量级锁：如果自旋次数过多仍没有获取到锁，就会升级为重量级锁，重量级锁导致线程阻塞

自旋锁CAS

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

AQS是java的线程同步的框架。

在AQS中，维护了一个信号量state和一个双向链表队列，其中，这个线程队列是用来给

线程排队的，state相当红绿灯，控制线程排队或放行。

在可重入锁场景下，state用来表示加锁的次数，0标识无锁。每加锁state加1，每释放锁，state减1

</details>







## MQ

## 分布式

CAP理论？BASE理论？

什么是RPC?

数据一致性模型有哪些？

分布式ID是什么？有哪些解决方案？

分布式锁的使用场景是什么？有哪些实现方案？

什么是ZAB协议？

为什么Zookeeper可以用来作为注册中心？





















