
####知识点整理

1. JAVA基础
    1. [ArrayList与Linkedlist的优缺点](java/ArrayList与Linkedlist的优缺点.MD)
    1. HashMap
        1. [为什么HashMap中链表长度超过8会转换成红黑树](java/为什么HashMap中链表长度超过8会转换成红黑树.MD)
        1. [为什么链表转换成红黑树选择6和8](java/为什么链表转换成红黑树选择6和8.MD)
        1. [为什么HashMap不使用AVL树而使用红黑树](java/为什么HashMap不使用AVL树而使用红黑树.MD)
        1. [Hashmap扩容机制](./java/Hashmap扩容机制.MD)
    1. ConcurrentHashMap
        1. [ConcurrentHashMap原理分析](./java/ConcurrentHashMap原理分析.MD)
    1. 阻塞队列BlockingQueue相关实现
    1. [字符串求每一个的个数](./java/字符串求每一个的个数.MD)
    1. Bio nio Aio 
1. Concurrent并发
    1. [AtomicInteger源码解析](./concurrent/AtomicInteger源码解析.MD)
    1. ReentrantLock实现，以及其内部同步器Sync的实现原理
    1. Java两个锁的底层实现synchronized和lock的区别
1. 线程池
    1. [线程池的作用](java/线程池优缺点.MD)
    1. 线程的生命周期
    1. 线程池的工作原理，生命周期
    1. Future的实现原理
    1. Java的线程池说一下，各个参数的作用，如何进行的?
    1. 线程池的源码实现
1. JVM
    1. [Jvm内存模型](jvm/JVM内存模型.MD)
    1. [内存溢出与内存泄漏](jvm/内存溢出与内存泄漏.MD)
    1. 类在jvm生命周期
    1. [排查CPU和内存飙升](jvm/jstack.MD)
    1. [如何确认这个类不被使用？](jvm/如何确认这个类不被使用.MD)
1. SpringBoot
   1. SpringBoot启动顺序
1. SpringCloud
   1. [为什么Dubbo比SpringCloud性能要高一些？](springcloud/为什么Dubbo比SpringCloud性能要高一些.MD)
   1. [Springcloud有哪些改进](springcloud/Springcloud有哪些改进.MD)
   1. Hystrix 重连机制
1. Mysql
   1. Mysql事务实现原理
   1. [Mysql几种引擎](mysql/mysql几种存储引擎介绍.MD)
   1. [Mysql几种索引](mysql/mysql几种索引类型.MD)
   1. [Mysql索引BTree、B+Tree详细分解](https://www.jianshu.com/p/d67c637776d6)
   1. [Mysql优化](mysql/Mysql优化.MD)
1. Zookeeper 
   1. [Zookeeper的高可用集群与leader选举策略](zookeeper/Zookeeper的高可用集群与leader选举策略.MD)
1. 缓存
   1. Redis 幂等性 如何处理 底层实现原理
   1. Redis有哪些锁
   1. Redis分布式锁的底层实现
   1. [redis持久化RDB和AOF](cache/redis持久化RDB和AOF.MD)
   1. [Redis缓存淘汰策略](cache/Redis缓存淘汰策略.MD)
   1. [redis 都有哪些数据类型？分别在哪些场景下使用比较合适？](cache/redis-data-types.md)
1. Nginx
   1. Nginx 为什么能撑住这么大的并发量
1. 架构
   1. [Cap base 微服务](microservices/CAP分别代表什么.MD)
   1. 服务拆分规则
   1. [缓存雪崩，缓存穿透解决方案](https://www.cnblogs.com/jinjiangongzuoshi/p/5240280.html)
   1. 200张 优惠券 千万人抢
   1. OAUTH2
   1. 集群环境下定时任务怎么保证执行一次
   1. 两种负载均衡的优缺点
1. 分布式事务
1. 协议
    1. TCP代表什么
    1. Rpc和http的不同
    1. Rpc的标准