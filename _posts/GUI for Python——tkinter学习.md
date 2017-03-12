---
title: GUI for Python——tkinter学习笔记（一）
date: 2017-03-05 15:03:23
tags: [随笔,学习]
categories: 学习
---
# 为什么要学习GUI
当然是为了我家可爱的宝宝啊，趁着女生节来袭，给宝宝写一个逗她开心的小程序来，结合我最近在入门的Python，果断写了一个小时钟。

只有命令行，没有GUI的程序十分简单，经过了3天的学习我就已经看不下去源代码了，然而懒得改，如下：

### 命令行小时钟代码：
```
#\21天学通Python\
import time
one = ('   |','   |','   |','   |','   |')
two = ('||||','   |','||||','|   ','||||')
thr = ('||||','   |','||||','   |','||||')
fou = ('  ||',' | |','||||','   |','   |')
fiv = ('||||','|   ','||||','   |','||||')
six = ('||||','|   ','||||','|  |','||||')
sev = ('||||','   |','   |','   |','   |')
eig = ('||||','|  |','||||','|  |','||||')
nin = ('||||','|  |','||||','   |','||||')
zer = ('||||','|  |','|  |','|  |','||||')
number = (zer,one,two,thr,fou,fiv,six,sev,eig,nin)
def printnum(num = [0,0]):
    #将数字拼合输出 两个数字中间存在一列空格
    for i in range(10) :
        if num[0] == i :
            c1 = number[i]
        if num[1] == i :
            c10 = number[i]
    numlist = [c10[0]+' '+c1[0],c10[1]+' '+c1[1],c10[2]+' '+c1[2],c10[3]+' '+c1[3],c10[4]+' '+c1[4]]
    return numlist
def splitnum(num):
    a = num
    if a >100 :
        print ('invilid num')
    else:
        a1 = a%10
        a2 = (a-a%10)%100/10
    A = [a1,a2]
    return A
def gettime() :
    t = time.localtime(time.time())
    nt = [t.tm_hour,t.tm_min,t.tm_sec]
    return nt
while(1):
    nt = gettime()
    ntpr = [printnum(splitnum(nt[0])),printnum(splitnum(nt[1])),printnum(splitnum(nt[2]))]
    timelist = [ntpr[0][0]+'    '+ntpr[1][0]+'    '+ntpr[2][0],ntpr[0][1]+' -- '+ntpr[1][1]+' -- '+ntpr[2][1],ntpr[0][2]+'    '+ntpr[1][2]+'    '+ntpr[2][2],ntpr[0][3]+' -- '+ntpr[1][3]+' -- '+ntpr[2][3],ntpr[0][4]+'    '+ntpr[1][4]+'    '+ntpr[2][4]]
    print ('\n',timelist[0],timelist[1],timelist[2],timelist[3],timelist[4],sep = '\n')
    time.sleep(1)
```
嗯，确实麻烦到家了= 。=

<!--more-->

GitHub地址如下：
`
https://github.com/starrysky1211/python-in-mac.git
`

然后 `cd python-in-mac/python-practice/print-the-num.py`就可以用IDE运行了。

运行后可以看到效果比较鬼畜，因此我觉得GUI的学习势在必行啊。于是翻开了《21天学通Python》，看到了tkinter的入门教程。

#开始入门
首先就是打开窗口添加基本元素啦。第一个教程教会我如何添加标签（label）和按钮（button）

```
# -*- coding:utf-8 -*-
import tkinter
root = tkinter.Tk()
label = tkinter.Label(root, text = 'hello, tkinter!')
label.pack()
button1 = tkinter.Button(root, text = 'button1')
button2 = tkinter.Button(root, text = 'button2')
button1.pack(side = tkinter.LEFT)
button2.pack(side = tkinter.RIGHT)
root.mainloop()
```
效果就是这样：

![](http://p1.bpimg.com/567571/578f182918651174.png)

虽然简陋了一些，但是它可是我第一次用Python打开一个小窗口啊！

上面代码中，没有特意明确的指定两个按钮以及标签的位置，所以就默认以合适的方式排列了。
据说这玩意还可以定制，不过我暂时不尝试啦。

图书馆奏响回家的音乐啦，我要回寝室阅读啦，明天再见：）