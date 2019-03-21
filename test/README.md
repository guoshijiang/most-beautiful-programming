
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



### 四.用登陆过程说下缓存机制

cookie缓存

分布式session缓存 + 验证码

redis缓存 + 验证码

APP本地缓存

### 五.Python内存溢出的原因

内存中加载的数据量过于庞大
集合类中有对对象的引用，使用完后未清空，使得系统不能回收；
代码中存在死循环或循环产生过多重复的对象实体；
使用的第三方软件中的BUG；
启动参数设定的过小；

### 六.进程跟线程的区别

#### 1.进程

每个进程在内核中都有一个进程控制块（PCB）来维护进程相关的信息，Linux内核的进程控制块是task_struct结构体。/usr/src/linux-headers-3.16.0-30/include/linux/sched.h文件中可以查看struct task_struct 结构体定义。其内部成员有很多，主要的有下面这些：

* 进程id。系统中每个进程有唯一的id，在C语言中用pid_t类型表示，其实就是一个非负整数。
* 进程的状态，有就绪、运行、挂起、停止等状态。
* 进程切换时需要保存和恢复的一些CPU寄存器。
* 描述虚拟地址空间的信息。
* 描述控制终端的信息。
* 当前工作目录（Current Working Directory）。
* umask掩码。
* 文件描述符表，包含很多指向file结构体的指针。
* 和信号相关的信息。
* 用户id和组id。
* 会话（Session）和进程组。
* 进程可以使用的资源上限（Resource Limit）。

进程基本的状态有5种。分别为初始态，就绪态，运行态，挂起态与终止态。其中初始态为进程准备阶段，常与就绪态结合来看。

#### 2.线程

LWP：light weight process 轻量级的进程，本质仍是进程(在Linux环境下)

#### 3.线程和进程的区别

进程：独立地址空间，拥有PCB
线程：也有PCB，但没有独立的地址空间(共享)
区别：在于是否共享地址空间。独居(进程)；合租(线程)。

Linux下：
线程：最小的执行单位
进程：最小分配资源单位，可看成是只有一个线程的进程。

调度：线程作为调度和分配的基本单位，进程作为拥有资源的基本单位

并发性：不仅进程之间可以并发执行，同一个进程的多个线程之间也可并发执行

拥有资源：进程是拥有资源的一个独立单位，线程不拥有系统资源，但可以访问隶属于进程的资源.

系统开销：在创建或撤消进程时，由于系统都要为之分配和回收资源，导致系统的开销明显大于创建或撤消线程时的开销。

### 七.redis,kafka,docker,bizflow在项目中主要作用是什么

#### 1.redis

redis是一种支持Key-Value等多种数据结构的存储系统。可用于缓存、事件发布或订阅、高速队列等场景。该数据库使用ANSI C语言编写，支持网络，提供字符串、哈希、列表、队列、集合结构直接存取，基于内存，可持久化。

##### redis的数据类型

Redis一共支持五种数据类：string(字符串)、hash(哈希)、list(列表)、set(集合)和zset（sorted set 有序集合）。

##### redis在项目中的应用

1、会话缓存（最常用）
2、消息队列，比如支付
3、活动排行榜或计数
4、发布、订阅消息（消息通知）
5、商品列表、评论列表等

#### 2.kafka

Apache Kafka是分布式发布-订阅消息系统，在 kafka官网上对 kafka 的定义：一个分布式发布-订阅消息传递系统。 它最初由LinkedIn公司开发，Linkedin于2010年贡献给了Apache基金会并成为顶级开源项目。Kafka是一种快速、可扩展的、设计内在就是分布式的，分区的和可复制的提交日志服务。

##### Kafka基本架构

它的架构包括以下组件：
1、话题（Topic）：是特定类型的消息流。消息是字节的有效负载（Payload），话题是消息的分类名或种子（Feed）名；
2、生产者（Producer）：是能够发布消息到话题的任何对象；
3、服务代理（Broker）：已发布的消息保存在一组服务器中，它们被称为代理（Broker）或Kafka集群；
4、消费者（Consumer）：可以订阅一个或多个话题，并从Broker拉数据，从而消费这些已发布的消息；

