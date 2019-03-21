
# 性能测试面试总结

### 一.冒泡排序

冒泡排序是一种效率低下的排序方法，在数据规模很小时，可以采用。数据规模比较大时，最好用其它排序方法。

冒泡排序是一种稳定的排序算法

冒泡排序的效率：O（n²）

冒泡排序原理图：
.： 
    ![.： 
](https://github.com/guoshijiang/most-beautiful-programming/blob/master/Image/1.png)

冒泡排序 Python 代码实现

    #!/usr/bin/env python
    # coding:utf-8

    def bubbleSort(nums):
        for i in range(len(nums)-1):    # 这个循环负责设置冒泡排序进行的次数
            for j in range(len(nums)-i-1):  # ｊ为列表下标
                if nums[j] > nums[j+1]:
                    nums[j], nums[j+1] = nums[j+1], nums[j]
        return nums

    nums = [5,2,45,6,8,2,1]

    print bubbleSort(nums)


### 二.数据库左链接on条件，跟where条件的结果比对


on 条件是在生成临时表时使用的条件，它不管on中的条件是否为真，都会返回左边表中的记录。
where 条件是在临时表生成好后，再对临时表进行过滤的条件。这时已经没有left join的含义（必须返回左边表的记录）了，条件不为真的就全部过滤掉。

### 三.MySql数据库索引原理

#### MySql数据库的索引类型

##### 简介

MySql数据库的索引方式有普通索引，唯一索引，主键索引，组合索引，全文索引；创建索引的语句如下：

##### 语句

    CREATE TABLE table_name[col_name data type][unique|fulltext][index|key][index_name](col_name[length])[asc|desc]

1.unique|fulltext为可选参数，分别表示唯一索引、全文索引
2.index和key为同义词，两者作用相同，用来指定创建索引
3.col_name为需要创建索引的字段列，该列必须从数据表中该定义的多个列中选择
4.index_name指定索引的名称，为可选参数，如果不指定，默认col_name为索引值
5.length为可选参数，表示索引的长度，只有字符串类型的字段才能指定索引长度
6.asc或desc指定升序或降序的索引值存储

##### 索引类型

1.普通索引
是最基本的索引，它没有任何限制。它有以下几种创建方式：
（1）直接创建索引

    CREATE INDEX index_name ON table(column(length))

（2）修改表结构的方式添加索引

    ALTER TABLE table_name ADD INDEX index_name ON (column(length))
    
（3）创建表的时候同时创建索引

    CREATE TABLE `table` (
        `id` int(11) NOT NULL AUTO_INCREMENT ,
        `title` char(255) CHARACTER NOT NULL ,
        `content` text CHARACTER NULL ,
        `time` int(10) NULL DEFAULT NULL ,
        PRIMARY KEY (`id`),
        INDEX index_name (title(length))
    )

（4）删除索引

    DROP INDEX index_name ON table
    
2.唯一索引

与前面的普通索引类似，不同的就是：索引列的值必须唯一，但允许有空值。如果是组合索引，则列值的组合必须唯一。它有以下几种创建方式：
（1）创建唯一索引

    CREATE UNIQUE INDEX indexName ON table(column(length))
    
（2）修改表结构

    ALTER TABLE table_name ADD UNIQUE indexName ON (column(length))
    
（3）创建表的时候直接指定

    CREATE TABLE `table` (
        `id` int(11) NOT NULL AUTO_INCREMENT ,
        `title` char(255) CHARACTER NOT NULL ,
        `content` text CHARACTER NULL ,
        `time` int(10) NULL DEFAULT NULL ,
        UNIQUE indexName (title(length))
    );

3.主键索引

是一种特殊的唯一索引，一个表只能有一个主键，不允许有空值。一般是在建表的时候同时创建主键索引：

    CREATE TABLE `table` (
        `id` int(11) NOT NULL AUTO_INCREMENT ,
        `title` char(255) NOT NULL ,
        PRIMARY KEY (`id`)
    );

4.组合索引

指多个字段上创建的索引，只有在查询条件中使用了创建索引时的第一个字段，索引才会被使用。使用组合索引时遵循最左前缀集合

    ALTER TABLE `table` ADD INDEX name_city_age (name,city,age); 

5.全文索引

主要用来查找文本中的关键字，而不是直接与索引中的值相比较。fulltext索引跟其它索引大不相同，它更像是一个搜索引擎，而不是简单的where语句的参数匹配。fulltext索引配合match against操作使用，而不是一般的where语句加like。它可以在create table，alter table ，create index使用，不过目前只有char、varchar，text 列上可以创建全文索引。值得一提的是，在数据量较大时候，现将数据放入一个没有全局索引的表中，然后再用CREATE index创建fulltext索引，要比先为一张表建立fulltext然后再将数据写入的速度快很多。
（1）创建表的适合添加全文索引

    CREATE TABLE `table` (
        `id` int(11) NOT NULL AUTO_INCREMENT ,
        `title` char(255) CHARACTER NOT NULL ,
        `content` text CHARACTER NULL ,
        `time` int(10) NULL DEFAULT NULL ,
        PRIMARY KEY (`id`),
        FULLTEXT (content)
    );

（2）修改表结构添加全文索引

    ALTER TABLE article ADD FULLTEXT index_content(content)

（3）直接创建索引

    CREATE FULLTEXT INDEX index_content ON article(content)
    
四、缺点

1.虽然索引大大提高了查询速度，同时却会降低更新表的速度，如对表进行insert、update和delete。因为更新表时，不仅要保存数据，还要保存一下索引文件。
2.建立索引会占用磁盘空间的索引文件。一般情况这个问题不太严重，但如果你在一个大表上创建了多种组合索引，索引文件的会增长很快。
索引只是提高效率的一个因素，如果有大数据量的表，就需要花时间研究建立最优秀的索引，或优化查询语句。

#### MySql数据库的索引原理



### 四.用登陆过程说下缓存机制

### 五.内存溢出的原因

### 六.进程跟线程的区别

### 七.redis,kafka,docker,bizflow在项目中主要作用是什么

### 八.写个nodejs文件查询查看功能

### 九.http跟https区别

#### 1.HTTPS和HTTP的概念

http的全称：Hypertext Transfer Protocol Vertion （超文本传输协议），说通俗点就是用网络链接传输文本信息的协议。
HTTPS的全称：Secure Hypertext Transfer Protocol（安全超文本传输协议），是在http协议基础上增加了使用SSL加密传送信息的协议。

它是一个安全通信通道，它基于HTTP开发，用于在客户计算机和服务器之间交换信息。它使用安全套接字层(SSL)进行信息交换，简单来说它是HTTP的安全版。 它是由Netscape开发并内置于其浏览器中，用于对数据进行压缩和解压操作，并返回网络上传送回的结果。HTTPS实际上应用了Netscape的安全全套接字层（SSL）作为HTTP应用层的子层。（HTTPS使用端口443，而不是象HTTP那样使用端口80来和TCP/IP进行通信。）SSL使用40位关键字作为RC4流加密算法，这对于商业信息的加密是合适的。HTTPS和SSL支持使用X.509数字认证，如果需要的话用户可以确认发送者是谁。

所以http和https之间的区别就在于其传输的内容是否加密和是否是开发性的内容。

#### 2.HTTPS和HTTP的区别：

1.https协议需要到ca申请证书，一般免费证书很少，需要交费。

2.http是超文本传输协议，信息是明文传输，https 则是具有安全性的ssl加密传输协议。

3.http和https使用的是完全不同的连接方式用的端口也不一样，前者是80，后者是443。

4.http的连接很简单，是无状态的。

5.HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，要比http协议安全。

#### 3.HTTPS解决的问题：

##### 信任主机的问题. 

采用https的server必须从CA申请一个用于证明服务器用途类型的证书. 该证书只有用于对应的server的时候，客户度才信任次主机。所以目前所有的银行系统网站，关键部分应用都是 https 的，客户通过信任该证书，从而信任了该主机，其实这样做效率很低，但是银行更侧重安全。这一点对我们没有任何意义，我们的server采用的证书不管自己issue还是从公众的地方issue，客户端都是自己人，所以我们也就肯定信任该server。
 
* 通讯过程中的数据的泄密和被窜改

一般意义上的https, 就是 server 有一个证书.

a) 主要目的是保证server 就是他声称的server. 这个跟第一点一样.

