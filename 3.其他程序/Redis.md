## 一、Redis数据类型

### 1.String(字符串)

- 是最基本的数据类型，可以包含任何数据包括图片和视频等，最大存储容量是512MB

#### （1）添加数据

- 添加或修当数据【key存在时修改数据，不存在则添加数据】

  ```
  set key value
  ```

- 添加或修改多个数量的数据

  ```
  mset key value [key value...]
  ```

- 添加单个数据【setnx、msetnx成功返回1,失败返回0。添加的键已存在则失败(主要保护数据安全)】

  ```
  setnx key value
  ```

- 添加多个数量的数据

  ```
  msetnx key value [key value...]
  ```

#### （2）读出数据

- 读取单个数据

  ```
  get key
  ```

- 读取多个数据

  ```
  mget key [key...]
  ```

- 读取字符串部分字符【start：索引开始位置起始值为0，end：索引结束值】

  ```
  getrange key start end
  ```

- 获取字符串长度

  ```
  strlen key
  ```

#### （3)修改数据

- 在字符串末尾添加字符

  ```
  append key value
  ```

- 将键中存储的数值加一

  ```
  incr key
  ```

- 将键中存储的数值减一

  ```
  decr key
  ```

- 将键中存储的数字加上指定的值【decrement指定要减去的值，如果非数字则会报错】

  ```
  incrby key decrement
  ```

- 将键中存储的数字减去指定的值

  ```
  indecr key decrement
  ```

### 2.Hash(哈希表)

- 是一个键值对集合，hash时String类型的field和value的映射表，适用于存储对象。

#### （1）添加数据

- 添加或修改键值对【key值表明，filed和value是键值对】

  ```
  hset key filed value
  ```

- 添加或修改多个键值对

  ```
  hmset key filed value
  ```

- 将单个键值对添加到嘻哈表中【当key表中field没有同名的时候才能创建，目的是保护数据安全】

  ```
  hsetnx key filed value
  ```

#### （2）读取数据

- 获取嘻哈表指定的字段值

  ```
  hget key filed
  ```

- 获取多个嘻哈表中指定的值

  ```
  hmget key filed [filed...]
  ```

- 获取嘻哈表中所有的field名

  ```
  hkeys key
  ```

- 获取嘻哈表中所有的value值

  ```
  hvals key 
  ```

- 获取所有field和value值【奇数列为field，偶数为value】

  ```
  hgetall key
  ```

- 读取哈希表中指定的字段是否存在【存在返回1，否则返回0】

  ```
  hexists key filed
  ```

- 获取哈希表字段的数量【如果hesh列表不存在则返回0】

  ```
  hlen key
  ```

#### （3）删除数据

- 删除哈希表中指定的键值对

  ```
  hdel key field [field...]
  ```

### 3.List(有序列表)

- 是一个简单的有序的字符串列表。最多存储2^32-1个元素（约40多亿）

#### （1）添加数据

- 把指定的列表值依次添加到左边(前面)【value1添加表中，value2添加表最左边，以此类推】

  ```
  lpush key value[value...]
  ```

- 把指定的列表值依次添加到右边(后面)

  ```
  rpush key value[value...]
  ```

- 将单个值添加到列表左边【lpushx和rpushx只能够在因存在的列表中添加值，不能创建列表。】

  ```
  lpushx key value
  ```

- 将单个值添加到列表右边

  ```
  rpushx key value
  ```

- 通过索引修改元素的值【index索引值，lset只能修改列表不能创建列表】

  ```
  lset key index value
  ```

#### （2）读取数据

- 读取范围内元素【start开始索引位置，end索引结束位置】

  ```
  lrange key start end
  ```

- 读取指定索引的数据【index指定的索引】

  ```
  lindex key index
  ```

- 获取列表长度

  ```
  llen key
  ```

#### （3）删除数据

- 移除列表左边的元素

  ```
  lpop key
  ```

- 移除类别右边的元素

  ```
  rpop key
  ```

### 4.Set(无序集合)

- set集合是string类型的无序集合，集合是通过哈希表实现的， 所以添加、删除、查找的复杂度都是O(1)，且集合里面的值不能重复。

#### （1）添加元素

```
sadd key member [member...]
```

#### （2）获取成员数量

```
scard key
```

#### （3）查看元素

- 【返还集合中所有元素】

```
smembers key
```

#### （4）移除集合中指定的元素

```
srem key member [member...]
```

### 5.Zset(有序集合)

- zset和set一样也是string类型元素集合，且不允许重复。不同的是
  - 每个元素都会关联一个double类型可重复的分数，redis通过分数对集合的元素排序
  - 分数越小的索引越靠前，首位索引是0
  - 分数相同时，后添加的元素索引靠前和list列表相似。

