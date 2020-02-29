---
layout: post
author: eature
published: true
categories: 系统编程
tags:
- c
- 进程
- unix
- Linux
---

##### Redis与Memcached的区别 

1. Redis提供更多的数据存储类型，当需要复杂的数据结构的时候， 可以选择Redis
2. Redis提供了数据持久化的功能  
3. Redis支持集群， 提供了Mater-Slave的主从功能

Memcache是纯kv的缓存数据库， 适合高并发的业务
原因有下：  
    1. Memcached使用的预先分配内存持的机制， 能够省去内存分配的时间，且数据不能超过所分配的内存，Redis是临时分配内存， redis当无力内存使用完以后， 会将较久不用的数据交换到磁盘中  
    2. Redis和Memcached都使用了非阻塞的io模型， 但是Redis提供了排序， 聚合等功能， 会延长io时间  
    3. memcached使用多线程模型， 主线程监听， worker线程接受请求，执行数据读写， Redis使用单线程模型， 无法利用处理器多核来提升吞吐量， 但是保证了数据按顺序执行， 提供了事务的功能， 保证一串事务的原子性
   

Memcache和Redis区别：

    Redis中，并不是所有的数据都一直存储在内存中的，这是和Memcache相比一个最大的区别。
    Redis在很多方面具备数据库的特征，或者说就是一个数据库系统，而Memcache只是简单的K/V缓存。
    他们的扩展都需要做集群；实现方式：master-slave、Hash。
    在100k以上的数据中，Memcache性能要高于Redis。
    如果要说内存使用效率，使用简单的key-value存储的话，Memcached的内存利用率更高，而如果Redis采用hash结构来做key-value存储，由于其组合式的压缩，其内存利用率会高于Memcache。当然，这和你的应用场景和数据特性有关。
    如果你对数据持久化和数据同步有所要求，那么推荐你选择Redis，因为这两个特性Memcache都不具备。即使你只是希望在升级或者重启系统后缓存数据不会丢失，选择Redis也是明智的。
    Redis和Memcache在写入性能上面差别不大，读取性能上面尤其是批量读取性能上面Memcache更强
    共同点:Memcache，Redis 都是内存数据库



区别:

 Memcache

    Memcache可以利用多核优势，单实例吞吐量极高，可以达到几十万QPS,适用于最大程度扛量

    只支持简单的key/value数据结构，不像Redis可以支持丰富的数据类型。

    无法进行持久化，数据不能备份，只能用于缓存使用，且重启后数据全部丢失

 

 Redis

    支持多种数据结构，如string,list,dict,set,zset,hyperloglog

    单线程请求，所有命令串行执行，并发情况下不需要考虑数据一致性问题。

    支持持久化操作，可以进行aof及rdb数据持久化到磁盘，从而进行数据备份或数据恢复等操作，较好的防止数据丢失的手段。

    支持通过Replication进行数据复制，通过master-slave机制，可以实时进行数据的同步复制，支持多级复制和增量复制.

    支持pub/sub消息订阅机制，可以用来进行消息订阅与通知。

    支持简单的事务需求，但业界使用场景很少，并不成熟
