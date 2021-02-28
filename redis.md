# redis

## redis安装

**redis官网**：https://redis.io/

- linux安装

  ```linux
  # wget https://download.redis.io/releases/redis-6.0.10.tar.gz
  # tar xzf redis-6.0.10.tar.gz
  # cd redis-6.0.10
  # make
  ```

  make时出现以下情况

  ![image-20210217142641199](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217142641199.png)

  需要安装make,执行以下命令

  ```linux
  yum install -y gcc-c++
  yum -y install gcc automake autoconf libtool make
  ```

- 启动redis服务

  执行完 **make** 命令后，redis-6.0.8 的 **src** 目录下会出现编译后的 redis 服务程序 redis-server，还有用于测试的客户端程序 redis-cli

  ```linux
  # cd src
  //	& 能让redis在后台运行即使ctrl+c后也能运行
  # ./redis-server &
  ```
```
  
注意这种方式启动 redis 使用的是默认配置。也可以通过启动参数告诉 redis 使用指定配置文件使用下面命令启动。
  
  ```linux
  # cd src
  # ./redis-server ../redis.conf
```

**redis.conf** 是一个默认的配置文件。我们可以根据需要使用自己的配置文件。

  启动 redis 服务进程后，就可以使用测试客户端程序 redis-cli 和 redis 服务交互了,在介绍redis数据类型时进行交互枚举。

- 关闭redis服务
  ```redis
  redis-cli -h host -p port -a password shutdown
  ```
- redis远程服务连接

  ```redis
  redis-cli -h host -p port -a password
  ```

  


## redis介绍

redis 是完全开源的，遵守 BSD 协议，是一个高性能的 key-value 数据库。其中value可以为String、hash、list、set、zset等多种数据结构的存储，可以满足很多应用场景。还提供了键过期、发布订阅、事务、流水线等附加功能。

redis 与其他 key - value 缓存产品有以下三个特点：

- Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。

- Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。

- Redis支持数据的备份，即master-slave模式的数据备份。

1. 特点

   - 速度快
   - 键值对的数据结构服务器
   - 丰富的功能
   - 简单稳定
   - 持久化
   - 主从复制
   - 高可用和分布式转移
   - 客户端语言多

2. redis优势

   - 性能极高 – Redis能读的速度是110000次/s,写的速度是81000次/s 。
   - 丰富的数据类型 – Redis支持二进制案例的 Strings, Lists, Hashes, Sets 及 Ordered Sets 数据类型操作。
   - 原子 – Redis的所有操作都是原子性的，意思就是要么成功执行要么失败完全不执行。单个操作是原子性的。多个操作也支持事务，即原子性，通过MULTI和EXEC指令包起来。
   - 丰富的特性 – Redis还支持 publish/subscribe, 通知, key 过期等等特性。

3. redis使用场景

   - 缓存数据库
   - 排行榜
   - 计数器应用
   - 社交网络
   - 消息队列(一般不用)、

4. redis配置

| 可执行文件       |            作用             |
| ---------------- | :-------------------------: |
| redis-server     |          启动redis          |
| redis-cli        |      redis命令行客户端      |
| redis-benchmark  |        基准测试工具         |
| redis-check-aof  | AOF持久化文件检测和修复工具 |
| redis-check-dump | RDB持久化文件检测和修复工具 |
| redis-sentinel   |          启动哨兵           |
| redis-trib       |     cluster集群构建工具     |

4. redis版本
   
   - 版本号第二位为奇数为非稳定版本(2.7、2.9)，为偶数为稳定版本(2.6、2.8)
   
   - 当前奇数版本是下一个稳定版本的开发版本，如2.7是2.8的开发版本
   
## redis数据结构

1. 字符串(string)

   字符串类型：实际上可以是字符串(包括xml、json)、数字(整数、浮点数)、二进制(图片、音频、视频)，最大不能超过512M

   命令
   
   ​	设值：set key value [EX seconds | PX milliseconds | KEEPTTL] [NX | XX]
   
   ​	取值：get key
   
   ​	批量设置：mset [key value ...]
   
   ​	批量取值：mget [key ...]
   
   ```redis
   //设置命令
   set age 25 ex 10 //10秒后过期 ex-秒 px-毫秒
   setnx name gss  //不存在键name时，返回1设置成功；存在的话失败0
