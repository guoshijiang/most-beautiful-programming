
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

### 三.数据库索引原理

4.用登陆过程说下缓存机制

5.内存溢出的原因

6.进程跟线程的区别

7.redis,kafka,docker,bizflow在项目中主要作用是什么

8.写个nodejs文件查询查看功能

9.http跟https区别

10.selenium简介，主要作用

11.代码实现文件上传

12.代码实现读文件中某域名平均响应时间

13.代码实现两个有序列表的中间位置查询

14.linux命令，读日志文件中10万行记录，查询某字符串 重复出现次数最多的前三

15.清空表数据的命令，in是不是走索引

16.http请求全过程

17.Post发送的明文密码安全吗？http跟https的关系

18.数据库索引的作用

19.like是否走索引

20.代码实现:传参数的装饰器

21.代码实现:2个已经排序的列表,合并成一个列表并排序

22.思路,四则运算表达式实现思路

23.递归

24.python中的数据结构