##### Kafka主要应用

（1）日志收集：一个公司可以用Kafka可以收集各种服务的log，通过kafka以统一接口服务的方式开放给各种consumer，例如Hadoop、Hbase、Solr等；
（2）消息系统：解耦和生产者和消费者、缓存消息等；
（3）用户活动跟踪：Kafka经常被用来记录web用户或者app用户的各种活动，如浏览网页、搜索、点击等活动，这些活动信息被各个服务器发布到kafka的topic中，然后订阅者通过订阅这些topic来做实时的监控分析，或者装载到Hadoop、数据仓库中做离线分析和挖掘；
（4）运营指标：Kafka也经常用来记录运营监控数据。包括收集各种分布式应用的数据，生产各种操作的集中反馈，比如报警和报告；
（5）流式处理：比如spark streaming和storm；
（6）事件源；


#### 3.Docker

Docker是唯一一能够应对整个混合云中的每个应用的提供集装箱服务的平台。 现在很多企业面临着数字化转型的压力，受到现有应用程序和基础架构的制约，很难有很好的发展。而Docker合理利用日益多样化的云，数据中心和应用程序架构产品组合。 真正实现了应用程序和基础架构与开发人员和IT操作员之间的真正独立性，以释放他们的潜力并创建更好的协作和创新模式。

Docker是开发，运维和运行应用程序的开放平台。 Docker使您能够将应用程序与基础架构分开，以便您可以快速交付软件。 使用Docker，您可以像管理应用程序一样管理基础架构。 通过利用Docker的优点，快速进行运维，测试和部署代码，可以明显地缩短编写代码，以及在生产环境中运行代码之间的延迟的时间。真正实现与平台解耦合。

##### docker的主要应用

部署项目，一次部署，多平台可用

#### 4.bizflow
BizFlow 是一款优秀的工作流产品，整套产品包含工作流引擎，基于B/S的工作台，基于Eclipse的流程设计器，以及若干的扩展适配器可以让我们直接与其他现有应用平台无缝集成，而其JAVA/SOA的构建特性可以完全满足我们的跨平台，跨开发语言的需求。

分支实现是每个工作流必须的功能，BizFlow使用BPMN标准来描述流程，所以我们基本上看符号就知道某一个Activity代表何种业务规则，BizFlow的分支具体分为四种。

###### XOR Gateway（也称为Exclusive Gateway或单一分支）

XOR Gateway 的只允许一进一出，主要用来满足以下的业务需求：

1、多个流出路径，但仅有一个路径会被触发。当没有一个路径满足条件时，XOR Gateway可以指定触发一个默认路径。
2、多个流入路径，但仅有一个路径会被触发，最后会有一个路径流出。

###### OR Gateway （也称为Inclusive Gateway或多路分支）

OR Gateway 允许多进多出，主要用来满足以下的业务需求：

1、分离——流出时会被分离成满足条件的若干路径
2、合并——可将多个满足条件的流入路径合并为一个，OR Gateway 并不需要等待所有流入路径都满足条件，只要满足指定数量的条件（比如两个路径满足条件时）就可继续进行下面的路径。

###### AND Gateway（也称为Parallel Gateway或全部分支）

AND Gateway 允许多进多出，主要用来满足以下的业务需求：

1、分离——AND Gateway不需要设置满足条件，流出时自动被分离成若干路径
2、合并——AND Gateway会等待所有流入路径都满足条件后才将多个流入路径合并为一个

###### Complex Gateway

BPMN还包含了一个Complex Gateway定义，以满足之前的分支活动都无法满足的需求。

##### bizflow作用

Bizflow的工作流组件开发与功能测试


