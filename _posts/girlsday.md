---
title: 女生节狗粮已送到·十万火急
date: 2017-03-07 07:56:19
categories: 学习
tags: 
- 学习
- Python
---
# 深夜请自行取食
***

## GUI for Python ——tkinter学习笔记（二）

前情提要请看：


[GUI for Python ——tkinter学习笔记（一）](https://starrysky1211.github.io/2017/03/05/GUI%20for%20Python%E2%80%94%E2%80%94tkinter%E5%AD%A6%E4%B9%A0/)

今天已经是女生节了啊，我的礼物距离完工还遥遥无期

## 怎么办！！


爬起来一大早趁着宝宝没睡醒接着学习一个。

<!-- more -->

上面说到可以定制位置，这需要用到布局组件（grad方法和place方法，或者直接在pack中添加传递参数）

1. after
2. anchor： 对齐（n/top s/foot w/left e/right）
3. before
4. side: 主窗口（top bottom rignt left）
5. column：列起始
6. columnspam：列宽
7. row： 行起始
8. rowspam： 行宽

那组件们除了按钮还有什么呢：

- 单选、复选框
- 文本框
- 图形组件（Canvas）
- 菜单
- 标签
- ...

什么叫做应有尽有，不外如是了（反正我又没有优化UI的野心，不需要太好看（捂脸逃～））

于是开始了我的礼物大业，虽然有这么多的东西，但是不能迷失初心，先做一个只能显示时间的小窗口出来，正好练练手。

那先做一下规划吧，我的UI要做成什么样子呢？

![](http://p1.bqimg.com/567571/bc471770891f3746.png)

嗯，挺美的。：）

行，看起来还不错（？），那就做吧。

首先肯定是初始化一个tk界面了，然后就要好好想一下，应该用图形框还是应该用文本框来搞这个事情。
感觉文本框成本低一些啊，那就文本框吧。

在组件列表里，看到单行文本框：Entry，可以很好的开始。

写了一半才发现，文本框是用来读取用户输入的= =，很好，我们再找一个别的。



### 标签

这个好，提供在窗口显示文本的组件，甚至可以显示图片。

连后期优化都可以有了。搞。

```
# -*- coding:utf-8 -*-
import sys
from tkinter import *
import time

def gettime():
    global time1
    time2 = time.strftime('%H:%M:%S')
    if (time1 != time2):
        time1 = time2
        clock.config(text = time1)
    clock.after(200,gettime)

root = Tk()
time1 = ' '
clock = Label(root,
        font = ('times' ,20 ,'bold'),
        bg = 'blue')
clock.grid(row = 0, column = 1)
gettime()

root.mainloop()
```

效果如图所示：

![](http://p1.bpimg.com/567571/d42fbb2759115c6a.gif)

还是可以的（对不起我眼睛瞎）我的小目标已经达成啦。

下期再见。

