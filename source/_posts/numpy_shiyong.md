---
title: numpy数组的使用
author: 雨轩恋
top: false
cover: false
toc: true
mathjax: false
date: 2019-01-09 11:01:15
img:
coverImg:
password:
summary:
    numpy 模块的使用
tags:
  - 爬虫
  - 知乎
categories:
  - 爬虫
---


机器学习的最基础模块就是numpy模块了，而numpy模块中的数组操作又是重中之重，所以我们要把数组的各种方法弄得明明白白的，以下就是数组的一些常用方法

1.创建各种各样的数组：

```
import numpy as np
import matplotlib.pyplot as plt

print(np.zeros(10))  #一维全零数组
print(np.zeros((3,3),dtype=np.int))  #多维tupple数组  3行3列  可以加数据类型
print(np.ones(10))   #一维全1数组
print(np.ones((4,4)))   #多维全1数组
print(np.full((3,5),8))  #可以指定数组元素的值
print(np.identity(4))   #创建单位矩阵
print(np.eye(4,4,1))    #4行4列单位矩阵 对角线从下标1开始


print(np.array([1,23,4,'ltf','fjf']))   #可以随便传入数据  一维数组
print(np.array([[1,2,3],['ltf','lsq','fjf'],['男','女','人妖']]))   #多维数组，随便定义、

a=np.array([[1,2,3],[4,3,6]])
b=np.full_like(a,3.2)
c=np.ones_like(a)
print(b)
print(c)

#根据一个向量创建斜对角线方阵 也可以指定对角线位置
arr2d=np.diag([1,2,3,4])
print(arr2d)

print(np.arange(1,6))  #类似于range 不包含上界
print(np.arange(1,10,2))   #开始 结束 步长
print(np.linspace(1,10,4))  #开始 结束 个数
print(np.logspace(1,4,4))     #分为4个等分点，形成数组【1,2,3,4】然后形成 对数的底数的指数
print(np.logspace(1,5,5,base=2))  #指定对数为2


#创建坐标系 其实可以用plt.show()
x=np.linspace(0,1,5)
y=np.linspace(0,1,3)
xv,yv=np.meshgrid(x,y)
print(xv)
print(yv)
plt.plot(xv,yv,'^')
plt.show()


#指数图
x=np.arange(-5,5,0.1)
y=np.power(2,x)
#print(y)
plt.plot(x,y)
#对数图
x=np.power(2,x)
y=np.log2(x)
plt.plot(x,y)
plt.show()


x1=np.arange(1,5,1)
y1=np.power(x1,3)  #x1的3次方
print(y1)

x2=np.array([1,8,27,64])
y2=np.power(x2,1/3)  #x2的1/3次方
print(y2)
```

2.数组的复制等各种操作
```
import numpy as np


#1  赋值 改变原数组
a=np.array([1,2,3,4,5])
b=a
b[0]=100
print(b)
print(a)

#2 拷贝 不改变原数组
a1=np.array([1,2,3,4,5])
b1=np.copy(a1)
b1[0]=20
print(a1)
print(b1)

#3  修改
arry=np.array([1,2,3,4,5])
#arry[2]=10
arry[0:2]=8  #包头不包尾
print(arry)

arr1=np.array([[1,2,3,4],[5,6,7,8]])
print(arr1.T)  #数组的转置
arr1.shape=4,2
print(arr1)    #简单分隔

#4 分隔
arr2=np.arange(0,20,1)
print(arr2.reshape(4,5))
newarr2=arr2.reshape(4,5)
newarr2[0:2,0]=8  #0行1行 的0列 为8
print(newarr2)

#5
newarr3=np.reshape(newarr2,(1,-1))  #行数为1,  列数 待定
print(newarr3)
newarr4=np.reshape(newarr2,(-1,1))  #列数为1， 行数 待定
print(newarr4)

newarr5=newarr3[0][:,np.newaxis]   #取第一行 即一维数组 在变成一列
print(newarr5)


#6 二维数组转一维数组
arr2d=np.arange(1,21,1).reshape(4,5) #4行5列
print(arr2d)
arr2d1=np.ravel(arr2d)
print(arr2d1)  #arr2d1和arr2d共享同一块内存
print(arr2d.flatten())   #不共享内存

#7 resize使用
arrresize=np.resize(arr2d,(5,2))  #5行2列  本来有20个元素 只取其中的10个也可以 不像reshape必须全取
print(arrresize)

#8 转置  多维转换置换 
arr3d=np.arange(1,28,1).reshape(3,3,3)
print(arr3d)
arr3d1=np.transpose(arr3d)
print(arr3d1)
```
3.数组的修改等各种操作
```
import numpy as np


#1.访问二维数组
a=np.arange(1,16,1).reshape(3,5) #3行5列数组
print(a)
print(a[1])  #访问第一行
print(a[1,1])  #访问第一行第一列的元素
print(a[1][1])  #访问第一行第一列的元素

#2.访问二维数组部分元素
print('-'*20)
b=np.arange(1,16,1).reshape(3,5) #3行5列二维数组
print(b)
print(b[0:1,2:4]) #第一行下标为2和下标为3的元素
print(b[:,3])     #所有行下标为3的列数的所有元素
print(b[:,2:5])   #所有行，2,3,4列元素


#3.删除元素
print('-'*20)
c=np.arange(1,16,1).reshape(3,5) #3行5列二维数组
print(c)
print(np.delete(c,1))  #删除行号 返回一位数组
print(np.delete(c,[2,3,8,9]))  #返回一位数组 删除下标为2,3,8,9的元素

#4.删除列元素
print('-'*20)
d=np.arange(1,16,1).reshape(3,5) #3行5列二维数组
print(d)
print(np.delete(d,1,axis=0))  #删除下标为1这一行
print(np.delete(d,[2,3],axis=1))  #删除下标为2和3 的这两列


#5.插入元素
print('-'*20)
e=np.array([[1,2],[3,4],[5,6]])
print(e)
print(np.insert(e,1,5)) #返回一维数组 把5插入到1号索引后
print(np.insert(e,1,5,axis=1))  #插入一列 该列元素全为5
print(np.insert(e,1,[0,2,5],axis=1)) #插入一列 为0,2,5
print(np.insert(e,len(e),[[7,8]],axis=0))  #在最后一列插入一行
print(np.c_[e,np.array([1,1,1])]) #在最后一行后面加一列
print(np.append(e,[[7,8]],axis=0))  #append追加一列
```