### 八.nodejs实现查找当前目录下得文件功能

    var fs = require('fs');
    var join = require('path').join;

    function getJsonFiles(jsonPath){
        let jsonFiles = [];
        function findJsonFile(path){
            let files = fs.readdirSync(path);
            files.forEach(function (item, index) {
                let fPath = join(path,item);
                let stat = fs.statSync(fPath);
                if(stat.isDirectory() === true) {
                    findJsonFile(fPath);
                }
                if (stat.isFile() === true) { 
                  jsonFiles.push(fPath);
                }
            });
        }
        findJsonFile(jsonPath);
        console.log(jsonFiles);
    }

    getJsonFiles("test");

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

    #!/usr/bin/env python
    # -*- coding:utf-8 -*-
    from flask import Flask,render_template, request, send_from_directory,jsonify, redirect
    import os
    # import sys
    # reload(sys)
    # sys.setdefaultencoding('utf-8')
    app = Flask(__name__)

    # ALLOWED_EXTENSTIONS = set(['png', 'jpg', 'jpeg', 'gif'])
    app.config['UPLOAD_FOLDER'] = os.getcwd()
    download_floder = app.config['UPLOAD_FOLDER'] + '/upload'

    def allow_file(filename):
        allow_list = ['png', 'PNG', 'jpg', 'doc', 'docx', 'txt', 'pdf', 'PDF', 'xls', 'rar', 'exe', 'md', 'zip'] 
        a = filename.split('.')[1]
        if a in allow_list:
            return True
        else:
            return False

    @app.route('/main')
    def home():
        return render_template('index.html')

    @app.route('/getlist')
    def getlist():
        file_url_list = []
        file_floder = app.config['UPLOAD_FOLDER'] + '/upload'
        file_list = os.listdir(file_floder)
        for filename in file_list:
            file_url = url_for('download',filename=filename)
            file_url_list.append(file_url)
        # print file_list
        return jsonify(file_list)

    @app.route('/download/<filename>')
    def download(filename):
        return send_from_directory(download_floder,filename, as_attachment=True)

    @app.route('/upload', methods=['POST', 'GET'])
    def upload():
        file = request.files['file']
        if not file:
            return render_template('index.html', status='null')
        # print type(file)
        if allow_file(file.filename):
            file.save(os.path.join(app.config['UPLOAD_FOLDER']+'/upload/', file.filename))
            return render_template('index.html', status='OK')
        else:
            return 'NO'

    if __name__ == '__main__':
        app.run(debug=True, host='0.0.0.0')

### 十二.代码实现读文件中某域名平均响应时间

### 十三. python代码实现两个有序列表的中间位置查询

    #!usr/bin/env python
    #encoding:utf-8

    import random
    def random_nums_genetor(max_value=1000, total=100):
      num_list=[]
      for i in range(total):
        num_list.append(random.randint(1,max_value))
      return num_list
    def find_two_list_mid_num(num_list1,num_list2):
      length1=len(num_list1)
      length2=len(num_list2)
      total=length1+length2
      if total%2==0:
        half=total/2-1
      else:
        half=total/2
      res_list=[]
      while len(num_list1) and len(num_list2):
        if num_list1[0]<num_list2[0]:
          res_list.append(num_list1.pop(0))
        else:
          res_list.append(num_list2.pop(0))
      if len(num_list1):
        res_list+=num_list1
      elif len(num_list2):
        res_list+=num_list2
      #print res_list
      print res_list[half]
      return res_list
    if __name__ == '__main__':
      print "test result："
      num_list1=[1,2,5,7,12,45,67,100]
      num_list2=[11,34,77,90]
      res_list=find_two_list_mid_num(num_list1,num_list2)
      print res_list[5]
      print '--------------------------------------------------------'
      num_list1=random_nums_genetor(max_value=1000, total=10)
      num_list2=random_nums_genetor(max_value=100, total=7)
      res_list=find_two_list_mid_num(num_list1, num_list2)
      print res_list[8]


### 十四.linux命令，读日志文件中10万行记录，查询某字符串 重复出现次数最多的前三

    cat log.log | sort | uniq -c | sort -k1,1nr | head -3


### 十五.清空表数据的命令，in是不是走索引

in 走索引了

### 十六.http请求全过程

1.在浏览器中输入URL。比如：www.baidu.com

2.浏览器解析域名：www.baidu.com为IP地址，先在浏览器DNS缓存中查找--->系统host文件中查找---->DNS服务查找

3.TCP三次握手，建立TCP链接

4.浏览器封装HTTP请求报文（HTTP请求信息）

