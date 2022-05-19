# Redis

redis是一款高效的NoSQL型的非关系型数据库,使用c语言开发的一款高效的键值对数据库

- 键(key):一定是字符串类型
- 值(value):支持的数据有
  - 字符串
  - 哈希类型
  - 列表
  - 集合
  - 有序列表

## Nosql概述

### 什么是NoSql

NoSQL -> Not Only SQL(不仅仅是SQL)

泛指非关系型数据库，在web2.0互联网的时代，传统的关系型数据库很难应对大规模的高并发的社区，NoSQL在当今大数据环境下发展迅猛，Redis是其中发展最快的

### NoSQL特点

1. 方便扩展（数据之间没有关系，很好扩展！）

2. 大数据量，高性能（NoSQL的缓存记录级，是一种细粒度的缓存，性能比较高）

3. 数据类型是多样的（不需要事先设计数据库）

4. 传统RDBMS和NoSQL

   ```
   传统的RDBMS
   - 结构化组织
   - SQL
   - 数据和关系都存在单独的表中
   - 操作，数据定义语言
   - 基础的事务
   ```

   ```
   NoSQL
   - 不仅仅是数据
   - 没有固定的查询语言
   - 键值对存储，列存储，文档存储，图形数据库（社交关系）
   - 最终一致性
   - CAP定理和BASE
   - 高性能，高可用，高扩展性
   ```

### NoSQL的缺点

1. 维护的工具和资料有限
2. 不提供对sql 的支持
3. 不提供事务的处理

### NoSQL的四大分类

##### KV键值对：

- 新浪：Redis
- 美团：Redis+Tair
- 阿里、百度：Redis+memecache

##### 文档型数据库（bson格式，和json语言）：

- MongoDB
  - MongoDB是一个基于分布式文件存储的数据库，C++编写，主要用于处理大量文档
  - MongoDB是一个介于关系型数据库和非关系型数据中中间的产品。**MongoDB是非关系型数据库中功能最丰富，最像关系型数据库的**
- ConthDB

##### 列存储数据库

- HBase
- 分布式文件系统

##### 图关系数据库

- Neo4J
- InfoGrid

##### 图示

![QQ截图20210521160829](\assets\QQ截图20210521160829.png)





## Redis入门

> Redis是什么?

Redis（Remote Dictionary Server )，即远程字典服务