4.数组的组合拼接等等
```
import numpy as np

#1.数组的行拼接
a=np.array([[1,2],[3,4]])
b=np.array([[5,6]])
c=np.concatenate((a,b),axis=0)  #axis=0 按行
d=np.vstack((a,b))  #行 方法
print(c)
print(d)

#2.数组的列拼接
a=np.array([[1,2],[3,4]])
b=np.array([[5],[6]])
c=np.concatenate((a,b),axis=1)  #axis=1 按列 要求具有同样的列数
d=np.hstack((a,b))  #列方法
print(c)
print(d)

#3.竖直方向将二维数组拆分成若干个数组
a=np.arange(1,21,1).reshape(4,5)
b=np.split(a,2)
c=np.vsplit(a,2)
print(b)
print(c)

#4.水平方向将二维数组拆分成若干个数组
a=np.arange(1,21,1).reshape(4,5)
b=np.hsplit(a,5)
print(b)
```
5.数组的查找，排序，统计
```
import numpy as np


#1.检查符合条件的元素
a=np.array([1,0,0,3,4,5,0,8])
b=np.nonzero(a)
print(b)  #不为0的下标
c=a[b]
print(c)  #输出不为0的元素 1,3,4,5,8

#2.二维数组查找
a=np.array([[1,2,0],[4,0,6],[0,8,9]])
b=np.nonzero(a)
c=a[b]
print(c)   #输出一维数组1,2,4,6,8,9

#3.查找指定条件
a=np.arange(10)
print(a)
b=np.where(a>5)
print(a[b])  #查找大于5的

#4.返回条件为true
a=np.arange(5)
b=np.array([True,False,True,True,False])
print(a[b]) #输出0,2,3
print(b[a])

#5.返回指定索引的若干个元素
a=np.array([4,3,5,7,6,8])
b=np.take(a,[0,1,4]) #返回索引为0,1,4的元素
print(b)


#5.数组排序
a=np.arange(5)
print(a[::-1])  #倒序，，-1指定步长为-1 倒数
b=np.array([3,4,1,8,4,9,5,6,9])
print(np.sort(b))  #一维数组排序

a=np.array([[3,1,5],[2,4,0]])
print(a)
b=np.sort(a,axis=0) #沿着行索引增加方向排序,也就是对每一列排序
print(b)
c=np.sort(a,axis=1) #沿着列索引增加方向排序,也就是对每一行排序
print(c)

#5.分界线排序
a=np.array([30,20,40,50,10,80,50,40,90,76])
b=np.partition(a,0)
print(b) #小于30的在左边 大于30的在右边 等于也在右边
c=np.partition(a,6)
print(c)  #小于50的在左边 大于50的在右边 等于也在右边

#6.数组统计
a=np.array([1,3,6,2,5,9,8,10,4])
print(a.max())  #最大值
print(np.max(a))  #最大值
print(np.min(a))  #最小值


a=np.arange(1,11,1).reshape(2,5) #2行5列2维数组
print(a)
print(np.max(a)) #所有元素里面的最大值
print(np.max(a,axis=0)) #行索引 找出每一列的最大值
print(np.max(a,axis=1)) #列索引 找出每一行的最大值

a=np.array([[1,3,9],[2,5,4],[6,7,8]])
print('-'*20)
print(np.max(a,axis=0)) #行索引 找出每一列的最大值
print(np.max(a,axis=1)) #列索引 找出每一行的最大值


#查找极值元素的索引
a=np.array([1,2,0,4,5,3,7,9])
print(np.argmax(a)) #索引号 7
print(np.argmin(a)) #索引号 2

a=np.array([[1,2,3],[6,5,4],[9,7,8]])  #3行3列
print(a)
print(np.argmax(a))
print(np.argmax(a,axis=0)) #每一列最大元素的索引
print(np.argmax(a,axis=1)) #每一行最大元素的索引

#计算数组平均值
a=np.arange(1,13,1).reshape(3,4)
print(a)
print(np.mean(a)) #输出 所有数的和的平均值
print(np.mean(a,axis=0)) #每一列的平均值
print(np.mean(a,axis=1)) #每一行的平均值

#计算数组加权平均值
a=np.arange(1,11)
print(a) #输出1-11的十个数
print(np.mean(a))  #没加权重
b=np.average(a,weights=np.array([1,3,1,0,0,1,1,0,1,2]))  #这是加了权重
print(b)
```
附上GitHub地址：

https://github.com/tyutltf/numpy_array_basic