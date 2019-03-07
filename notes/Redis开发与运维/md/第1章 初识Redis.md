---
typora-root-url: ../images
---

## 第1章 初识Redis

#### Redis定义

* Redis是一种基于键值对(Key-value)的NoSQL数据库.

#### Redis值

* string 字符串、hash 哈希、list 列表、 set 集合、zset 有序集合、 Bitmaps 位图、HyperLogLog、GEO地理信息定位

#### 除了5中数据结构,提供的其他额外的功能

* 提供了键过期功能,可以用来实现缓存
* 提供了发布订阅功能,可以用来实现消息系统
* 支持Lua脚本功能,可以利用Lua创造出新的Redis命令
* 提供了简单的事务功能,能在一定程度上保证事务特性
* 提供了流水线(Pipeline)功能,这样客户端能将一批命令一次性传到Redis,减少了网络的开销

#### Redis的8个特性

1. 速度快
2. 基于键值对的数据结构服务器
3. 丰富的功能
4. 简单稳定
5. 客户端语言多
6. 持久化(RDB|AOF)
7. 主从复制
8. 高可用和分布式

#### Redis使用场景

1. 缓存
2. 排行榜系统
3. 计数器应用
4. 社交网络
5. 消息队列系统

#### Redis 在linux下的安装命令

```
$ wget http://download.redis.io/releases/redis-3.0.7.tar.gz
$ tar xzf redis-3.0.7.tar.gz
$ ln -s redis-3.0.7 redis
$ cd redis
$ make
$ make install
```

#### 启动Redis的三种方法

* 默认配置启动 `$ redis-server`
* 运行配置启动  `$ redis-server --port 6380`
* 配置文件启动 `$ redis-server /opt/redis/redis.conf`

#### Redis 基础配置项

| 配置名    | 配置说明                                |
| --------- | --------------------------------------- |
| port      | 端口                                    |
| logfile   | 日志文件                                |
| dir       | Redis工作目录(存放持久化文件和日志文件) |
| daemonize | 是否以守护进程方式启动Redis             |

#### Redis命令行客户端

* 交互式方式: `redis-cli -h {host} -p {port}`
* 命令行方式: `redis-cli -h {host} -p {port} {command}` 

* 停止Redis服务

  * `redis-cli shutdown`


#### 停止Redis服务注意事项

1. Redis关闭的过程:断开与客户端的连接,持久化文件生成, 是一种相对优雅的关闭方式
2. 不要粗暴地使用`kill -9` 强制杀死Redis服务,不但不会做持久化操作,还会造成缓冲区等资源不能被优雅关闭,极端状况会造成AOF和复制丢失数据的情况.
3. shutdown还有一个参数,代表是否在关闭Redis前,生成持久化文件  `redis-cli shutdown nosave|save`

