---
title: jieba中文分词
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
    jieba中文分词加词云技术的使用
tags:
  - jieba
  - 分词
categories:
  - 词云
---

今日学习了python的词云技术
```
from os import path
from wordcloud import WordCloud
import matplotlib.pyplot as plt

d=path.dirname(__file__)
text=open(path.join(d,"data//constitution.txt")).read()

# 步骤3-2：设置一张词云图对象
wordcloud = WordCloud(background_color="white", max_font_size=40).generate(text)

# 步骤4-1：创建一个图表画布
plt.figure()
# 步骤4-2：设置图片
plt.imshow(wordcloud, interpolation="bilinear")
# 步骤4-3：取消图表x、y轴
plt.axis("off")
# 显示图片
plt.show()
```
结果如下：这是没有背景图的词云

![1](https://img2018.cnblogs.com/blog/1471003/201810/1471003-20181013094636318-1518808863.png)

接下来这个是爱丽丝漫游小说的词云

```
from os import path
from PIL import Image
import numpy as np
from wordcloud import WordCloud
import matplotlib.pyplot as plt

d=path.dirname(__file__)
text=open(path.join(d,"data//alice.txt")).read()
alice_mask = np.array(Image.open(path.join(d, "data/alice_mask.png")))

wordcloud=WordCloud(background_color="white",max_words=2000,mask=alice_mask)
wordcloud.generate(text)

wordcloud.to_file(path.join(d,"images//alice_word.png"))
```
用英文做词云很简单，不需要很麻烦的分词技术，用wordcloud模块就可以简单实现

运行结果如下

背景图：

![1](https://img2018.cnblogs.com/blog/1471003/201810/1471003-20181013095221225-704742962.png)

结果:

![1](https://img2018.cnblogs.com/blog/1471003/201810/1471003-20181013095152050-940671331.png)

最后是中文词云，中文词云就比较麻烦了，得用到jieba模块的分词技术，还得筛选

```
import jieba
from os import path  #用来获取文档的路径

#词云
from PIL import Image
import numpy as  np
import matplotlib.pyplot as plt
#词云生成工具
from wordcloud import WordCloud,ImageColorGenerator
#需要对中文进行处理
import matplotlib.font_manager as fm

#背景图
bg=np.array(Image.open("data/4.jpg"))

#获取当前的项目文件加的路径
d=path.dirname(__file__)
#读取停用词表
stopwords_path='data/alice.txt'
#添加需要自定以的分词
jieba.add_word("侯亮平")


#读取要分析的文本
text_path="data//sanguo.txt"
#读取要分析的文本，读取格式
text=open(path.join(d,text_path),encoding="utf8").read()

#定义个函数式用于分词
def jiebaclearText(text):
    #定义一个空的列表，将去除的停用词的分词保存
    mywordList=[]
    #进行分词
    seg_list=jieba.cut(text,cut_all=False)
    #将一个generator的内容用/连接
    listStr='/'.join(seg_list)
    #打开停用词表
    f_stop=open(stopwords_path,encoding="utf8")
    #读取
    try:
        f_stop_text=f_stop.read()
    finally:
        f_stop.close()#关闭资源
    #将停用词格式化，用\n分开，返回一个列表
    f_stop_seg_list=f_stop_text.split("\n")
    #对默认模式分词的进行遍历，去除停用词
    for myword in listStr.split('/'):
        #去除停用词
        if not(myword.split()) in f_stop_seg_list and len(myword.strip())>1:
            mywordList.append(myword)
    return ' '.join(mywordList)
text1=jiebaclearText(text)

#生成
wc=WordCloud(
    background_color="white",
    max_words=150,
    mask=bg,            #设置图片的背景
    max_font_size=60,
    random_state=42,
    font_path='C:/Windows/Fonts/simkai.ttf'   #中文处理，用系统自带的字体
    ).generate(text1)
#为图片设置字体
my_font=fm.FontProperties(fname='C:/Windows/Fonts/simkai.ttf')
#产生背景图片，基于彩色图像的颜色生成器
image_colors=ImageColorGenerator(bg)
#开始画图
plt.imshow(wc,interpolation="bilinear")
#为云图去掉坐标轴
plt.axis("off")
#画云图，显示
#plt.figure()
plt.show()
#为背景图去掉坐标轴
plt.axis("off")
plt.imshow(bg,cmap=plt.cm.gray)
#plt.show()

#保存云图
wc.to_file("data/sanguo.png")

```

运行结果：

![1](https://img2018.cnblogs.com/blog/1471003/201810/1471003-20181013095531710-1842021476.png)

可以看出，三国前20回里，吕布，曹操，玄德等词出现的最多