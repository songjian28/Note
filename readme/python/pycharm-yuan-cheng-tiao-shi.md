# Pycharm 远程调试

远程调试的配置方法

**1、在远程计算机上安装pydevd模块**

首先，在本地开发环境的PyCharm安装路径中找到pycharm-debug.egg文件（若远程计算机运行的是Python3，则需要pycharm-debug-py3k.egg）；

然后，将pycharm-debug.egg文件拷贝至远程计算机，在远程计算机中将pycharm-debug.egg添加至引用路径，可以采用多种方式：

* 采用easy\_install pycharm-debug.egg命令进行安装（pip命令无法安装，只能使用easy\_install）
* 将pycharm-debug.egg添加至PYTHONPATH或sys.path: import sys; sys.path.append('/home/leo/app-dependancies/pycharm-debug.egg')
* 解压pycharm-debug.egg，将其中的pydev文件夹拷贝至远程应用程序目录下

最后，在远程计算机的Python命令行中输入import pydevd，若没有报错则说明pydevd模块安装成功。

**2、在本地开发环境的PyCharm中进行监听配置**

在PyCharm中配置说明如下：

* 【Run】->【Edit Configurations】
* 【Add New Configuration】->【Python Remote Debug】
* 填写Local host name和Port，其中Local host name指的是本机开发环境的IP地址，而Port则随便填写一个10000以上的即可；需要注意的是，由于远程计算机需要连接至本地开发环境，因此本地IP地址应该保证远程可以访问得到
* 【Apply】and【OK】

**3、在本地开发环境的PyCharm中配置Mapping映射**

**4、在远程计算机的应用程序中插入代码**

将如下代码插入至远程计算机的应用程序中。

import pydevd pydevd.settrace('100.84.48.156', port=31235, stdoutToServer=True, stderrToServer=True)

其中，IP地址和端口号要与PyCharm中的监听配置保持一致。

**5、在PyCharm中启动Debug Server**

【Run】->【Debug…】，选择刚创建的远程调试配置项，在Debug Console中会显示如下信息：

Starting debug server at port 31235 Waiting for process connection... Use the following code to connect to the debugger: import pydevd pydevd.settrace('100.84.48.156', port=31235, stdoutToServer=True, stderrToServer=True)

这说明Debug Server已经启动并处于监听状态。

**6、在远程计算机中启动应用程序**

在远程计算机中启动应用程序，当执行到pydevd.settrace语句时，便会与本地开发环境中的PyCharm建立通讯连接，接下来便可以在本地IDE中进行单步调试了。

需要注意的是，本地开发环境必须保证IP地址和端口号可从远程计算机访问得到，否则会无法建立连接。

```
{content}nbsp;telnet 100.84.48.156 31235
Trying 100.84.48.156...
telnet: Unable to connect to remote host: Connection refused
 
```

```
{content}nbsp;python devicedectector.py
Could not connect to 100.84.48.156: 31236
Traceback (most recent call last):
  File "/usr/local/lib/python2.7/dist-packages/pycharm-debug.egg/pydevd_comm.py", line 478, in StartClient
    s.connect((host, port))
  File "/usr/lib/python2.7/socket.py", line 224, in meth
    return getattr(self._sock,name)(*args)
error: [Errno 111] Connection refused
```