#### （1）添加数据

- 在有序集合中添加和修改成员分数【score是分数，member是集合中的值】

  ```
  zadd key score member [score member...]
  ```

#### （2）读取数据

- 通过索引区间返回有序集合指定区间的成员

  ```
  zrange key start stop
  ```

- 获取指定分数之间的所有成员【全闭合区间、min最小分数、max最大分数【

  ```
  zrangebysore key min max
  ```

- 获取所有集合成员的数量

  ```
  zcard key
  ```

- 计算指定分数范围内的成员数量

  ```
  zcount key min max
  ```

- 返回有序集合中指定成员的索引

  ```
  zrank key member
  ```

- 返回集合中指定成员的分数

  ```
  zscore key member
  ```

#### （3）删除数据

- 移除有序集合中的指定的成员

  ```
  zrem key member [member...]
  ```

- 移除集合中给定排名区间的所有成员(按索引删除)

  ```
  zremrangegebyrank key start stop
  ```

- 移除结合中指定分数区间的所有成员

  ```
  zremrangebyscore key min max
  ```

## 二、redis命令

### 1.启动客户端(reids-cli)

```
redis-cli -h [redis服务器IP地址] -p [redis的端口号] -a [redis密码]
```

### 2.redis操作命令

#### （1）列出指定的键

- *通配符，代表所有的键。

```
keys *
```

#### （2）获取键的总数

```
dbsize
```

#### （3）查询键是否存在

- 返回键的个数。

```
exists key [key...]
```

#### （4）查询键的类型

```
type key
```

#### （5）返回数据库中随机一个键

```
randomkey
```

#### （6）修改键名

- 修改键的名称，当新名字在内存中存在时，会覆盖掉原来的。

  ```
  rename key newkey
  ```

- 修改键的名称，当新名字在内存中已存在时，创建失败

  ```
  renamex key newkey
  ```

#### （7）删除指定键

```
del key [key...]
```

#### （8）删除当前库中所有的键

- 删除当前数据库中所有的键

  ```
  flushdb
  ```

- 删除所有数据库中的所有键

  ```
  flushall
  ```

### 3.redis选择数据库

- 默认库编号是0，默认库数量是16个编号0-15，可以调试配置文件进行设置

```
select 0
```

### 4.redis设置键的时间

#### （1）设置时间

- 以秒设置时间，超过时间会被回收【second秒值】

  ```
  expire key second 
  ```

- 以毫秒设置时间【millseconds毫秒值】

  ```
  pexpire key milliseconds
  ```

#### （2）查看和移除时间

- 返回以秒剩余的时间

  ```
  ttl key
  ```

- 返回以毫秒剩余的时间

  ```
  pttl key
  ```

- 清除键过期的时间

  ```
  expire key 
  ```

### 5.链接

```
>认证：需要提前设置好密码
auth password
>测试是否链接成功
ping
```

### 6.服务

```
>产看服务信息（服务状态，客户端状态、用户状态等）
info
>Redis数据持久化
```

### 7.退出

```
exit 或 quit
```

## 三、rediso发布订阅

- 概念：当一个客户端通过publish命令向订阅者发布信息的时候，我们称这个客户端为发布者（publisher），而另一个客户端使用subscribe或者psubscribe命令接受此信息的时候，我们称这个客户端为订阅者（subscriber），为了解耦发布者和订阅者之间的关系，redis使用channel（频道）作为两者中介---发布者将信息直接发布给channel，而channel负责将信息发送给适当的订阅者，发布者和订阅者之间没有相互关系，也不知道对方的存在。

### 1.使用方法

- 客户端窗口执行，创建订阅,可以是创建多个订阅。

  ```
  subscribe channel [channel..]
  ```

- 第二个客户端执行【channel指定频道、message发布的消息】

  ```
  publish channel message 
  ```

### 2.其他命令

```
①	订阅一个或多个符合给定模式的频道。
PSUBSCRIBE  pattern  [pattern ...]
②	查看订阅与发布系统状态。
PUBSUB  subcommand  [argument [argument ...]]
③	将信息发送到指定的频道。
PUBLISH   channel   message
④	退订所有给定模式的频道。
PUNSUBSCRIBE   [pattern [pattern ...]]
⑤	订阅给定的一个或多个频道的信息。
SUBSCRIBE   channel   [channel ...]
⑥	指退订给定的频道。
UNSUBSCRIBE  [channel [channel ...]]
```

## 四、redis事务(multi / exec)