5.TCP层封装TCP头报文（TCP或UDP，源端口号、目的端口号）

6.IP层封装IP头报文（源IP地址、目的IP地址）

7.MAC层封装MAC头报文（源MAC地址、目的MAC地址），该处的目的MAC地址，会通过其他协议获取到家庭路由器的MAC地址

8.浏览器发送请求包

9.家庭路由器接收到请求包后，解析MAC头部

10.解析IP头部，校验IP是否为自己IP

11.如果不是自己IP，则重新封装MAC头报文（源MAC地址、目的MAC地址）

12.下一个路由器再次进行该操作，一直到解析IP头不时发现自己的IP和IP头部的目的IP一样。上图中即负载均衡服务器

13.解析TCP头部，获取目的端口号

14.解析HTTP报文，查看是请求还是应答，还是数据包，并在对应端口号的进行中进行相应的处理

### 十七.Post发送的明文密码安全吗？http跟https的关系

不安全，不管是http还是https,Post发送的明文密码都有被抓包的的风险，https加密层位于http层和tcp层之间，https保证的是传输过程的保密性防篡改性， 所以抓到的http层的数据并没有加密。同理， 在后台接收端， 经历解密后， 到达http层的数据也是明文。 要注意， https不是对http报文进行加密， 而是对业务数据进行加密， 然后用http传输。

### 十八.数据库索引的作用

数据库索引是为了增加查询速度而对表字段附加的一种标识

### 十九.like是否走索引

后通配  走索引   
前通配 走全表

### 二十.代码实现:传参数的装饰器

    def title(show = ''):
        def printStar(func):
            def f(a, b):
                print(show,'------------------')
                return func(a, b)
            return f
        return printStar

    @title('add')
    def add(a, b):    
        return a + b

    @title('sub')
    def sub(a, b):    
        return a - b

    print(add(1, 1))

    print(sub(2, 1))

### 二十一.代码实现:2个已经排序的列表,合并成一个列表并排序

#### 方法一

    def merge_list(a,b):
        if not a:
            return b
        if not b:
            return a
        a_index = b_index = 0
        ret = list()
        while a_index < len(a) and b_index < len(b):
            if a[a_index] <= b[b_index]:
                ret.append(a[a_index])
                a_index += 1
            else:
                ret.append(b[b_index])
                b_index += 1
        if a_index < len(a):
            ret.extend(a[a_index:])
        if b_index < len(b):
            ret.extend(b[b_index:])
        return ret
    if __name__ == "__main__":

        #组合小文件
        lt1 = [1,8,12,13]
        lt2 = [5,8,17,28]
        lt3 = [1,90,98,99,100]
        res = merge_list(lt1,lt2)
        res1 = merge_list(res,lt3)
        print(res)
        print(res1)



如果是多个待排序的列表,采用方法二较好,借助reduce()函数

#### 方法二

    from functools import reduce
    lts = list()
    lts.append(lt1)
    lts.append(lt2)
    lts.append(lt3)
    res2 = reduce(merge_list,lts)
    print(res2)


### 二十二.四则运算表达式实现思路

#### 栈实现四则运算表达式的思路

思路：将输入的中缀表达式用栈转化为后缀表达式，再根据后缀表达式用栈实现运算。

中缀表达式：运算符位于运算数中间的表达式。如`1+2`，`3*4` 
后缀表达式：运算符位于运算数后的表达式。如`12+`，`34*`

有中缀，有后缀，当然也有前缀。将中缀转换成前缀表达式然后进行计算与转换成后缀其实完全类似，这里只介绍后者。
 