b) 服务端和客户端之间的所有通讯，都是加密的.

i. 具体讲，是客户端产生一个对称的密钥，通过server 的证书来交换密钥，一般意义上的握手过程。

ii. 加下来所有的信息往来就都是加密的，第三方即使截获，也没有任何意义，因为他没有密钥，当然窜改也就没有什么意义了。

* 少许对客户端有要求的情况下，会要求客户端也必须有一个证书。

a) 这里客户端证书，其实就类似表示个人信息的时候，除了用户名/密码， 还有一个CA 认证过的身份，个人证书一般来说上别人无法模拟的，所有这样能够更深的确认自己的身份。

b) 目前少数个人银行的专业版是这种做法，具体证书可能是拿U盘作为一个备份的载体。

### 十.selenium简介，主要作用

### 十一.代码实现文件上传

### 十二.代码实现读文件中某域名平均响应时间

### 十三.代码实现两个有序列表的中间位置查询

### 十四.linux命令，读日志文件中10万行记录，查询某字符串 重复出现次数最多的前三

### 十五.清空表数据的命令，in是不是走索引

### 十六.http请求全过程

### 十七.Post发送的明文密码安全吗？http跟https的关系

### 十八.数据库索引的作用

### 十九.like是否走索引

### 二十.代码实现:传参数的装饰器

### 二十一.代码实现:2个已经排序的列表,合并成一个列表并排序

### 二十二.思路,四则运算表达式实现思路

### 二十三.递归

### 二十四.python中的数据结构