set age 24 //存在键age时，返回1成功,实现更新
   
   ```

//获值命令  get [key] 存在则返回value 不存在返回nil
   get age

//批量设值
   mset country china city beijing
   //批量获取
   mget country city
   ```
   
   批量设值、批量获取
   
   ![image-20210217152742103](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217152742103.png)
    常用命令
   
   ```redis
   incr age //必须为整数自加1，非整数返回错误，无age键从0自增返回1
   decr age  //整数age减1
   incrby age 2  //整数age+2
   decrby age 2//整数age -2
   incrbyfloat score 1.1 //浮点型score+1.1
   append追加指令：
       set name hello; append name world 
       //追加后
       helloworld
   字符串长度：
      set hello “世界”；strlen hello//结果6，每个中文占3个字节
   截取字符串：
      set name helloworld ; getrange name 2 4//返回 llo
   
   ```

2. 哈希(hash)

   哈希(hash)是一个string类型的field和value的映射表，哈希特适合用于存储对象

   假设user有如下表结构

   |id| name | age  |
   | ---- | ---- | ---- |
   |1| gss  | 25 |

   如果使用string结构进行存储
   
   ```redis
   set user:1:name gss
   set user:1:age 25
   ```
   
   如果使用hash结构进行存储
   
   ```redis
   hset user:1 name gss age 25
   ```
   
   命令
   
   ​	设值：hset  key field value
   
   ​	取值：hget key field
   
   ​	批量设值：hmset key [field value ...]
   
   ​	批量取值：hmget key field1 field2 field3
   
   ​	获取所有field：hkeys key
   
   ​	获取所有value：hvals key
   
   ​	获取所有field和value：hgetall key
   
   ​	计算个数：hlen key
   
   ​	判断field是否存在：hexists key field
   
   ​	增加：hincrby key field increment
   
   ![image-20210217163026371](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217163026371.png)
   
   ![image-20210217163048399](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217163048399.png)
   
   ![image-20210217163133507](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217163133507.png)

三种方案实现对象信息存储优缺点对比

- 原生：set user:1:name james;
              set user:1:age  23;
              set user:1:sex boy;
        优点：简单直观，每个键对应一个值
        缺点：键数过多，占用内存多，用户信息过于分散，不用于生产环境

- 将对象序列化存入redis
        set user:1 serialize(userInfo);
        优点：编程简单，若使用序列化合理内存使用率高
        缺点：序列化与反序列化有一定开销，更新属性时需要把userInfo全取出来进行反序列化，更新后再序列化到redis

- 使用hash类型：
          hmset user:1 name james age 23 sex boy
     优点：简单直观，使用合理可减少内存空间消耗
     缺点：要控制ziplist与hashtable两种编码转换，且hashtable会消耗更多内存erialize(userInfo);

  

3. 列表(list)

   用来存储多个有序的字符串，一个列表最多可存2^32-1个元素

   因为有序，可以通过索引下标获取元素活某个范围内元素列表

   列表元素可重复

   lpush 左进

   rpush 右进

   lpop 左出

   rpop 右出

   ![image-20210217165602637](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217165602637.png)

   命令

   ​	右添加：rpush key [element ...]

   ​	左添加：lpush key [element ...]

   ​	右删除：rpop key

   ​	左删除：lpop key	

   ​	查找：lrange key start end   //索引下标特点：从左到右为0到(N-1)，从右到左为-1到-N，所以查询所有的命令为：lrange key 0 -1

   ​	检索：lindex key index  //从左到右为0到N-1.从右到左为-1到-N，所以查询所有的命令为：lrange key 0 -1

   ​	当前列表长度：llen key

   ​	在pivot前或者后插入element：linsert key BEFORE|AFTER pivot element

   ​	![image-20210217174958120](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217174958120.png)

   ![image-20210217175125583](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217175125583.png)

   ![image-20210217175233183](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217175233183.png)

4. 集合(set)

5. ![image-20210217180742290](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217180742290.png)

   不允许有重复元素且集合无序，一个集合最多可存2^32-1个元素，除了支持增删改查，还支持集合交集、并集、差级；

   命令

   ​	添加：sadd key member [member ...] //可添加一个或多个

   ​	获取所有元素：smembers key

   ​	删除：srem key member [member ...]

   ​	计算元素个数：scard key

   ![image-20210217180633879](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217180633879.png)

