---
title: Python操作redis
author: 雨轩恋
top: false
cover: false
toc: true
mathjax: false
date: 2019-04-09 11:01:15
img:
coverImg:
password:
summary:
    python操作redis
tags:
  - redis
categories:
  - 数据库
---

### 介绍
redis是一个基于内存的高效的键值型非关系数据库，接下来我们就来看看这些操作是如何具体使用的吧

#### 数据库连接操作
```
from redis import StrictRedis

#数据库连接方式 因为就算我自己使用的，所有没有设置密码
redis=StrictRedis(host='localhost',port=6379,db=0,password=None)
#redis.set('age',20)
print(redis.get('name'))

print(redis.exists('name')) #是否存在name这个键

print(redis.type('name'))  #判断name的类型

print(redis.keys('n*'))  #获取所有以n开头的键

print(redis.randomkey())  #获取随机一个键

print(redis.dbsize()) #获取当前数据库中的键的数目
```


结果如下：

​![1](https://img-blog.csdnimg.cn/2018121216552372.PNG)

#### 字符串操作：

```
from redis import StrictRedis,ConnectionPool

#另一种连接方式
pool=ConnectionPool(host='localhost',port=6379,db=0,password=None)
redis=StrictRedis(connection_pool=pool)

#redis.set('name','Bob')
print(redis.get('name'))

#print(redis.getset('name','Mike'))  #赋值name为Mike并返回上一次的value

print(redis.mget(['name','age']))   #输出name键和age键的value

#print(redis.setnx('newname','james'))  #如果键值不存在，则赋值

#print(redis.mset({'name1':'smith','name2':'curry'}))  #批量赋值

#print(redis.msetnx({'name3':'ltf','name4':'lsq'}))    #不存在才批量赋值

#print(redis.incr('age',1))   #age对应的value 加1
#print(redis.decr('age',5))   #age对应的value 减5

#print(redis.append('name4','is a sb'))   #在name4的value后追加 is a sb 返回字符串长度

print(redis.substr('name',1,4))   #截取键 name
print(redis.getrange('name',0,-1))  #截取键 name

```


结果如下：

​![1](https://img-blog.csdnimg.cn/2018121216571096.PNG)

#### 列表操作

```
from redis import StrictRedis

redis=StrictRedis(host='localhost',port=6379,db=0,password=None)

#print(redis.rpush('list',1,2,3)) #向键名为list的列表尾部添加1,2,3 返回长度

#print(redis.lpush('list',0))   #向键名为list的列表头部添加0 返回长度

print(redis.llen('list'))   #返回列表的长度

print(redis.lrange('list',1,3))  #返回起始索引为1 终止索引为3的索引范围对应的列表

print(redis.lindex('list',1))   #返回索引为1的元素-value

#print(redis.lset('list',1,5))  #将list的列表索引为1的重新赋值为5

#print(redis.lpop('list'))  #删除list第一个元素

#print(redis.rpop('list'))   #删除list最后一个元素

#print(redis.blpop('list'))   #删除list第一个元素

#print(redis.brpop('list'))    #删除最后一个元素

print(redis.rpoplpush('list','list1'))   #删除list的尾元素并将其添加到list1的头部
```

运行结果如下：

![1​(https://img-blog.csdnimg.cn/20181212165818751.PNG)

#### 集合操作：

```
from redis import StrictRedis,ConnectionPool

pool=ConnectionPool(host='localhost',port=6379,db=0,password=None)
redis=StrictRedis(connection_pool=pool)

#print(redis.sadd('tags','Book','Tea','Coffee'))  #返回集合长度 3

#print(redis.srem('tags','Book'))  返回删除的数据个数

#print(redis.spop('tags'))   #随机删除并返回该元素

#print(redis.smove('tags','tags1','Coffee'))

print(redis.scard('tags'))  #获取tags集合的元素个数

print(redis.sismember('tags','Book'))   #判断Book是否在tags的集合中

print(redis.sinter('tags','tags1'))    #返回集合tags和集合tags1的交集

print(redis.sunion('tags','tags1'))    #返回集合tags和集合tags1的并集

print(redis.sdiff('tags','tags1'))     #返回集合tags和集合tags1的差集

print(redis.smembers('tags'))     #返回集合tags的所有元素

print(redis.srandmember('tags'))   #返回tags的一个随机元素
```


运行结果如下：

​![1](https://img-blog.csdnimg.cn/20181212165939322.PNG)

#### 哈希表操作：

```
from redis import StrictRedis,ConnectionPool

pool=ConnectionPool(host='localhost',port=6379,db=0,password=None)
redis=StrictRedis(connection_pool=pool)

#print(redis.hset('price','cake',5))  # 向键名为price的散列表添加映射关系，返回1 即添加的映射个数

#print(redis.hsetnx('price','book',6)) # 向键名为price的散列表添加映射关系，返回1 即添加的映射个数

print(redis.hget('price','cake'))  #获取键名为cake的值 返回5

#print(redis.hmset('price',{'banana':2,'apple':3,'pear':6,'orange':7}))   #批量添加映射

print(redis.hmget('price',['apple','orange']))   #查询apple和orange的值 输出 b'3',b'7'

#print(redis.hincrby('price','apple',3))   #apple映射加3 为6

print(redis.hexists('price','banana'))    #在price中banana是否存在  返回True

#print(redis.hdel('price','banana'))    #从price中删除banana 返回1

print(redis.hlen('price'))   #输出price的长度

print(redis.hkeys('price'))  #输出所有的映射键名

print(redis.hvals('price'))  #输出所有的映射键值

print(redis.hgetall('price'))  #输出所有的映射键对
```


运行结果如下：

​![1](https://img-blog.csdnimg.cn/20181212170044107.PNG)

还有一个是无序集合操作，不过我在实现这个操作的时候遇到了不可解决的问题。。

print(redis.zadd('price',100,'bob',98,'mike') 这句话遇到了莫名其妙的错误，，怎么也解决不了，希望有人可以帮我解决。。