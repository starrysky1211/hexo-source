---
title: python_email
date: 2017-03-14 11:26:35
categories: 学习
tags: python
---
# 论如何使用python发一封写着自己IP地址的邮件

近来收到动态IP困扰，远程桌面使用的略不顺手，总是因为奇奇怪怪的ip改换导致连接失败。所以写个脚本用于读取本地IP并发送给自己的邮箱，方便你我他嗯。

## 思路
1. 读取IP
2. 生成邮件
3. 发送邮件
<!-- more -->
***

## 实践
### 读取IP
这一步倒是简单的很，windows的命令行有这样一条命令：`ipconfig`

这条命令是用于读取本地的实时IP，可以读取所有网卡（包括虚拟网卡的地址），因此不需要我再找什么模块或者插件了。

![](http://p1.bqimg.com/567571/b8e07bdbfd685259.png)

运行结果如上图所示，很不错，接下来就是调用subprocess模块进行操作啦。

#### 其实python执行系统命令总共有以下几种方式

1. `os.system('command') #没有返回值，可以用来关机什么的= =`
2.  还是使用os模块

	```
	result = os.open('command')
	res = result.read()
	for line in res.splitlines():
		print line
	# 读取命令结果并逐行输出
	
	```
3. 使用subprocess模块

	```
	p = subprocess.Popen('command', shell=True, stdout=subprocess.PIPE)
	out,err = p.communicate()
	for line in out.splitlines():
			print line
	# 读取命令结果并逐行输出
	```
4. 执行命令并获取返回值

	```
	output = commands.getstatusoutput('command')
	print output
	```
#### 使用一个文件来记录IP

这一步我们需要用到python的文件读写，还是很简单的，只需要把文件创建，写入，保存加进去就可以。

由于我无所谓ip是否有变化，所以并不需要使用文件读取功能：

```
#!usr/bin/python #指定系统运行的python版本
import subprocess

p = subprocess.Popen('command', shell=True, stdout=subprocess.PIPE)
out,err = p.communicate()
# 读取当前本地IP
i = open('C:\Users\starrysky\Desktop\ip_now.txt','w')
# 以写入的形式打开桌面上的ip_now.txt文件，如果不存在就进行创建。
for line in out.splitlines():
	inpu = line + '\n'
	i.write(inpu)
# 使用循环对文件写入命令读取结果
i.close() #关闭读取文件，释放内存
print ('file: ip_now.txt\'s changed! ')
```

****

### 发送邮件
读取到ip之后保存在文件中，我还想要把文件发送出去（其实也可以直接把ip作为邮件的body发出去，不过就失去了锻炼的意义啊= =）

#### 实现发送邮件功能

这里需要用到Python的email模块中的MIMEText和stmplib模块

代码如下：

```
# -*- coding: UTF-8 -*-
import smtplib
from email.mime.text import MIMEText

# 输入收件人列表、发送邮箱地址、发送邮箱密码
mail_to_list = ['sunny1231sunshine@163.com']
mail_host = "smtp.163.com"
mail_user = "1**********8"
mail_pass = "s********1"
mail_postfix = "163.com"

# 对上面的输入进行格式构建
def send_mail(to_list, sub, content):
    me = "<" + mail_user + "@" + mail_postfix + ">"
    msg = MIMEText(content, _subtype="plain")
    msg['Subject'] = sub
    msg['From'] = me
    msg['To'] = ";".join(to_list)

# 进行发送邮件的尝试，成功就输出done！，失败就输出failed！，并输出报错信息。
    try:
        server = smtplib.SMTP()
        server.connect(mail_host)
        server.login(mail_user, mail_pass)
        server.sendmail(me, to_list, msg.as_string())
        server.close()
        return True
    except Exception, e:
        print (str(e))
        return False
for i in range(1):
    if send_mail(mail_to_list, "宝宝宝宝快来看，么么哒～", "这是来自哥哥写的python脚本的邮件哦，爱你～（比心）"):
        print "done! "
    else:
        print "failed! "

```

代码里面自带粮食，请单身狗们自行寻找。

其实到这里我们已经可以把ipconfig的返回结果写成email的body进行发送了，不过没有梦想和咸鱼有什么分别呢（手动傲娇脸）

#### 实现附件功能

附件需要用到的是另外一个email的模块——MIMEMultipart，这代表要构建的邮件本身，然后添加MIMEText作为正文对象，MIMEBase作为附件对象。

因此，只有构造邮件的过程发生了变化，发送邮件的过程并没有变化，看起来并没有什么锻炼啊= =

然而并不是这样，官方文档里并没有写如何定义一个文件的maintype，我只能乱写一个用做测试（谁叫我测试用的文件瞎选了一个.yml的呢），其次就是附件头的定义，谁能告诉我什么叫做附件头啊？？

```
# -*- coding: UTF-8 -*-
import smtplib
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email.mime.multipart import MIMEMultipart


mail_to_list = ['starry_sky_@outlook.com']
mail_host = "smtp.163.com"
mail_user = "1*********8"
mail_pass = "s*********1"
mail_postfix = "163.com"


def send_mail(to_list, sub, content):
    me = "<" + mail_user + "@" + mail_postfix + ">"
    msg = MIMEMultipart()
    msg['Subject'] = sub
    msg['From'] = me
    msg['To'] = ";".join(to_list)

    body = MIMEText(content, "plain", 'utf-8')
    msg.attach(body)

    with open('/Users/starrysky/GitHub/hexo/_config.yml', 'rb') as f:
        mime = MIMEBase('file', 'yml', filename='_config.yml')

        mime.add_header('Content-Disposition', 'attachment', filename='_config.yml')
        mime.set_payload(f.read())
        mime['Content-Type'] = 'application/octet-stream'

        msg.attach(mime)

    try:
        server = smtplib.SMTP()
        server.connect(mail_host)
        server.login(mail_user, mail_pass)
        server.sendmail(me, to_list, msg.as_string())
        server.close()
        return True
    except Exception as e:
        print (str(e))
        return False


for i in range(1):
    if send_mail(mail_to_list, "text-mail", "有没有附件？"):
        print "done! "
    else:
        print "failed! "

```

效果如下图（不得不说iphone和MacBook共用剪贴板太舒服了）
![](http://i1.piimg.com/567571/1a220563c6ae2da2.png)

好啦，现在我们的邮件可以发送附件了（其实html形式的网页也是可以发送的，换汤不换药），接下来就是把两个部分结合在一起了。

### 结合——使用邮件发送IP文件。
这就没什么好解释的啦，废话不多说，直接上代码

```
# !usr/bin/python
# -*- coding: UTF-8 -*-

import subprocess
import smtplib
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email.mime.multipart import MIMEMultipart

p = subprocess.Popen('ipconfig', shell=True, stdout=subprocess.PIPE)
out, err = p.communicate()


i = open('C:\Users\starrysky\Desktop\ip_now.txt', 'w')
for line in out.splitlines():
    inpu = line + '\n'
    i.write(inpu)
i.close()
print ('file:ip_now.txt\'s changed')


mail_to_list = ['starry_sky_@outlook.com']
mail_host = "smtp.163.com"
mail_user = "1*********8"
mail_pass = "s*********1"
mail_postfix = "163.com"


def send_mail(to_list, sub, content):
    me = "<" + mail_user + "@" + mail_postfix + ">"
    msg = MIMEMultipart()
    msg['Subject'] = sub
    msg['From'] = me
    msg['To'] = ";".join(to_list)

    body = MIMEText(content, "plain", 'utf-8')
    msg.attach(body)

    with open('C:\Users\starrysky\Desktop\ip_now.txt', 'rb') as f:
        mime = MIMEBase('file', 'txt', filename='ip_now') 
        # 附件文件名的定义

        mime.add_header('Content-Disposition', 'attachment', filename='ip_now.txt')
        mime.set_payload(f.read())
        mime['Content-Type'] = 'application/octet-stream'

        msg.attach(mime)

    try:
        server = smtplib.SMTP()
        server.connect(mail_host)
        server.login(mail_user, mail_pass)
        server.sendmail(me, to_list, msg.as_string())
        server.close()
        return True
    except Exception as e:
        print (str(e))
        return False


for i in range(1):
    if send_mail(mail_to_list, "text-mail", "Is this my IP?"):
        print ("done! ")
    else:
        print ("failed! ")

```

效果如图所示：

![](http://p1.bpimg.com/567571/f3c8ad27bafec2c0.png)

完美啊哈哈哈。

好啦，今天到此为止。