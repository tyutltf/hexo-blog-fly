---
title: pyechart使用
author: 雨轩恋
top: false
cover: false
toc: true
mathjax: false
date: 2019-03-19 11:01:15
img:
coverImg:
password:
summary:
    pyechart的简单使用
tags:
  - echart
categories:
  - 可视化
---

由于需要在项目中展示数据，查了查资料发现，pyecharts模块在网页数据展示方面有很大优势，所以就学了点pyechas

参考博客：

Python：数据可视化pyecharts的使用 - JYRoy - 博客园  http://www.cnblogs.com/jyroy/p/9446486.html
             
python可视化pyecharts - ting_163的博客 - CSDN博客  https://blog.csdn.net/ting_163/article/details/80896419?utm_source=blogxgwz0

两位大佬的博客都写的不错，学到了很多

最基本的柱状图：

```
from pyecharts import Bar
bar=Bar('我的第一个图表','副标题')
bar.add("服装",["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"],[5,20,36,10,75,90])
bar.show_config()
bar.render('柱状图.html')
```
运行结果：

![1](https://img2018.cnblogs.com/blog/1471003/201810/1471003-20181015211934891-1225587641.png)


词云图：
```
from pyecharts import WordCloud


name =['110', 'haihai', '鬼子', '豆腐', '旺旺', '南哥', '黑子', '两凡', '蒙多', '一哥', '小三', '末伏', '相大胖', '大路', '幺爸', '刘能', '刘瑞']
value =[10000, 6181, 4386, 4055, 2467, 2244, 1898, 1484, 1112, 965, 847, 582, 555, 550, 462, 366, 360]


wordcloud =WordCloud(width=1300, height=620)
wordcloud.add("", name, value, word_size_range=[30, 100], shape='')
#词云图轮廓，有'circle', 'cardioid', 'diamond', 'triangle-forward', 'triangle', 'pentagon', 'star'可选
#意思：圆，心形，钻石，三角形，三角形，五角大楼，星星
wordcloud.show_config()
wordcloud.render('回忆.html')
```
运行结果：

![1](https://img2018.cnblogs.com/blog/1471003/201810/1471003-20181015212458306-116916436.png)

还弄了一个比较好玩的：
```
from pyecharts import Map
value = [20,190,253,77,65,40,70,80,20,180,800]
attr = ['运城市', '临汾市', '太原市', '大同市', '忻州市','长治市','晋中市','吕梁市','晋城市','阳泉市','朔州市']
map = Map("山西地图示例", width=1200,height=600)
map.add("", attr, value, maptype='山西',
                is_visualmap=True,
                visual_text_color='#000',is_label_show=True)
map.render('山西.html')
```
运行结果：

![1](https://img2018.cnblogs.com/blog/1471003/201810/1471003-20181015212405397-587114063.png)

咳咳咳，接下来这个就，
```
from pyecharts import WordCloud

name =['世奇老狗', '老猥琐', '丰晋峰', '老狗逼', '老湿机', '草泥马', '阿伟', '牛牛', '嘤嘤嘤', '竹鼠商', '200GANA', '波多老师', '一柱擎天', '雪碧', '辣鸡', '渣渣', '落地成盒']
value =[10000, 6181, 4386, 4055, 2467, 2244, 1898, 1484, 1112, 965, 847, 582, 555, 550, 462, 366, 360]


wordcloud =WordCloud(width=1300, height=620)
wordcloud.add("", name, value, word_size_range=[30, 100], shape='pentagon')
#词云图轮廓，有'circle', 'cardioid', 'diamond', 'triangle-forward', 'triangle', 'pentagon', 'star'可选
#意思：圆，心形，钻石，三角形，三角形，五角大楼，星星
wordcloud.show_config()
wordcloud.render('世奇.html')
```
运行结果：

![1](https://img2018.cnblogs.com/blog/1471003/201810/1471003-20181015212705382-1087169515.png)

以上就是我对pyecharts的一些简单例子的使用，总的来说，pyecharts是一个很强大的模块

 