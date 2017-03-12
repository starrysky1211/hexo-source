---
title: 在next主题中使用algolia服务
date: 2017-03-07 21:01:06
categories: 学习
tags: Hexo
---
# algolia 插件使用技巧
### 前情提要
博客里没有搜索总会觉得怪怪的，所以就果断把鼠标朝向了度娘。

刚开始看到的方式都是关于swiftype的，但是。。

<!-- more -->

<table><tr><td bgcolor = #00ffff>swiftype不能注册啊！！</td></tr></table>

一定是我的智商跟不上众位大神的脚步，只能曲线救国了:)

经过一番探查，找到了另外一个法国的公司提供的服务，algolia。

据说还比swiftype更快呢(暗自窃喜)。

于是就愉快的开始了接下来的工作。
****
### 注册
[algolia](https://www.algolia.com/users/sign_in)注册点击这里就可以，直接用邮箱就可以注册，还可以GitHub登陆，爽飞啦！

登陆后会有一个新手引导，全英文界面，想看就看也挺好玩的，不想看就直接右上角叉掉。

![](http://i1.piimg.com/567571/0ee635676596058d.png)

上面就是我们的index界面（indices），右边可以rename你的index，这个名字可以改一下，方便记住，一会还要用。

然后再左边看一看你的API keys，里面有：

1. Application ID. 
2. Search-only API key. 
3. monitoring API key. 
4. Admin API key. 

第1、2、4个是要用的，一会可以直接点击复制。

这时注册工作已经完成啦。

### 配置
打开命令行，cd到你的hexo根目录，然后运行：

```
npm install hexo-algolia --save
```
接着在根目录的_config.yml中添加：

```
algolia:
  applicationID: 'your application ID'
  apiKey: 'your search-only api Key'
  adminApiKey: 'your admin Api Key'
  indexName: 'your index Name'
  chunkSize: 5000
```
然后在hexo根目录运行：

```
hexo algolia
```
就完成了和algolia的通信。

接下来在next主题中进行配置。

```
cd themes/next/
vim _config.yml
```
这样就用vim打开了主题配置文件。如果不会用vim，也可以用别的编辑器打开，使用":q"就可以退出vim。接下来我以vim为例进行讲解。

然后我们要找到algolia的设置，next主题自带，不需要很麻烦，其他主题出门左转谷歌度娘不送。

```
/algolia "按回车键
```
就能够看到需要设置的位置了。

使用上下左右键将光标移到“False”上，i键进入编辑模式，删除掉，改成“true”，按`esc键`退回普通模式，输入`:wq`就编辑成功啦。

接下来不要忘记在hexo根目录进行

```
hexo clean
hexo g -d
```
就可以在自己的博客菜单栏看到搜索框啦，快去体验吧。
![](http://p1.bpimg.com/567571/47cbc2dbe28e7aaa.png)