6. 有序集合(zset)

   

   ![image-20210217180902916](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217180902916.png)

   有序集合与集合及队列区别：

   ![image-20210217184553905](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217184553905.png)

   命令

   ​	添加：zadd key [NX|XX] [CH] [INCR] score member [score member ...]

   ​	查找：zrange key start stop [withscores]

   |                   命令                   | 描述                                                         |
   | :--------------------------------------: | ------------------------------------------------------------ |
   | zadd key score1 member1 [score2 member2] | 向有序集合添加一个或多个成员，或者更新已存在成员的分数       |
   |                zcard key                 | 获取有序集合的成员数                                         |
   |            zcount key min max            | 计算在有序集合中指定区间分数的成员数                         |
   |       zincrby key increment member       | 有序集合中对指定成员的分数加上增量 increment                 |
   |   zrange key start stop [WITHSCORES\]    | 通过索引区间返回有序集合指定区间内的成员                     |
   |            zscore key member             | 返回有序集中，成员的分数值                                   |
   |           zrevrank key member            | 返回有序集合中指定成员的排名，有序集成员按分数值递减(从大到小)排序 |
   |       zrem key member [member ...]       | 移除有序集合中的一个或多个成员                               |
   
   更多参数参考菜鸟教程：https://www.runoob.com/redis/redis-sorted-sets.html

## redis常用命令

- TTL命令

  Redis TTL命令以秒为单位返回key的剩余过期时间。

  语法：ttl key

  ![image-20210217172146062](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217172146062.png)

  当 key 不存在时，返回 -2 。 当 key 存在但没有设置剩余生存时间时，返回 -1 。 否则，以秒为单位，返回 key 的剩余生存时间。

  **注意：**在 Redis 2.8 以前，当 key 不存在，或者 key 没有设置剩余生存时间时，命令都返回 -1 。

- FLUSHDB命令

  Redis FLUSHDB命令用于清空当前数据库中的所有 key。

  语法：FLUSHDB

- DBSIZE命令

  Redis Dbsize 命令用于返回当前数据库的 key 的数量。

  语法：DBSIZE

- EXISTS命令

  Redis EXISTS 命令用于检查给定 key 是否存在。

  语法：EXISTE key

  返回值：若key存在返回1，否则返回0。

- FLUSHALL命令

  Redis FLUSHALL命令用于清空整个 Redis 服务器的数据(删除所有数据库的所有 key )。

  语法：FLUSHALL
  
- SELECT命令

  Redis Select 命令用于切换到指定的数据库，数据库索引号 index 用数字值指定，以 0 作为起始索引值。(一共16个数据库 0-15)

  语法：SELECT index

- KEYS命令

  Redis Keys 命令用于查找所有符合给定模式 pattern 的 key 。

  语法：KEYS PATTERN

  ```redis
  //查找当前数据库所有key
  keys *
  ```

- DEL命令

  Redis DEL 命令用于删除已存在的键。不存在的 key 会被忽略。

  语法：DEL key
  
- TYPE命令

  Redis Type 命令用于返回 key 所储存的值的类型。

  语法：TYPE key

  ![image-20210217190527120](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210217190527120.png)

- EXPIRE

  Redis Expire 命令用于设置 key 的过期时间，key 过期后将不再可用。单位以秒计。

  语法：EXPIRE key seconds

## redis desktop manager 连接不上redis服务器

1. 检查在redis服务器上是否能连接redis

   进入到redis中src目录下

   ```redis
   # ./redis-cli -h 192.168.1.112 -p 6379 -a redis
   ```

2. 查看redis配置文件redis.conf

   通过/bind 127.0.0.1搜索将其注释掉或者改为 bind 0.0.0.0

   ![image-20210218162601555](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210218162601555.png)

   通过/requirepass foobared搜索到后将注释打开，将foobared修改为要为redis设置的密码

   ![image-20210218162738425](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210218162738425.png)

   通过/protected-mode yes搜索后将yes改为no

   ![image-20210218164414935](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210218164414935.png)

3. 确保redis端口开放

   6379是redis的默认端口，不打开端口，其他计算机将无法访问redis

   查看防火墙是否将6379端口开放

   ```linux
   firewall-cmd --query-port=6379/tcp
   ```

   

   如果提示firewall-cmd未找到该命令，使用yum安装

   ```linux
   yum install firewalld
   ```

   

   如果防火墙没有运行并显示 	firewalld is not running

   使用

   ```linux
   systemctl start firewalld.service
   ```

   将防火墙打开

   然后再将6379端口打开

   ```linux
   firewall-cmd --add-port=6379/tcp
   ```

   再次查看防火墙是否将6379端口开放，返回yes

   ![image-20210218163200657](C:\Users\耿帅帅\AppData\Roaming\Typora\typora-user-images\image-20210218163200657.png)

