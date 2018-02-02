# centos7安装python3.6.1，pip3，配置默认虚拟环境
* 安装一下前置的文件
```Java
yum install openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel
yum install wget gcc make
```
* 安装 
* * 1.下载：wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz
* * 2.减压：tar -xzvf Python-3.6.1.tgz
* * 3.cd Python-3.6.1
* * 4../configure --prefix=/usr/local/python3.6.1  #指定安装路径
* * 5.make #编译
* * 6.make install #安装
* * 7.ln -s /usr/local/python3.6.1/bin/python3.6 /usr/bin/python3 #建立Python的软连接，指向Python-3.6.1
* * 8.ln -s /usr/local/python3.6.1/bin/pip3 /usr/bin/pip3 #建立pip3新的软连接，指向Python-3.6.1下面的bin
