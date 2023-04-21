# anaconda命令

1、查看conda中环境情况：

`conda env list`\
2、安装python环境（环境名称为my\_env）

`conda create -n my_env python`\
3、安装python环境，版本号为3.7

`conda create -n my_env python=3.7`\
如果输入以上两行命令出现错误，如An unexpected error has occurred. Conda has prepared the above report.可能原因是开了VPN，请关闭VPN（可能但不限于这种原因）

4、从base环境转到my\_env环境

`conda activate my_env`\
5、查看my\_env 环境python版本号

`python -V`\
6、安装包Biopython

`pip install Biopython`\


如果出现以上问题

`pip install Biopython --default-timeout=1000`

7、安装完成后，以下代码可以看到该环境下安装的库的情况

`conda list﻿​`
