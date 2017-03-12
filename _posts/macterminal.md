---
title: macterminal
date: 2017-03-06 20:16:27
categories: 学习
tags: mac命令行
---
## 用来备忘mac命令行命令
1.终端自动补全的配置

打开终端，输入 : 

nano .inputrc

在文件里面写上：

set completion-ignore-case on
set show-all-if-ambiguous on
TAB: menu-complete

ctrl + o ,回车，重启终端，自动补全按tap键就ok。

<!-- more -->

2.常用命令

pwd　　　　　　     当前工作目录

cd（不加参数）　进root 

cd（folder）　　      进入文件夹

cd ..　　　　　　     上级目录

cd ~　　　　　　     返回root

cd -　　　　　　      返回上一个访问的目录

rm 文件名 　　　　  删除 

cat 文件名(|less)　    在终端下查看文件

ls　　　　　　　　  列出目录下所有文件

cp 文件名 目标目录　将文件拷贝到目标目录下

~代表root　　           如：~/Document/CPP2/

mkdiv　　　　　　   新建文件夹

g++ 源文件名　　　  编译源文件，产生a.out

./文件名     运行  例如：./a.out < 输入文件名 > 输出文件名

control+d　　　　　中断a.out运行

nano 　　　　　　   编写脚本语言　　ctrl+o存储

nano ....sh　　　　   打开

bash ....sh　　　　   运行脚本

echo "...$i..."　　　   输出语句

tar -zxf abc.tar.gz       tar文件解压

ssh root@192.168.1.222   以root账号远程连接222服务器

unrar x abc.rar           rar文件解压，需要安装rar工具

