# centos7安装python3.6.1，pip3，配置默认虚拟环境
* 安装一下前置的文件
```Java
yum install openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel
yum install wget gcc make
```
* 安装 Python-3.6.1，pip3
* * 1.下载：wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz
* * 2.减压：tar -xzvf Python-3.6.1.tgz
* * 3.cd Python-3.6.1
* * 4../configure --prefix=/usr/local/python3.6.1  #指定安装路径
* * 5.make #编译
* * 6.make install #安装
* * 7.ln -s /usr/local/python3.6.1/bin/python3.6 /usr/bin/python3 #建立Python的软连接，指向Python-3.6.1
* * 8.ln -s /usr/local/python3.6.1/bin/pip3 /usr/bin/pip3 #建立pip3新的软连接，指向Python-3.6.1下面的bin

* 虚拟环境配置，python3默认带了虚拟环境
* * #TestVenv默认环境名称
* * 1.安装虚拟环境的文件夹：cd /home/pythonVenv	
* * 2.安装：python3 -m venv TestVenv
* * 3.开启虚拟环境：source /home/pythonVenv/TestVenv/bin/activate	    
* * 4.退出虚拟环境：deactivate

* 安装flask,gunicorn,防火墙添加端口
* * 1.安装flask：pip install flask
* * 2.安装gunicorn：pip install gunicorn
* * 3.添加防火墙端口8000： firewall-cmd --zone=public --add-port=8000/tcp --permanent
* * 4.重新载入：firewall-cmd --reload
* * 5.查看：firewall-cmd --zone=public --query-port=8000/tcp
* * 6.当前还在虚拟环境下面。
* * * 6.1 创建flask测试项目：touch /home/www/test/test.py，然后vi /home/www/test/test.py复制下面内容
```Java
from flask import Flask
app = Flask(__name__)
@app.route('/')
def index():
    return "Hello World! 123123"
```
* * * 6.2 gunicorn运行。此时就可以访问了
```Java
#gunicorn运行
gunicorn test:app
#设置8000端口监听，0.0.0.0：所有外网IP
gunicorn rocket:app -p rocket.pid -b 0.0.0.0:8000 -D
```
* * * 6.3 退出虚拟环境：deactivate，安装nginx，安装参考：https://www.cnblogs.com/tangjiansheng/p/6928722.html
配置就参考项目下面的default.conf
```Java
#检查配置：
nginx -t
#查看端口：
ss -tnl | grep 8000
```