先介绍用栈将中缀表达式转换成后缀表达式 
1.建立两个栈 s1, s2. 
2.遍历表达式字符串 
3.若遇到数字，则直接压入s1 
4.若遇到运算符（包括括号） 
4.1.若s2为空，或s2栈顶为’(‘,则直接压入s2 
4.2.若运算符比s2栈顶的运算符优先级高，则直接压入s2 
4.3.若(1)(2)均不成立，则推出s2栈顶元素，将s2的栈顶元素压入s1，再回去进行(1)(2)两步骤 
5.若遇到’(‘,则直接压入s2 
6.若遇到‘)’,则将s2的元素推出并压入s1，直到s2栈顶出现’(‘,

根据后缀表达式计算 
1.建立一个栈s 
2.遍历后缀表达式字符串 
3.遇到数字，则直接压入s 
4.遇到运算符，则推出s的最上面两个数，根据运算符对两个数进行加减乘除，并将运算结果压回s 
5.遍历结束后，最终结果就在栈s顶。

#### 二叉树实现四则运算表达式的思路

一、目标：可以对输入的四则混合运算表达式进行分析，并求出其结果。程序须支持：整数及小数运算、支持加（+），减（-），乘（*），除（/），技术括号嵌套。

二、原理：表达式的分析过程可以看作三步，（1）分析出表达式中各个标记，包括数值、括号以及操作符，将这些标记按顺序存放起来；（2）根据步骤1所得的标记，根据四则运算规则将其转换成一棵语法树（二叉树）；（3）使用后序遍历步骤2所得语法树，按操作进行求值，得出最后结果。程序的整个核心在于语法树如何建立。

三、语法树的建立：
如：`10+(5+9)/3-7*3`可以解析得如下语法树：

.： 
    ![.： 
](https://github.com/guoshijiang/most-beautiful-programming/blob/master/Image/2.png)


使用后序遍历方式对语法树进行遍历，可以得出其值; 
尽管上面的语法树是正确的，构建上面的语法树却不是那么简单，因为在此过程中，我们需要考虑：如何使得一对括号内的数值作为一个整体优先被计算？ 如果只是按操作符的优先级进行比较，那么我们很可能得出错误的结论。比如上述的表达式换成“`10+（5+9）+7*3`”，在构建完“`10+（5+9）+`”的语法树后，此时所得的树根是“10+（”中的“+”，它的运算优先级比“7*3”中的“*”的优先级要低，如果只是按照运算符优先级规则，我们很可能得一棵错误的语法树！因此，我们要简化对问题的思考方式，如何将一个有括号的表达式转换成一个没有括号的表达式，这样，我们只须考虑操作符的优先级就可以创建正确的语法树了！方法很简单，我们首先将没有嵌套的括号内的表达式进行解析，然后对它求值，将其结果作为一个数值结点替换原来的括号表达式，如果括号外部有括号，则按上述方法重复进行，直到去掉所有括号为止。如上面的“`10+（5+9）/3+（7*3）`”可以转换成：“`10+14/3+21`”，这样就很容易创建语法表达式了。


### 二十三.递归

递归，就是在运行的过程中调用自己。在数学和计算机科学中，递归指由一种（或多种）简单的基本情况定义的一类对象或方法，并规定其他所有情况都能被还原为其基本情况。

构成递归需具备的条件：

1. 子问题须与原始问题为同样的事，且更为简单；

2. 不能无限制地调用本身，须有个出口，化简为非递归状况处理。

#### 递归算法一般用于解决三类问题：

(1)数据的定义是按递归定义的。（Fibonacci函数）

(2)问题解法按递归算法实现。

这类问题虽则本身没有明显的递归结构，但用递归求解比迭代求解更简单，如Hanoi问题。

(3)数据的结构形式是按递归定义的。

如二叉树、广义表等，由于结构本身固有的递归特性，则它们的操作可递归地描述。

#### 递归的缺点：

递归算法解题相对常用的算法如普通循环等，运行效率较低。因此，应该尽量避免使用递归，除非没有更好的算法或者某种特定情况，递归更为适合的时候。在递归调用的过程当中系统为每一层的返回点、局部量等开辟了栈来存储。递归次数过多容易造成栈溢出等。

#### 递归典型问题： 梵塔问题（汉诺塔问题）

已知有三根针分别用A, B, C表示，在A中从上到下依次放n个从小到大的盘子，现要求把所有的盘子从A针全部移到B针，移动规则是：可以使用C临时存放盘子，每次只能移动一块盘子，而且每根针上不能出现大盘压小盘，找出移动次数最小的方案.

### 二十四.python中的数据结构

列表list、元组tuple、字典dict、集合set
