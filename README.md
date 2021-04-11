## PHP
- [PHP-Interview-QA](https://github.com/colinlet/PHP-Interview-QA)
- [php-interview-2018](https://github.com/sushengbuhuo/php-interview-2018)
- [PHPerInterviewGuide](https://github.com/todayqq/PHPerInterviewGuide)
- [php-engineer-interview-questions](https://github.com/hookover/php-engineer-interview-questions)
- [interview](https://github.com/wanglelecc/interview)
- [php-be-intervie](https://github.com/rucblake/php-be-interview)
- [PHP面试题及答案](https://github.com/lengyue1024/BAT_interviews/blob/master/PHP%E9%9D%A2%E8%AF%95%E9%A2%98%E5%8F%8A%E7%AD%94%E6%A1%88.md)
- [mysql优化面试题](mysql优化面试题.pdf)
- [PHP8新特性之JIT简介](https://www.laruence.com/2020/06/27/5963.html)
- [PHP8新特性盘点](https://blog.thinkphp.cn/2052124)
- [PHP7新特性](https://www.runoob.com/w3cnote/php7-new-features.html)
- [CGI、FastCGI和PHP-FPM关系图解](https://www.awaimai.com/371.html)
- [PHP7为什么比5快](https://blog.csdn.net/changfangyuansh/article/details/102692923)


## 消息队列
- [消息队列高频问题](http://www.mianshigee.com/tag/messagequeen/s1/)
- [2021最新 RabbitMQ面试题精选](https://blog.csdn.net/lupengfei1009/article/details/114525479)

## 缓存
- [redis中跳表原理&实现](https://blog.csdn.net/mffandxx/article/details/112284405)
- [码上一波 Redis 面试题，面试跳槽不要慌!](https://blog.csdn.net/weixin_50333534/article/details/112447835?spm=1001.2014.3001.5501)
- [2021一波最新 Redis 面试题](https://blog.csdn.net/weixin_50333534/article/details/112447879?spm=1001.2014.3001.5501)
- [2021年最新版 68道Redis面试题](https://www.php.cn/faq/457390.html)
- [史上最全的50个Redis面试题及答案](https://www.php.cn/redis/436652.html)
- [2021年Redis面试题（持续更新）](https://blog.csdn.net/qq1515312832/article/details/113880849)

## Linux

### 统计nginx日志里访问次数最多的前十个IP
```bash
awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -nr -k1 | head -n 10
```

## 常见算法
- [数据结构与算法系列目录](https://www.cnblogs.com/skywang12345/p/3603935.html)

### 树常见面试题
- [红黑树常见面试问题整理](https://blog.csdn.net/fantacy10000/article/details/100855055)
- [红黑树之原理和算法详细介绍](https://www.cnblogs.com/skywang12345/p/3245399.html)
- [B树，B+树，红黑树 数据库常见面试题](https://blog.csdn.net/zhangshk_/article/details/83013482)
- [腾讯、阿里面试题 了解B+树吗？](https://blog.csdn.net/zycxnanwang/article/details/105384618)

### 二分查找

```php
#二分查找
function binarySearch(Array $arr, $target) {
    $low = 0;
    $high = count($arr) - 1;
        
    while($low <= $high) {
        $mid = floor(($low + $high) / 2);
        #找到元素
        if($arr[$mid] == $target) return $mid;
        #中元素比目标大,查找左部
        if($arr[$mid] > $target) $high = $mid - 1;
        #重元素比目标小,查找右部
        if($arr[$mid] < $target) $low = $mid + 1;
    }
    #查找失败
    return false;
}
```

### 冒泡排序

```php
$demo_array = array(23,15,43,25,54,2,6,82,11,5,21,32,65);
// 第一层for循环可以理解为从数组中键为0开始循环到最后一个
for ($i=0;$i<count($demo_array);$i++) {
    // 第二层将从键为$i的地方循环到数组最后
    for ($j=$i+1;$j<count($demo_array);$j++) {
        // 比较数组中相邻两个值的大小
        if ($demo_array[$i] > $demo_array[$j]) {
            $tmp            = $demo_array[$i]; // 这里的tmp是临时变量
            $demo_array[$i] = $demo_array[$j]; // 第一次更换位置
            $demo_array[$j] = $tmp;            // 完成位置互换
        }
    }
}
```

### 快速排序

```php
function quick_sort($arr){
    //先判断是否需要继续进行
    $length = count($arr);
    if($length <= 1) {
        return $arr;
    }
    //选择第一个元素作为基准
    $base_num = $arr[0];
    //遍历除了标尺外的所有元素，按照大小关系放入两个数组内
    //初始化两个数组
    $left_array = array();  //小于基准的
    $right_array = array();  //大于基准的
    for($i=1; $i<$length; $i++) {
        if($base_num > $arr[$i]) {
            //放入左边数组
            $left_array[] = $arr[$i];
        } else {
            //放入右边
            $right_array[] = $arr[$i];
        }
    }
    //再分别对左边和右边的数组进行相同的排序处理方式递归调用这个函数
    $left_array = quick_sort($left_array);
    $right_array = quick_sort($right_array);
    //合并
    return array_merge($left_array, array($base_num), $right_array);;
}
```

## 常见问题

### Redis跳表的实现,延迟队列的实现

```
Redis跳表的实现是由一个双向链表和分成结构实现的, 分成的机制是有抛硬币决定的,连续抛出正面的次数决定了他的层数, 节点中只保存了索引书和指针浪费的内存可以忽略不计

延时队列使用有序集合实现 score 存到期时间key为消息内容, 并使用zrangebyscore(0 - 当前时间,limit 1)进行消费

```

### 大批量导入数据（百万级别以上）

```
mysql load data 拆分文件 多开  InnoDB Buffer 关闭binlog 改 myisam
PHP insert合并 事务  有序 扛得住可以多开
```

### tcp和udp的区别

```
TCP/IP(链路层,网络层,传输层,应用层)

UDP(无连接,单播-多播-广播,面向报文,不可靠)

UDP无连接(不可靠,支持一对一,一对多,多对一和多对多交互通信,面向报文,首部开销小，仅8字节),适用于实时应用（IP电话、视频会议、直播等）
TCP面向连接(可靠,只能是一对一通信,面向字节流,首部最小20字节，最大60字节),适用于要求可靠传输的应用，例如文件传输
```

### 击穿缓存，直接访问数据库，导致服务不可用怎么办

```
在缓存失效的时候（判断拿出来的值为空），不是立即去load db，而是先使用缓存工具的某些带成功操作返回值的操作（比如Redis的SETNX或者Memcache的ADD）去set一个mutex key，当操作返回成功时，再进行load db的操作并回设缓存, 否则，就重试整个get缓存的方法

事前：Redis 高可用，主从+哨兵，Redis cluster，避免全盘崩溃。

事中：本地 ehcache 缓存 + Hystrix 限流+降级，避免MySQL被打死。

事后：Redis 持久化 RDB+AOF，一旦重启，自动从磁盘上加载数据，快速恢复缓存数据。

```

### 给定一个大文件（内存放不下），如何排序

```
PHP可以使用迭代器,实现流程: 拆分成多个小文件 -> 对单个小文件排序 -> 在从各个小文件读取指定数据(可顺序,倒叙)进行排序 -> 合并输出

```

### php-fpm原理
```
php-fpm是一种master（主）/worker（子）多进程架构，与nginx设计风格有点类似。master进程主要负责CGI及PHP环境初始化、事件监听、子进程状态等等, worker进程负责处理php请求。

master只是负责管理工作，并不是很多人认为的把客户端发来的请求分给worker进程处理，而是由worker进程负责客户端的请求监听和处理, master只负责管理worker，如重启，重新加载配置文件，并不会派发请求。
worker是同步阻塞,必须等这次处理完，才会处理其它请求,并发性能不行.
杀掉 master 正常工作
```

### MySQL主从同步不一致的原因

```
原因
    人为原因导致从库与主库数据不一致（从库写入）
    主从复制过程中，主库异常宕机
    设置了ignore/do/rewrite等replication等规则
    binlog非row格式
    异步复制本身不保证，半同步存在提交读的问题，增强半同步起来比较完美。 但对于异常重启（Replication Crash Safe），从库写数据（GTID）的防范，还需要策略来保证。
    从库中断很久，binlog应用不连续，监控并及时修复主从
    从库启用了诸如存储过程，从库禁用存储过程等
    数据库大小版本/分支版本导致数据不一致？，主从版本统一
    备份的时候没有指定参数 例如mysqldump --master-data=2 等
    主从sql_mode 不一致
    一主二从环境，二从的server id一致
    MySQL自增列 主从不一致
    主从信息保存在文件里面，文件本身的刷新是非事务的，导致从库重启后开始执行点大于实际执行点
    采用5.6的after_commit方式半同步，主库当机可能会引起主从不一致，要看binlog是否传到了从库
    启用增强半同步了（5.7的after_sync方式），但是从库延迟超时自动切换成异步复制
预防和解决的方案
    配置 redolog&binlog 及时写入磁盘
    设置从库库为只读模式
    可以使用5.7增强半同步避免数据丢失等
    binlog row格式
    必须引定期的数据校验机制
    当使用延迟复制的时候，此时主从数据也是不一致的（计划内），但在切换中，不要把延迟从提升为主库哦~
    mha在主从切换的过程中，因主库系统宕机，可能造成主从不一致（mha本身机制导致这个问题）    

```

### mysql事务的底层实现

> [mysql事务的底层实现](http://www.pladios.top/archives/mysql%E4%BA%8B%E5%8A%A1%E5%BA%95%E5%B1%82%E5%AE%9E%E7%8E%B0)

```
事务具有ACID四个特性。也即：原子性，一致性，隔离性，持久性


原子性的实现:  这个事务，要么成功commit，要么失败rollback。其实更简单的来说，原子性需要保证，事务发生了异常，能够rollback。
原子性的核心，就是一个可回滚的操作。
undo log(回滚日志）undo log事务中，用于存放数据被修改时操作相反的逻辑操作。

持久性的实现:  一个事务一旦提交，它对数据库中数据的改变就应该是永久性的。但是事务回滚，这个数据是不会改变的。所以在持久性的体现主要在事务提交。在MySQL实现持久性，主要是通过redo log保证的
redo log(重做日志)   redo log包括两部分，重做日志缓冲（redo log buffer）和重做日志文件（redo log file），前者是易失的缓存，后者是持久化的文件。
当事务提交时，必须先将事务的所有日志写入日志文件进行持久化

隔离性的实现: 隔离性，就是根据容忍程度，定义了四个隔离级别，解决三个问题。
```

### 索引的原理，B-tree和B+tree的区别

```
索引的原理: 通过不断的缩小想要获得数据的范围来筛选出最终想要的结果，同时把随机的事件变成顺序的事件，也就是我们总是通过同一种查找方式来锁定数据。

MyISAM索引文件和数据文件是分离的，索引文件仅保存数据记录的地址。而在InnoDB中，表数据文件本身就是按B+Tree组织的一个索引结构，这棵树的叶节点data域保存了完整的数据记录。这个索引的key是数据表的主键，因此InnoDB表数据文件本身就是主索引。

B-tree中非叶子节点可以存值；但是B+tree非叶子节点不可以存值，只能存key，值只存在叶子节点中。
B-tree中叶子节点没有用指针连接起来；而B+tree中的叶子节点用指针连接起来，所以B+tree的查询很快，当定位到叶子节点后，只需要遍历叶子节点即可。B+树相比于B树能够更加方便的遍历。
B+树简单的说就是变成了一个索引一样的东西。 B+的搜索与B-树也基本相同，区别是B+树只有达到叶子结点才命中（B-树可以在非叶子结点命中），B+树的性能相当于是给叶子节点做一次二分查找。
B+树的查找算法：当B+树进行查找的时候，你首先一定需要记住，就是B+树的非叶子节点中并不储存节点，只存一个键值方便后续的操作，所以非叶子节点就是索引部分，所有的叶子节点是在同一层上，包含了全部的关键值和对应数据所在的地址指针。这样其实，进行 B+树的查找的时候，只需要在叶子节点中进行查找就可以了。

```

### mvcc的原理

```
MVCC是通过在每行记录后面保存两个隐藏的列来实现的。这两个列，一个保存了行的创建时间，一个保存行的过期时间（或删除时间）。当然存储的并不是实际的时间值，而是系统版本号（system version number)。每开始一个新的事务，系统版本号都会自动递增。事务开始时刻的系统版本号会作为事务的版本号，用来和查询到的每行记录的版本号进行比较。

```

### 前缀索引

```
对于列的值较长，比如BLOB、TEXT、VARCHAR，就必须建立前缀索引，即将值的前一部分作为索引。这样既可以节约空间，又可以提高查询效率。但无法使用前缀索引做 ORDER BY 和 GROUP BY，也无法使用前缀索引做覆盖扫描
```

### Mysql回表原理

```
MySQL innodb的主键索引是簇集索引，也就是索引的叶子节点存的是整个单条记录的所有字段值，不是主键索引的就是非簇集索引，非簇集索引的叶子节点存的是主键字段的值。回表是什么意思？就是你执行一条sql语句，需要从两个b+索引中去取数据。举个例子：

表tbl有a,b,c三个字段，其中a是主键，b上建了索引，然后编写sql语句

SELECT * FROM tbl WHERE a=1

这样不会产生回表，因为所有的数据在a的索引树中均能找到

SELECT * FROM tbl WHERE b=1

这样就会产生回表，因为where条件是b字段，那么会去b的索引树里查找数据，但b的索引里面只有a,b两个字段的值，没有c，那么这个查询为了取到c字段，就要取出主键a的值，然后去a的索引树去找c字段的数据。查了两个索引树，这就叫回表。

索引覆盖就是查这个索引能查到你所需要的所有数据，不需要去另外的数据结构去查。其实就是不用回表。

怎么避免？不是必须的字段就不要出现在SELECT里面。或者b,c建联合索引。但具体情况要具体分析，索引字段多了，存储和插入数据时的消耗会更大。这是个平衡问题。
```

### 常见协议层

```
OSI分层(7层)
    物理层 -> 数据链路层 -> 网络层 -> 运输层 -> 会话层 -> 表示层 -> 应用层
五层协议(是OSI和TCP/IP的综合)
    物理层 -> 数据链路层 -> 网络层 -> 运输层 -> 应用层
TCP/IP(4层)
    网络接口层 -> 网际层 -> 运输层 -> 应用层    
```

### TCP三次握手

> 为什么要三次握手:  为了防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误, 三次握手保证了数据的正确性，避免了因网络问题带来的问题。同时防止server端的一直等待，浪费资源。

```
1. 客户端发送一个TCP的SYN=1的包(SYN=1, seq=客户端序列号) 客户端进入SYN_SEND状态 
2. 服务器发回ACK确认包(SYN=1, ACK=1, seq=服务端序列号, ACKnum(确认序号)=客户的ISN加1) 服务器端进入SYN_RCVD状态 
3. 客户端再次发送ACK确认包(ACK=1，seq=客服端的ISN+1 ACKnum(确认序号)=服务端的ISN加1) 客户端进入ESTABLISHED(已确认)状态,服务端收到到后进入ESTABLISHED(已确认)状态 
```

### TCP四次挥手

>为什么要四次挥手: 确保数据能够完成传输, 当收到对方的FIN报文通知时，它仅仅表示对方没有数据发送给你了；但未必你所有的数据都全部发送给对方了,你可能还需要发送一些数据给对方之后，再发送FIN报文给对方来表示你同意现在可以关闭连接了，所以它这里的ACK报文和FIN报文多数情况下都是分开发送的

```
1. 客服端发送FIN=1标志位置为1的包(FIN=1，seq=x) 客户端进入FIN_WAIT_1状态
2. 服务器端发送一个ACK确认包(ACK=1，ACKnum=x+1) 服务器端进入CLOSE_WAIT状态 (客户端接收到这个确认包之后，进入FIN_WAIT_2状态)
3. 服务器端发送一个结束连接请求(FIN=1，seq=y) 服务器端进入LAST_ACK状态(等待来自客户端的最后一个ACK)
4. 客户端接收到后发送一个ACK确认包，并进入TIME_WAIT状态(可能出现的要求重传的ACK包) 等待了某个固定时间 进入CLOSED状态
```

### Cookie&Session区别
```
存储位置不同 (cookie放在客服端,session在服务端)
存储容量不同 (cookie大小受浏览器限制,对于session来说并没有上限)
隐私策略不同 (cookie对客户端是可见的,session存储在服务器上)
```

###  Http报文格式

```
请求
    请求行：请求方法 + URL + 协议/版本号
    请求头部：浏览器告知给服务端的属性信息
    空行
    请求主体：请求相关的数据信息（参数等）
响应
    响应行：协议/版本号 + 状态码 + 描述信息
    响应头部：服务端告知浏览器的属性信息
    空行
    响应主体：响应数据(html文件等)    
```

### 一个完整的HTTP&HTTPS请求

```
http:
    域名解析 -> 发起TCP的3次握手 -> 建立TCP连接后发起http请求 -> 服务器响应http请求 -> TCP连接关闭 -> 浏览器得到html代码 -> 渲染
https(HTTPS跟HTTP一样，只不过增加了SSL):
    验证服务器端 -> 允许客户端和服务器端选择加密算法和密码，确保双方都支持 -> 验证客户端(可选) -> 使用公钥加密技术来生成共享加密数据 -> 创建一个加密的SSL连接
-> 基于该 SSL 连接传递 HTTP 请求
```

### 对称加密和非对称加密的区别
```
对称加密:  是最快速、最简单的一种加密方式, 加密与解密用的是同样的密钥
非对称加密:  
1. A要向B发送信息，A和B都要产生一对用于加密和解密的公钥和私钥。
2. A的私钥保密，A的公钥告诉B；B的私钥保密，B的公钥告诉A。
3. A要给B发送信息时，A用B的公钥加密信息，因为A知道B的公钥。
4. A将这个消息发给B（已经用B的公钥加密消息）。
5. B收到这个消息后，B用自己的私钥解密A的消息，其他所有收到这个报文的人都无法解密，因为只有B才有B的私钥。
6. 反过来，B向A发送消息也是一样。

```

### 常见状态码

>参考
- [Http状态码](其他/Http状态码.md)

```
400：bad requst - 通常是请求语法问题
403：forbidden - 认证授权未通过
404：not found - 资源不存在
500：Internal server error - 不可预期的错误
502：gateway bad - 收到后端无效响应
503：service unavaible - 由于临时的服务器维护或者过载
504：gateway timeout - 服务器尝试执行请求时未能及时收到响应
499：认为是不安全的连接，主动拒绝了客户端的连接
```

### GET和POST方法区别
```
数据存储位置: Get方法放在URL中；Post方法放到body中
数据大小限制: 浏览器对URL长度有限制
安全性: 用户名和密码等参数出现在URL上存在安全隐患
数据类型: GET只允许ASCII字符,POST没有限制
```

### HTTP1.1和HTTP2.0的区别
```
多路复用：连接共享机制让一个连接让可以有多个request请求，服务端通过request请求id区分后让不同的服务端进行响应，让原本的串行的请求-响应模式变为并行，提高传输处理效率
二进制格式：让原本基于文本格式的解析方法变为二进制格式的解析方法，以此来提高解析报文的健壮性
header压缩：通过缓存头部字段来减少传输大小和避免重复发送header字段问题
服务端推送：把客户端所需要的资源伴随着index.html一起发送到客户端，省去了客户端重复请求的步骤，以此提高性能
长连接：同一个TCP连接可以承载多个http请求和响应；而多路复用指的是同一个http连接可以共享
```

### 秒杀&超卖问题

>参考
- [https://blog.csdn.net/zhoudaxia/article/details/38067003](https://blog.csdn.net/zhoudaxia/article/details/38067003)
- [秒杀系统的设计与实现](PHP/秒杀系统的设计与实现.md)


```
分两个步骤解决:
1. 前端
    扩容(加机器，这是最简单的方法，通过增加前端机器来抗峰值) 
    静态化(将页面上的所有可以静态的元素全部静态化，并尽量减少动态元素。通过CDN来抗峰值。)
    限流(可以通过限制 IP,按钮,用户 ID 等来限制单人短时间内发起的请求数量)
    拒绝请求(随机拒绝部分请求来保护整体的可用性,可以使用 nginx 进行限流)
2. 后端
    业务分离(将秒杀业务系统和其他业务分离，单独放在高配服务器上，可以集中资源对访问请求抗压)
    使用缓存(热点数据都从缓存获得，尽可能减小数据库的访问压力)
    库存前置(放入内存中异步同步到数据库,可以使用队列或Redis事务进行减库存操作)
    使用队列(商品放入队列中,来一个人取一个过程中有操作失败,可重新返回队列)
    分流(部署多台机器,通过负载均衡共同处理客户端请求，分散压力。)
    异步(如发短信、更新数据库等，从而缓解服务器峰值压力。)    
```