- Redis的事务实际上就是可以一次性执行多个命令的队列
  - 批量操作发送exec命令前被放入列队缓存
  - 收到exec命令后进入事物执行，事物中任意命令执行失败，其余命令依然执行
  - 在事物执行过程中，其他客户端的命令请求不会插入到事物命令序列中
  - 事物三个阶段（1）开始事物（2）命令入队（3）执行事物
- 注意：当命令执行错误时不影响后面的，不会停止执行，如get的string没有，但是语法错误会回滚，整个事物一条也不执行。

```
~>multi
~>set string "springmvc"
QUEUED
~>get string
QUEUED
~>exec
1)OK
2)"springmvc"
```

## 五、redis介绍

### 1.简介

Redis 是完全开源的，遵守 BSD 协议，是一个高性能的 key-value 数据库。

Redis 与其他 key - value 缓存产品有以下三个特点：

- Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
- Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
- Redis支持数据的备份，即master-slave模式的数据备份。

### 2.关系型和非关心型数据库

- 关系型数据库（mysql）
  - 数据是存储在物理硬盘上的。
  - 有三种状态：临时状态、持久化、游离态：托管状态。
- 非关系型数据库（nomysql）
  - 数据存储在内存中。
  - 数据没有关联和关系可循，数据之间是独立的。

### 3.redis游戏

- 性能极高 – Redis能读的速度是110000次/s,写的速度是81000次/s 。
- 丰富的数据类型 – Redis支持二进制案例的 Strings, Lists, Hashes, Sets 及 Ordered Sets 数据类型操作。
- 原子 – Redis的所有操作都是原子性的，意思就是要么成功执行要么失败完全不执行。单个操作是原子性的。多个操作也支持事务，即原子性，通过MULTI和EXEC指令包起来。
- 丰富的特性 – Redis还支持 publish/subscribe, 通知, key 过期等等特性。

### 4.Radis与其他key-value存储不同

- Redis有着更为复杂的数据结构并且提供对他们的原子性操作，这是一个不同于其他数据库的进化路径。Redis的数据类型都是基于基本数据结构的同时对程序员透明，无需进行额外的抽象。
- Redis运行在内存中但是可以持久化到磁盘，所以在对不同数据集进行高速读写时需要权衡内存，因为数据量不能大于硬件内存。在内存数据库方面的另一个优点是，相比在磁盘上相同的复杂的数据结构，在内存中操作起来非常简单，这样Redis可以做很多内部复杂性很强的事情。同时，在磁盘格式方面他们是紧凑的以追加的方式产生的，因为他们并不需要进行随机访问。

### 5.redis数据库在开发环境是什么角色

- 在开发过程中，如果程序分为关系型数据库会产生很多io通道，且关系型数据库在io通道方面有严格的把控（io通道很消耗资源），为了减少与关系型数据库的频繁交互，中间添加nosql数据库，进行数据过渡，再有nosql数据库持久化到关系型数据库中

## 六、配置文件

- 核心配置文件redis.window.conf（linux下是redis.conf）
- Port:指定redis监听端口，默认是6379
- Daemonize no：使用yes是启动线程守护，默认是no（windows不支持守护线程的配置为no）
- Bind 127.0.0.1：绑定的主机地址（对应的主机地址）
- Timeout:当客户端限制多长秒后关闭连接，如果指定为0，表示关闭该功能
- Loglevel：指定日志记录级别，debug、verbose、notice、waring，默认的notice
- Logfile：日志记录方式，默认是标准输出，如果配置redis为进程守护方式运行，而这里又配置日志记录方式为标准输出，则日志将会发送给/dev/null
- Databases 16:设置数据库的数量，默认数据库为0，可以使用select命令在连接上指定数据库id
- Save < seconds> < changes>：指定在多长时间内，有多少次更新操作，就将数据同步到数据文件，可以多个条件配合
- rdbcompression yes:指定存储至本地数据库时是否压缩数据，默认为yes，redis采用lzf压缩，如果为了节省cpu时，可以关闭，但是会导致数据库文件变大
- dbfilename dump.rdb：指定本地数据库文件名称，默认dump.rdb

## 七、Windows安装

1.下载地址：https://github.com/tporadowski/redis/releases

2.解压：下载后可以解压或安装到指定的地址

3..配置：将Redis-x64-3.3.100下载的目录配置到环境变量中

4.修改配置：打开redis.windows.conf配置文件。

- 修改：bind 127.0.0.1将其注释到，以为默认只能让本机访问。
- 修改：protected-mode no关掉保护模式

5.在安装目录打开cmd，执行 redis-server.exe redis.windos.conf 可配置成服务器。

6.打开另一个cmd窗口执行Redis-cli.exe -h 127.0.0.1 -p 6379 运行。-h是ip地址，-p是端口号。

7.配置windows服务命令：redis-server --service-install redis.windows.conf --loglevel verbose