一个开源的使用ANSI [C语言](https://baike.baidu.com/item/C语言)编写、支持网络、可基于内存亦可持久化的日志型、Key-Value[数据库](https://baike.baidu.com/item/数据库/103728)，并提供多种语言的API

免费和开源，是现在最热门的NoSQL技术之一，也被称为结构化数据库

> Redis能干嘛?

1. 内存存储,持久化(rdb,aof)
2. 效率高,可以用于高速缓存
3. 发布订阅系统
4. 地图信息分析
5. 计时器,计数器(游览量!)

> 特性

1. 多样的数据类型
2. 持久化
3. 集群
4. 事务

> Redis是单线程的

官方表示：Redis是基于内存操作，CPU不是Redis性能瓶颈，Redis的瓶颈是根据机器的内容和网络带宽，既然可以使用单线程来实现，就使用单线程！（ps：Redis6版本之后支持多线程，但默认还是单线程的）

## Window使用Redis

1. 在github中下载redis:https://github.com/redis/redis
2. 解压
3. 获得以下文件![QQ截图20210521093025](\assets\QQ截图20210521093025.png)
4. 首先启动服务,后启动客户端即可使用
5. ![QQ截图20210521093209](\assets\QQ截图20210521093209.png)



## Linux使用Redis

1. 官网下载并获得安装包

2. 将安装包上传至Linux

3. 解压![image-20210526102907031](\assets\image-20210526102907031.png)

   完成之后获得redis文件

   ![image-20210526102950958](\assets\image-20210526102950958.png)

4. 进入解压后的文件,可以看到redis的配置文件

5. 安装基本的环境

   ```bash
   yum install gcc-c++
   
   make
   
   make install
   ```

   ![image-20210526103516670](\assets\image-20210526103516670.png)

6. redis的默认安装路径`usr/local/bin`

   ![image-20210526103846042](\assets\image-20210526103846042.png)

7. 将redis配置文件,复制到当前目录下

   ![image-20210526104228293](\assets\image-20210526104228293.png)

8. redis默认不是后台启动的,需要修改配置文件

   ![image-20210526104446905](\assets\image-20210526104446905.png)将daemonize属性从no改为yes

9. 启动redis服务

   在redis目录下,通过指定的配置文件启动redis

   ```bash
   运行： redis-server redisconfig/redis.conf
   ```

   然后使用redis客户端进行连接

   ![image-20210526105012829](\assets\image-20210526105012829.png)

10. 查看redis的进程是否开启

    ![image-20210526105230678](\assets\image-20210526105230678.png)

11. 关闭redis服务

    shutdown关闭redis

    ![image-20210526105350509](\assets\image-20210526105350509.png)




## 性能测试

redis-benchmark是redis自带的一个压力测试工具

redis-benchmark命令参数：

![image-20210531132055518](\assets\image-20210531132055518.png)

简单测试命令

```bash
# 测试：100个并发  100000次请求
[root@localhost bin]# redis-benchmark -h localhost -p 6379 -c 100 -n 100000
```







## Redis命令

可以前往Redis中文官网查看具体命令：[Redis命令中心](http://www.redis.cn/commands.html)

### Redis-Key

1. 添加数据：**set key value [ex | px] [nx | xx]**
   1. key：键，必须是string类型
   2. value：数据的值，可以有5个数据类型
   3. ex：key的生命周期，单位秒/s
   4. px：key的生命周期，单位毫秒/ms
   5. nx：key不存在时添加数据
   6. xx：key存在时添加数据（修改数据）
   7. 当设置了声明周期后，时限一到，数据删除。没有设置声明周期即可永久存在
2. 获取数据：**get key**
   1. key存在则返回对应的数据，不存在则返回nil
3. 判断key是否存在：**exists key [key .....]**
   1. 返回存在的key的个数，key不存在返回0
4. 获取key的名称：**keys pattern**
   1. pattern：模型
      1. *：任意字符	—>  keys * 就是查看所有的key
      2. ？：单个字符
      3. []：区间中的单个字符
      4. [^]：不在区间中的单个字符
5. 删除
   1. **flushdb**：删除当前数据库中的所有的key
   2. **flushall**：删除所有数据库中的所有key
6. 切换数据库：**select index**
   1. redis共16个数据库
   2. index：数据库的下标，从0开始
7. key重命名：**rename key newkey**
   1. key：原始名称
   2. newkey：新名称
8. 设置key的生命周期：**expire key timeout**
   1. timeout：生命周期的时间，单位秒/s
   2. 执行成功返回1，失败返回0
9. 查看key的生命周期：**ttl key**
   1. 返回指定key剩余的生命周期数，单位秒/s
   2. 返回-1表示这个key永久有效，没有生命周期
   3. key不存在返回-2
10. 取消生命周期：**persist key**
  1. 当key取消生命周期后，key永久有效



### 基本数据(String)

> 数据类型操作

​	redis中的数据类型指代的是value中的数据类型

​	一个存储空间只能存储一个数据

1. 字符串（string）

   - 添加多个数据: **mset key value [key value key value........]**

     同时添加多个键值对数据

   - 获取多个数据：**mget key [key.....]**
     key不存在返回nil

   - 获取value字符串长度：**strlen key**
     返回key对应的value字符串长度，key不存在返回0

   - 追加字符：**append key value**
     给指定的key追加value数据，返回追加后的字符串长度，key不存在则创建新的key

   - 字符串增量：**incr key**
     让key对应的value自增1，要求key对应的value的值必须是整数

   - 手动增量字符串：**incrby key value**
     手动给value值增量，value值必须是整数，为负表示减少

   - 字符串减量：**decr key**
     让key对应的value自减1，要求key对应的value的值必须是整数

   - 手动减量字符串
     手动给value值减量，value值必须是整数，为负表示增加
     
   - 截取字符串：getrange key 截取位置  截取长度

     ```bash
     127.0.0.1:6379> set key "hello world"
     OK
     127.0.0.1:6379> get key
     "hello world"
     127.0.0.1:6379> getrange key 0 4	
     # 0为截取的起始位置下标4为停止截取位置的下标
     "hello"
     127.0.0.1:6379> getrange key 0 -1
     # 获取全部的字符串,和get key是一样的
     "hello world"
     
     ```

   - 替换字符串：setrange key 替换起始位置  插入内容

     ```bash
     127.0.0.1:6379> set key1 "ABCDEFG"
     OK
     127.0.0.1:6379> get key1
     "ABCDEFG"
     127.0.0.1:6379> setrange key1 2 xx
     # 2是插入的位置,表示从第二个字符串开始替换
     # xx是插入的内容
     (integer) 7
     127.0.0.1:6379> get key1
     "ABxxEFG"
     ```
     
   - setex  (set with expire)  设置过期时间
   
   - setnx (set if not expire) 不存在的设置
   
     ```bash
     # c
     127.0.0.1:6379> setex key3 30 "hello"	
     # 设置key3的值为hello,30秒后过期
     OK
     127.0.0.1:6379> ttl key3
     (integer) 27
     127.0.0.1:6379> setnx key4 "redis"
     # 如果key4不存在,则创建key4返回1
     (integer) 1
     127.0.0.1:6379> keys *
     4) "key1"
     5) "key"
     8) "key4"
     127.0.0.1:6379> setnx key4 "Java"
     # 如果key4不存在,则创建失败返回0
     (integer) 0
     127.0.0.1:6379> get key4
     "redis"
     
     ```
   
     
   
   


### 哈希数据(Hash)

将数据进行分支,方便管理,一个存储空间可以存储多个键值对数据

主要用于存储对象信息

格式:

​	key -> value

value-> 存储的哈希数据

field -> value

field ->存储的字段名

value -> 自动对应的数据

实例:

​	users(key) -> user(value)

​		user(哈希数据)

​			name-> 张三

​			age ->20

​			sex -> man



>  添加数据

- ​	语法：hset key field value
  - 一次添加一个字段
- hmset key field value [field value field value.....]
  - 一次添加多个字段
  - 4.0版本后已经被弃用,正常使用hset即可

> 获取数据

- hget key field
  - 获取一个字段的值
- hmget key field [key field....]
  - 获取多个字段的值

> 判断字段是否存在

- hexists key field
  - 当字段存在,返回1,不存在则返回0

> 获取所有的字段

- hgetall key
  - 返回所有的字段和值

> 获取所有字段的个数

- hlen key
  - 返回字段的个数

> 获取所有的字段

- hkeys key
  - 获取对象中的所有key

> 获取所有字段的value值

- hvals key
  - 获取对象中的所有值

> 删除某个字段

- hdel key
  - 删除某个键值对



### 列表数据(list)

可以存储有序的多个数据，按照数据的下标进行排序。它们的空间是连续的。

底层采用双向链表结构，value的数据类型为String

> 添加数据

- lpush key value [value.....]
  - 从列表的头部添加数据
- rpush key value [value.....]
  - 从列表的尾部添加数据
  - 运行成功后返回列表中的数据个数

> 获取数据

- lindex key index
  - 通过下标获取数据,下标从0开始
- lrange key start stop
  - 获取指定范围内的数据，start表示开始的下标，stop表示结束的下标（包括）

> 获取列表的长度

- llen key

> 删除数据

- lpop key
  - 删除头部的第一个数据
- rpop key
  - 删除尾部的第一个数据
  - 返回被删除的数据
- lrem key num value
  - 删除列表指定的元素
  - num：为删除个数（如果小于0 从右往左删除，如果等于0，全部删除）
  - value：要删除的值
  - 删除指定个数的元素
  - 返回被删除数据的个数

> 对集合进行截取

- ltrim key  起始位置  截取长度

  - ```bash
    127.0.0.1:6379> Lpush mylist "hello1" "hello2" "hello3" "hello4"
    (integer) 4
    127.0.0.1:6379> lrange mylist 0 -1
    1) "hello4"
    2) "hello3"
    3) "hello2"
    4) "hello1"
    127.0.0.1:6379> ltrim mylist 1 2
    # 从下标1开始,截取两个数据。截取后改变list
    OK
    127.0.0.1:6379> lrange mylist 0 -1
    1) "hello3"
    2) "hello2"
    
    ```

> 替换数据

- lset  将列表中指定下标的值替换为另一个值,更新操作

  - ```bash
    127.0.0.1:6379> lrange mylist 0 -1
    1) "hello3"
    2) "hello2"
    # 如果不存在列表或是下标不存在去更新就会报错,
    127.0.0.1:6379> lset mylist 0 hello1
    # 将mylist列表下标为0的值更新为hello1
    OK
    127.0.0.1:6379> lrange mylist 0 -1
    1) "hello1"
    2) "hello2"
    127.0.0.1:6379> 
    
    ```

> 插入值

- linsert key before| after  被插入的值  插入的值

  - ```bash
    127.0.0.1:6379> lrange mylist 0 -1
    1) "hello1"
    2) "hello2"
    127.0.0.1:6379> linsert mylist before hello1 hello
    # 往hello1这个值之前插入hello
    # before往前插入
    # after往后插入
    (integer) 3
    127.0.0.1:6379> lrange mylist 0 -1
    1) "hello"
    2) "hello1"
    3) "hello2"
    ```

  - 

### 集合（set）

存储的结构和hash完全相同，不能有相同的键。它只存储键，不存储value值且不能有相同的数据。一个无序不重复的集合

> 存储数据

- sadd key member [member..]
  - member就是存储的键

>获取数据

- smember key
  - 显示集合中的所有数据
- scard key
  - 获取集合中元素的数量

> 删除数据

- srem key value
  - 删除集合中指定的数据
  - value：指定的数据

> 判断数据是否存在

- sismember key value
  - 判断元素是否在集合中，如果存在 返回 1，否则返回0
  - value：要判断的数据

> 随机筛选集合内一个元素

- srandmember key 

  - ```bash
    127.0.0.1:6379> sadd myset hello hello1 hello2 hello3
    (integer) 4
    127.0.0.1:6379> srandmember myset
    "hello1"
    127.0.0.1:6379> srandmember myset
    "hello3"
    127.0.0.1:6379> srandmember myset
    "hello"
    127.0.0.1:6379> srandmember myset
    "hello1"
    127.0.0.1:6379> srandmember myset 2
    # 一次抽选出两个元素
    1) "hello"
    2) "hello2"
    ```

  - 

### 有序集合（Zset）

存储的数据类型为String，不允许有重复数据。不同的数据都管理一个double分数

double分数：主要进行数据的排序，默认升序排序

> 添加数据

- ZADD  key score memebr[score number ......] 
  - 向有序集合加入一个元素和该元素的分数，如果该元素已经存在的话，则是更新该元素的分数，返回新加入到集合的元素个数。其中分数不仅可以是整数还可以是浮点数。
  - score：关联的排序字段（double分数）
  - member：要存储的数据

> 获取数据

-  ZRANGE key start  stop [WITHSCORES] 
  - 以升序方式获取数据
  - start：开始的下标，从0开始
  - stop：结束的下标
  - WITHSCORES：是否显示排序字段
- ZREVRANGE key start  stop [WITHSCORES] 
  - 以降序方式获取数据
- ZCARD key
  - 获得集合中元素的数量
- ZCOUNT key min_score max_score
  - 获得指定分数范围内的元素个数

> 删除数据

- ZREM key member [member .....]
  - 删除一个或是多个元素，返回的是被删除元素的个数
- ZREMRANGEBYRANK key start stop
  - 删除指定排名的元素

### geospatial 地理位置

Redis的Geo在Redis3.2版本就推出了。这个功能可以推算地理位置的信息，两地之间的距离，附近的人

> geoadd 添加地理位置 

```bash
# geoadd key 经度 维度 城市名
# 地球两极无法添加,一般使用会去下载城市数据,通过java一次性导入

127.0.0.1:6379> geoadd china:city 116.40 39.90 beijing
(integer) 1
127.0.0.1:6379> geoadd china:city 121.47 31.23 shanghai
(integer) 1
127.0.0.1:6379> geoadd china:city 106.50 29.53 chongqin
(integer) 1
127.0.0.1:6379> geoadd china:city 114.05 22.52 shengzen
(integer) 1
```

> geopos 获取经纬度

```bash
127.0.0.1:6379> geopos china:city beijing
# geopos key 城市名
1) 1) "116.39999896287918091"
   2) "39.90000009167092543"
```

> geodist 获取两地之间的距离

```bash
# geodist key 城市名 城市名
127.0.0.1:6379> geodist china:city beijing chongqin
# 查看beijing到chongqin的直线距离
"1464070.8051"
127.0.0.1:6379> geodist china:city beijing chongqin km
# 最后添加距离单位可以将距离自动转换
"1464.0708"

```

> georadius 以给定的经纬度为中心,找出某一半径内的元素

```bash
127.0.0.1:6379> georadius china:city 110 30 1000 km
# 以110 30的经纬度为中心,查询半径1000km内的内容
1) "chongqin"
2) "shengzen"

```



### hyperloglog

Redis 在 2.8.9 版本添加了 HyperLogLog 结构。

Redis HyperLogLog 是用来做基数统计的算法，HyperLogLog 的优点是，在输入元素的数量或者体积非常非常大时，计算基数所需的空间总是固定 的、并且是很小的。

在 Redis 里面，每个 HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基 数。这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比。

但是，因为 HyperLogLog 只会根据输入元素来计算基数，而不会储存输入元素本身，所以 HyperLogLog 不能像集合那样，返回输入的各个元素。

#### 什么是基数?

比如数据集 {1, 3, 5, 7, 5, 7, 8}， 那么这个数据集的基数集为 {1, 3, 5 ,7, 8}, 基数(不重复元素)为5。 基数估计就是在误差可接受的范围内，快速计算基数。

-----------------------------------------------分割线--------------------------------------------------

hyperloglog一般可以用于统计页面访问量，（例如每个用户访问网站计算一次访问量，但是同一个用户多次访问网站我们也只视为一次访问量）

但是redis官方表示hyperloglog有大约0.81%错误率，所以在信息精准度要求高的程序中不推荐使用

> 测试使用

```bash
127.0.0.1:6379> PFadd mykey a b c d e f j h i j k
# 创建第一组元素
(integer) 1
127.0.0.1:6379> pfcount mykey
# 统计mykey中的基数数量
(integer) 10
127.0.0.1:6379> pfadd mykey2 a b c d e 1 2 3 4 5 
# 创建第二组元素
(integer) 1
127.0.0.1:6379> pfcount mykey2
(integer) 10
127.0.0.1:6379> pfmerge mykey3 mykey mykey2
# 合并第一组与第二组元素,并生成新的第三组元素
OK
127.0.0.1:6379> pfcount mykey3
# 统计第三种元素中的基数数量
(integer) 15

```

**如果是允许容错的信息，就可以使用hyperloglog！**

### Bitmap

> 位存储

统计用户信息、活跃，不活跃、是否登录、打卡等只有两种状态的都可以使用bitmaps。

bitmaps位图，都是操作二进制位来进行记录，就只有0和1两个状态！

365天的状态 = 365bit	1字节=8bit	365天的状态=46个字节左右



> 测试

```bash
127.0.0.1:6379> setbit sign 0 1 
(integer) 0
127.0.0.1:6379> setbit sign 1 1 
(integer) 0
127.0.0.1:6379> setbit sign 2 1 
(integer) 0
127.0.0.1:6379> setbit sign 3 1 
(integer) 0
127.0.0.1:6379> setbit sign 4 1 
(integer) 0
127.0.0.1:6379> setbit sign 5 1 
(integer) 0
127.0.0.1:6379> setbit sign 6 0 
(integer) 0
# 第一个参数视为天数,第二个参数视为打卡情况(1为打卡)
127.0.0.1:6379> getbit sign 3
# 查看星期四的记录
(integer) 1
127.0.0.1:6379> getbit sign 6
# 查看星期天的记录
(integer) 0
127.0.0.1:6379> bitcount sign
# 查看总打卡次数
(integer) 6


```

使用bitmap来统计周一至周日的打卡记录

从0开始视为周一,直到6



## 事务

Redis事务本质：一组命令的集合，一个事务中的所有命令都会被序列化，在事务执行的过程中，会按照顺序执行！

一次性、顺序性、排它性、

```bash
------- 队列 set set set 执行---

```

**Redis事务没有隔离级别的概念**

所有的命令在事务中，不会被直接执行，只有发起执行命令的时候才会一次性按顺序执行

**Redis单条命令是保证原子性的，但是事务不保证原子性**

redis的事务：

1. 开启事务（multi）
2. 命令入队（....）
3. 执行事务（exec）

> 正常执行事务

```bash
127.0.0.1:6379> multi
# 开启事务
OK
# 命令入队
127.0.0.1:6379(TX)> set k1 v1
QUEUED
127.0.0.1:6379(TX)> set k2 v2
QUEUED
127.0.0.1:6379(TX)> set k3 v3
QUEUED
127.0.0.1:6379(TX)> get k2
QUEUED
# 执行事务
127.0.0.1:6379(TX)> exec
1) OK
2) OK
3) OK
4) "v2"


127.0.0.1:6379(TX)> discard
# 放弃事务,事务队列中命令不会被执行
```

redis事务中出现bug有以下两种情况

- > 编译型异常(命令有错),事务中的所有命令都不会被执行

- > 运行时异常，如果事务队列中存在语法性错误，那么执行命令的时候，其它命令是可以正常执行的。错误的命令会抛出异常

### 悲观锁

- 很悲观，认为什么时候都会出现问题，无论什么操作都会加锁

### 乐观锁

- 很乐观，认为什么时候都不会出现问题，所以不会上锁！更新数据的时候去判断一下，在此期间是否有人修改过这个数据
- 获取version
- 更新的时候比较version

> Redis监视测试

正常执行

```bash
127.0.0.1:6379> set money 200
OK
127.0.0.1:6379> set out 0
OK
127.0.0.1:6379> watch money  # 监视money对象
OK
127.0.0.1:6379> multi	
OK
127.0.0.1:6379(TX)> decrby money 30
QUEUED
127.0.0.1:6379(TX)> incrby out 30
QUEUED
127.0.0.1:6379(TX)> exec # 事务正常结束,数据期间没有发生异常,这个时候就正常执行成功
1) (integer) 170
2) (integer) 30
```



测试多线程修改值，使用watch可以当作redis的乐观锁操作

```bash
127.0.0.1:6379> watch money  # 监视money
OK
127.0.0.1:6379> multi
OK
127.0.0.1:6379(TX)> decrby money 10
QUEUED
127.0.0.1:6379(TX)> incrby out 10
QUEUED
127.0.0.1:6379(TX)> exec  # 在执行之前,另外一个线程修改了money的值,这个时候就会导致事务执行失败
(nil)

```

```bash
127.0.0.1:6379> unwatch		# 如果事务执行失败,就先解锁
OK
127.0.0.1:6379> watch money	# 获取最新的值,再去监视
OK
127.0.0.1:6379> multi
OK
127.0.0.1:6379(TX)> decrby money 10
QUEUED
127.0.0.1:6379(TX)> incrby money 10
QUEUED
127.0.0.1:6379(TX)> exec	# 比对监视的值是否发生了变化,如果没有变化即执行成功,如果变化了即执行失败
1) (integer) 90
2) (integer) 100

```

如果修改失败,获取最新的值再执行即可



## Jedis

### Java使用Jedis

我们需要Java来操作Redis

> jedis是什么

jedis是Redis官方推荐的java连接开发工具，使用java操作Redis中间件

> 使用

1. 导入对应的依赖

   ```xml
       <dependency>
         <groupId>redis.clients</groupId>
         <artifactId>jedis</artifactId>
         <version>3.6.0</version>
       </dependency>
   <!--json-->
       <dependency>
         <groupId>com.alibaba</groupId>
         <artifactId>fastjson</artifactId>
         <version>1.2.75</version>
       </dependency>
   ```

2. 连接Redis

   ```java
    public static void main(String[] args) {
           //1.创建Jedis对象 -> 连接指定位置上的Redis
           Jedis jedis = new  Jedis("localhost",6379);
           try {
               System.out.println(jedis);
               //查看服务是否运行
               System.out.println("服务正在运行: "+jedis.ping());
               Set<String> keys = jedis.keys("*");
               System.out.println(keys.toString());
               System.out.println("获取所有的key");
               System.out.println("分割线----------------------------------------------");
   
               //关机redis连接
               jedis.close();
   
           }catch (Exception ex){
               System.out.println(ex);
           }
   
       }
   ```

> Jedis所有的方法就是redis的所有命令，名字，效果一模一样



> java中使用jedis执行事务

```java
public static void main(String[] args) {
        Jedis jedis = new Jedis("localhost", 6379);

        Transaction multi = jedis.multi();  //开启事务
    	//jedis.watch("user1");       //监控数据
        try {
            multi.set("user1","zhangsan");
            multi.set("user2","lisi");
            multi.exec();   //成功即执行事务
        } catch (Exception e) {
            multi.discard();     //失败就放弃事务
            e.printStackTrace();
        } finally {
            System.out.println(jedis.get("user1"));
            System.out.println(jedis.get("user2"));
            jedis.close();  //关闭jedis连接
        }
        
    }
```



### springboot整合jedis

ps：在SpringBoot2.x之后，原来使用的jedis被替换为了lettuce

jedis：采用的直连，多个线程操作的话，是不安全的。想要避免不安全，使用jedis pool连接池

lettuce：采用netty，实例可以在多个线程中进行共享，不存在线程不安全的情况

> 整合流程

1. 导入依赖

   ```xml
   <!--导入redis依赖-->
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-data-redis</artifactId>
   </dependency>
   ```

2. 配置连接

   ```properties
   # 这里采用yml语法配置
   spring:
     redis:
       host: localhost
       port: 6379
   ```

   

3. 测试

   ```java
       @Autowired
       private RedisTemplate redisTemplate;
   
       @Test
       void redisTest(){
   
           //opsForValue 操作字符串,类似String
           redisTemplate.opsForValue().set("user1","zhangsan");
           //opsForList 操作list类型
           redisTemplate.opsForList();
   
           //除了基本的操作,一般常用的方法都可以使用redisTemplate操作,比如事务,和基本的crud操作
           redisTemplate.multi();
   
           //一些数据库的操作都通过连接来进行操作
           //获取redis的连接对象
           //RedisConnection connection = redisTemplate.getConnectionFactory().getConnection();
           //connection.flushDb();
       }
   ```



## Redis持久化

Redis是内存数据库，如果不将内存中的数据库状态保存到磁盘，那么一旦服务器进程退出，服务器中的数据也会消失。所以Redis提供了持久化功能

### RDB（Redis DataBase）

> 什么是RDB



在指定的时间间隔内将内存中的数据集体快照写入磁盘，也就是行话讲的Snapshot快照，它恢复时是将快照文件直接读到内存中

Redis会单独创建（fork）一个子进程来进行持久化，会先将数据写入到一个临时文件中，待持久化过程都结束了，再用这个临时文件替换上次持久化好的文件。整个过程中，主进程是不进行任何IO操作的，这就确保了极高的性能，如果需要进行大规模数据的恢复，且对于数据恢复的完整性不是非常敏感，那RDB方式要比AOF方式更加的高效。RDB的缺点是最后一次持久化后的数据可能丢失。

默认使用的都是RDB，一般情况下不需要修改配置

==rdb保存的文件是dump.rdb==



> 触发机制

1. save的规则满足的情况下，会自动触发rdb规则
2. 执行flushall命令，也会触发rdb规则
3. 退出redis，也会产生rdb文件

备份就会自动生成一个dump.rdb文件



> 如何恢复rdb文件

1. 只需要将rdb文件放在redis启动目录就可以，redis启动的时候会自动检查dump.rdb恢复其中的数据
2. 查看需要存在的位置

```bash
127.0.0.1:6379> config get dir
1) "dir"
2) "/usr/local/bin" #在这个目录下存在dump.rdb文件,启动时就会自动恢复其中数据
```



优点:

1. 适合大规模的数据恢复
2. 对数据的完整性要求不高

缺点:

1. 需要一定的时间间隔进程操作，如果redis意外宕机了，就没办法保存最后修改的数据
2. fork进程的时候，会占用一定的内存空间

### AOF（Append Only File）

将我们所有的命令都记录下来，恢复的时候就把这个记录全部再执行一遍

> AOF是什么

以日志的形式来记录每个写操作，将Redis执行过的所有指令记录下来（读取操作不记录），只许追加文件但不可以改写文件，Redis启动之初会读取该文件重新构建数据，换言之：**Redis重启后就根据日志文件将指令从头到尾执行一遍以完成数据的恢复工作**

因此,在数据量十分庞大的时候，AOF执行速度缓慢

Aof保存的是 appendonly.aof 文件

默认是不开启的，我们需要手动对redis.conf配置文件中的appendonly 值从no 改为yes即可开启aof。修改完之后重启即可生效

如果aof文件出现错误，这时候redis启动不起来，我们需要修复这个aof文件

redis给我们提供了一个工具`redis-check-aof --fix aof文件名 ` 	(它会直接将错误的数据删除)

> 优点和缺点

优点:

1. 每一次修改都同步，文件完整性性会更加好
2. 每秒同步一次，可能会丢失1秒的数据
3. 从不同步，效率最高

缺点：

1. 相对于数据文件来说，aof远远大于rdb，修复的速度也比rdb慢
2. Aof运行效率也要比rdb慢，所以redis默认的配置都是rdb持久化



### 拓展

1、RDB持久化方式能够在指定的时间间隔内对你的数据进行快照存储。
2、AOF 持久化方式记录每次对服务器写的操作，当服务器重启的时候会重新执行这些命令来恢复原始的数据,，AOF命令以Redis协议追加保存每次写的操作到文件末尾，Redis还能对AOF文件进行后台重写，使得AOF文件的体积不至于过大。
3、只做缓存，如果你只希望你的数据在服务器运行的时候存在，你也可以不使用任何持久化
4、同时开启两种持久化方式
在这种情况下，当redis重启的时候会优先载入AOF文件来恢复原始的数据，因为在通常情况下AOF文件保存的数据集要比RDB文件保存的数据集要完整。
RDB的数据不实时，同时使用两者时服务器重启也只会找AOF文件，那要不要只使用AOF呢？作者建议不要，因为RDB更适合用于备份数据库( AOF在不断变化不好备份)，快速重启，而且不会有AOF可能潜在的Bug，留着作为一个以防万一的手段。
5、性能建议
因为RDB文件只用作后备用途，建议只在Slave上持久化RDB文件，而且只要15分钟备份一 次就够了，只保留 save 900 1 这条规则。
如果Enable AOF，好处是在最恶劣情况下也只会丢失不超过两秒数据，启动脚本较简单只load自己的AOF文件就可以了，代价一是带来了持续的IO，二是AOF rewrite的最后将rewrite过程中产生的新数据写到新文件造成的阻塞几乎是不可避免的。只要硬盘许可，应该尽量减少AOF rewrite的频率，AOF重写的基础大小默认值64M太小了，可以设到5G以上，默认超过原大小100%大小重写可以改到适当的数值。
如果不Enable AOF，仅靠Master-Slave Repllcation实现高可用性也可以，能省掉一大笔IO，也减少了rewrite时带来的系统波动。代价是如果Master/Slave 同时挂掉，会丢失 十几分钟的数据，启动脚本也要比较两个Master/Slave中的RDB文件，载入较新的那个，微博就是这种架构。



## Redis发布订阅

Redis发布订阅（pub/sub)是一种消息通信模式：发送者（pub）发送信息，订阅者(sub)接收信息。微信、微博、关注系统

Redis客户端可以订阅任意数量的频道。

订阅/发布消息图:

第一个：消息发生者，第二个：频道，第三个：消息订阅者

![image-20210602153611474](\assets\image-20210602153611474.png)



下图展示了频道 channel1 ， 以及订阅这个频道的三个客户端 —— client2 、 client5 和 client1 之间的关系：

![img](\assets\pubsub1.png)

当有新消息通过 PUBLISH 命令发送给频道 channel1 时， 这个消息就会被发送给订阅它的三个客户端：

![img](\assets\pubsub2.png)



> 命令

这些命令广泛用于构建即时通信应用，比如网络聊天室和实时广播，实时提醒等。

| 序号 | 命令及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [PSUBSCRIBE pattern [pattern ...\]](https://www.runoob.com/redis/pub-sub-psubscribe.html) 订阅一个或多个符合给定模式的频道。 |
| 2    | [PUBSUB subcommand [argument [argument ...\]]](https://www.runoob.com/redis/pub-sub-pubsub.html) 查看订阅与发布系统状态。 |
| 3    | [PUBLISH channel message](https://www.runoob.com/redis/pub-sub-publish.html) 将信息发送到指定的频道。 |
| 4    | [PUNSUBSCRIBE [pattern [pattern ...\]]](https://www.runoob.com/redis/pub-sub-punsubscribe.html) 退订所有给定模式的频道。 |
| 5    | [SUBSCRIBE channel [channel ...\]](https://www.runoob.com/redis/pub-sub-subscribe.html) 订阅给定的一个或多个频道的信息。 |
| 6    | [UNSUBSCRIBE [channel [channel ...\]]](https://www.runoob.com/redis/pub-sub-unsubscribe.html) 指退订给定的频道。 |

> 测试

订阅端

```bash
127.0.0.1:6379> subscribe maplef 	# 订阅一个频道 maplef
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "maplef"
3) (integer) 1
# 等待读取推送的inx
1) "message"	# 消息
2) "maplef"		#哪个频道的消息
3) "hello,world" #具体的内容
```

发送端

```bash
[root@localhost bin]# redis-cli -p 6379	
127.0.0.1:6379> ping
PONG
127.0.0.1:6379> publish maplef hello,world	
# 发布者发布消息到频道
(integer) 1
```

> 原理

Redis通过 publish、subscribe和psubscribe等命令实现发布和订阅功能

微信：

通过subscribe命令订阅某频道后，redis-server里维护了一个字典，字典的键就是一个个频道。而字段的值则是一个链表，链表中保存了所有订阅这个channel的客户端。subscribe命令的关机，就是将客户端添加到给定channel的订阅链表中。

通过publish命令向订阅者发送消息，redis-server会使用给定的频道作为键，在它所维护的channel字典中查找记录了订阅这个频道的所有客户端的链表，遍历这个链表，将消息发布给所有订阅者。

pub/sub从字面上理解就是发布与订阅，在Redis中，可以设定对某一个key值进消息发布与消息订阅，当一个key值上进行了消息发布后，所有订阅它的客户端都会收到相应的消息。这一功能最明显的用法就是用作实时消息系统，比如普通的即时聊天，群聊等功能

## Redis主从复制

### 概念

主从复制，是指将一台Redis服务器的数据，复制到其它的Redis服务器。前者称为主节点（master/leader),后者称为从节点(slave/follower)；**数据的复制是单项的，只能由主节点到从节点**。Master以写为主，Salve以读为主。

**默认情况下，每台Redis服务器都是主节点**；且一个主节点可以有多个从节点（或没有从节点），但一个从节点只能有一个主节点

主从复制的作用主要包括：

1. 数据冗余：主从复制实现了数据的热备份，是持久化之外的一种数据冗余方式
2. 故障修复：当主节点出现问题时，可以由从节点提供服务，实现快速的故障修复；实际上是一种服务的冗余
3. 负载均衡：在主从复制的基础上，配合读写分离，可以由主节点提供写服务，由冲节点提供读服务（即写Redis数据时应用连接主节点，读Redis数据时应用连接从节点），分担服务器负载；尤其是在写少读多的情况下，通过多个从节点分担读负载，可以大大提高Redis服务器的并发量。
4. 高可用（集群）基石：除了上述作用意外，主从复制还是哨兵和集群能够实施的基础，因此说主从复制是Redis高可用的基础



一般来说，要将Redis运用于工程项目中，只使用一台Redis是万万不能的（可能会宕机），原因如下：

1. 从结构上，单个Redis服务器会发生单点故障，并且一台服务器需要处理所有的请求负载，压力较大；
2. 从容量上，单个Redis服务器内存容量有限，就算一台Redis服务器内存容量为256G，也不能将所有内存用作Redis存储内存，一般来说，单台Redis最大使用内存不应该超过20G

电商网站上的商品，一般都是一次上次，无数次游览。也就是"多读少写"。对于这种场景，就可用使用以下架构

![image-20210602170806706](\assets\image-20210602170806706.png)

**只要在公司中，主从复制就是必须使用的**



### 环境配置

只配置从库，不用配置主库

```bash
127.0.0.1:6379> info replication	# 查看当前库的信息
# Replication
role:master
connected_slaves:0
master_failover_state:no-failover
master_replid:59e37364ecaa73d4149302b0d1db9bb2bcfb2f56
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

```

复制出3个配置文件,然后给每个配置文件修改对应的端口信息

```bash
[root@localhost redisconfig]# ls
redis.conf
[root@localhost redisconfig]# cp redis.conf redis6379.conf
[root@localhost redisconfig]# cp redis.conf redis6380.conf
[root@localhost redisconfig]# cp redis.conf redis6381.conf
[root@localhost redisconfig]# ls
redis6379.conf  redis6380.conf  redis6381.conf  redis.conf
[root@localhost redisconfig]# vim redis6379.conf
[root@localhost redisconfig]# vim redis6380.conf
[root@localhost redisconfig]# vim redis6381.conf
```

将每个复制处理的.conf文件修改成对应的端口配置

```bash
# 主要修改以下4个配置
port 6381
pidfile /var/run/redis_6381.pid
logfile "6381.log"
dbfilename dump6381.rdb
```

修改完毕后，在三个不同的端口上分别启动不同的redis端口服务

![image-20210602172644067](\assets\image-20210602172644067.png)

可用通过命令查看redis的服务

![image-20210602172822333](\assets\image-20210602172822333.png)

### 一主二从

**默认情况下，每台Redis服务器一启动都是主节点**；一般情况下只配置从机就行了 

`slaveof 127.0.0.1 6379`：让当前服务连接到主机

```bash
# 一主(6379)二从(6380,81)
127.0.0.1:6380> slaveof 127.0.0.1 6379
# 让本机下的6379端口的进程为自己的主机
OK
127.0.0.1:6380> info replication
# Replication
role:slave	# 从机
master_host:127.0.0.1	# 主机的信息
master_port:6379
master_link_status:up
master_last_io_seconds_ago:2
master_sync_in_progress:0
slave_repl_offset:42
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:16492e0fc7f8093e2019483419e82f33478ce85a
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:42
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:42


# 在主机中查看
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:1	# 从机的数量与信息
slave0:ip=127.0.0.1,port=6380,state=online,offset=266,lag=0
master_failover_state:no-failover
master_replid:16492e0fc7f8093e2019483419e82f33478ce85a
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:266
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:266

```

真实的主从配置应该在配置文件中配置，这样配置后的端口每次启动都默认为从机

> 细节

**主机可用写，从机不能写只能读。主机中的所有信息和数据，都会自动被从机保存！**

主机断开连接后，从机依旧连接主机，直到主机重新上线，从机依旧可以获取到主机的信息。

> 从节点分担任务

假如现在我们有 79(主) 80(从) 81(从)三个主机

可以将81的主机设置为80这个从机

80被81指定为主机之后，它本质上仍然是79的一个从机，只能读不能写。但81可以通过80获取到79的数据



> 主机宕机后处理

如果主机断开了连接，可以手动使用`slaveof no one`使一个从机变为主机，其它的节点就可以手动连接到这个新的主节点

在设置完成之后，即使原来的主机重新上线，也不会回到原来的情况



### 哨兵模式

自动选举主机的模式

> 概述

主从切换技术的方法是：当主机宕机之后，需要手动把一台从服务器切换为主服务器，这就需要人工干预，不仅费时费力，还会造成一段时间内服务不可用。更多情况下，会去优先考虑哨兵模式。Redis从2.8开始正式提供了Sentinel（哨兵）架构来解决问题

Sentinel能够后台监控主机是否故障，如果故障了根据投票数自动将从库转换为主库

哨兵模式是一种特殊的模式，首先Redis提供了哨兵的命令，哨兵是一个独立的进程，作为进程，它会独立运行。其原理是**哨兵通过发送命令，等待Redis服务器响应，从而监控运行多个Redis实例**

![image-20210603112339228](\assets\image-20210603112339228.png)

这里的哨兵有两个作用

- 通过发送命令，让Redis服务器返回监控其运行状态，包括主服务器和从服务器。
- 当哨兵监测到master宕机，会自动将slave切换成master，然后通过**发布订阅模式**通知其他的从服务器，修改配置文件，让它们切换主机。

然而一个哨兵进程对Redis服务器进行监控，可能会出现问题，为此，我们可以使用多个哨兵进行监控。各个哨兵之间还会进行监控，这样就形成了多哨兵模式。

用文字描述一下**故障切换（failover）**的过程。假设主服务器宕机，哨兵1先检测到这个结果，系统并不会马上进行failover过程，仅仅是哨兵1主观的认为主服务器不可用，这个现象成为**主观下线**。当后面的哨兵也检测到主服务器不可用，并且数量达到一定值时，那么哨兵之间就会进行一次投票，投票的结果由一个哨兵发起，进行failover操作。切换成功后，就会通过发布订阅模式，让各个哨兵把自己监控的从服务器实现切换主机，这个过程称为**客观下线**。这样对于客户端而言，一切都是透明的。



> 测试

1. 在redis配置文件目录下配置哨兵配置文件`sentinel.conf`

   ```bash
   #sentinel monitor 被监控的名称 主机 端口 1
   #数字1,代表主机挂了之后最少有几个哨兵认为主服务器下线,主服务器会被认定为客观下线
   sentinel monitor myredis 127.0.0.1 6379 1
   ```

   

2. 启动哨兵

   ```bash
   [root@localhost bin]# redis-sentinel redisconfig/sentinel.conf
   9965:X 02 Jun 2021 23:42:03.296 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
   9965:X 02 Jun 2021 23:42:03.296 # Redis version=6.2.3, bits=64, commit=00000000, modified=0, pid=9965, just started
   9965:X 02 Jun 2021 23:42:03.296 # Configuration loaded
   9965:X 02 Jun 2021 23:42:03.297 * Increased maximum number of open files to 10032 (it was originally set to 1024).
   9965:X 02 Jun 2021 23:42:03.297 * monotonic clock: POSIX clock_gettime
                   _._                                                  
              _.-``__ ''-._                                             
         _.-``    `.  `_.  ''-._           Redis 6.2.3 (00000000/0) 64 bit
     .-`` .-```.  ```\/    _.,_ ''-._                                  
    (    '      ,       .-`  | `,    )     Running in sentinel mode
    |`-._`-...-` __...-.``-._|'` _.-'|     Port: 26379
    |    `-._   `._    /     _.-'    |     PID: 9965
     `-._    `-._  `-./  _.-'    _.-'                                   
    |`-._`-._    `-.__.-'    _.-'_.-'|                                  
    |    `-._`-._        _.-'_.-'    |           https://redis.io       
     `-._    `-._`-.__.-'_.-'    _.-'                                   
    |`-._`-._    `-.__.-'    _.-'_.-'|                                  
    |    `-._`-._        _.-'_.-'    |                                  
     `-._    `-._`-.__.-'_.-'    _.-'                                   
         `-._    `-.__.-'    _.-'                                       
             `-._        _.-'                                           
                 `-.__.-'                                               
   
   9965:X 02 Jun 2021 23:42:03.297 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
   9965:X 02 Jun 2021 23:42:03.300 # Sentinel ID is 04b320489f4f81245ab209c7e1d14249c12a7924
   9965:X 02 Jun 2021 23:42:03.300 # +monitor master myredis 127.0.0.1 6379 quorum 1
   9965:X 02 Jun 2021 23:42:03.301 * +slave slave 127.0.0.1:6381 127.0.0.1 6381 @ myredis 127.0.0.1 6379
   9965:X 02 Jun 2021 23:42:03.303 * +slave slave 127.0.0.1:6380 127.0.0.1 6380 @ myredis 127.0.0.1 6379
   
   ```

   如果Master节点断开了，这个时候就会从从机中随机选择一个服务器

   ![image-20210603114839846](\assets\image-20210603114839846.png)

3. 主机在宕机后重新上线，哨兵模式会自动将其归并到新的主机下，当作从机

   > 优缺点

   优点:

   - 哨兵集群,基于主从复制模式，所有的主从配置优点，它都有
   - 主从可以切换，故障可以转移，系统的可用性就会更好
   - 哨兵模式就算主从模式的升级，从手动到自动，更加健壮

   缺点：

   - Redis不好在线扩容，集群容量一旦到达上限，在线扩容就十分麻烦
   - 实现哨兵模式的配置十分麻烦



## Redis缓存穿透和雪崩

### 缓存穿透

> 概念

缓存穿透的概念很简单，用户想要查询一个数据，绕行Redis内存数据库中没有，也就是缓存没有命中，于是向持久层数据库查询。发现也没有，于是本次查询失败。当用户很多的时候，缓存都没有命中，于是都去请求了持久层数据库，会给持久层数据库造成很大压力，这时候就相当于出现了缓存穿透。

> 解决方案

#### 布隆过滤器

布隆过滤器是一种数据结构,对所有可能查询的参数以hash形式存储，在控制层先进行校验，不符合则丢弃，从而避免了对底层存储系统的查询压力

![image-20210603121234695](\assets\image-20210603121234695.png)

##### 缓存空对象

当存储层不命中后，即使返回的空对象也将其缓存起来，同时会设置一个过期时间，之后再访问这个数据将会从缓存中获取，保护后端数据源

![image-20210603121249475](\assets\image-20210603121249475.png)

但是会存在两个问题：

1. 如果空值能够被缓存起来，就意味着缓存需要更多的空间存储更多的键，因此可能导致会有很多空值的键
2. 即使对空值设置了过期时间，还是会存在缓存层和存储层的数据会有一段时间窗口的不一致，这对于需要保持一致性的业务会有影响



### 缓存击穿

> 概述

缓存击穿,指一个key非常热门,在不停的被访问,大并发集中对这一个点进行访问,当这个key在失效的瞬间,持续的大并发就会穿破缓存,直接请求数据库,就像在一面墙上凿开了一个洞

当某个key在过期的瞬间，有大量的请求并发访问，这类数据一般是热点数据，由于缓存过期，会同时访问数据库查询最新数据并回显缓存，会导致数据库瞬间压力过大

> 解决方案

##### 设置热点数据永不过期

从缓存层面来看,没有过期时间,所以不会出现热点key过期后产生的问题

##### 加互斥锁

分布式锁：使用分布式锁，保证对于每个key同时只有一个线程去查询后端服务，其它线程没有获取分布式锁的权限，因此只需要等待即可，这种方式将高并发的压力转移到了分布式锁，因此对分布式锁的考验很大



### 缓存雪崩

缓存雪崩指在某一个时间段，缓存集中过期失效，Redis宕机。

例如，双12，马上迎来一波抢购，这波商品集中放入了缓存，并设置缓存1个小时，那么到了凌晨1点的时候，缓存全部过期，而之后对这批商品的访问查询全部转移到数据库，对于数据库而言，就会产生周期性的压力波峰，于是所有的请求都会达到存储层，存储层的调用量会暴增，导致存储层也崩溃的情况

还有一种情况，指服务器某个节点宕机或者断网，因为自然形成的缓存雪崩，一定是在某个时间段集中创建缓存，这种情况下，无非是对数据库产生周期性的压力而已，而缓存服务节点的宕机，对数据库服务器造成的压力是不可预知的，很有可能瞬间就把数据库压垮

> 解决方案

##### redis高可用

既然redis有可能挂掉,那么就多增几台服务器，即使一台挂掉之后其它的还可用继续工作，其实就算搭建集群

##### 限流降级

在缓存失效后，通过加锁或者队列来控制读数据库写缓存的线程数量，比如对某个key只允许一个线程查询访问，其它线程等待

##### 数据预热

在正式部署前，先把可能访问的数据提前访问一遍，这样大部分的访问数据会提前加载进缓存中，在即将发送大规模并发访问前手动触发加载缓存不同的key，设置不同的过期时间，让缓存失效的时间点尽量均匀



## 小结

- Redis缓存穿透与雪崩只是略做了解，并未深入
- 分布式锁未了解
- 集群未了解，只是简单配置了多个服务
- 

