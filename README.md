# centos7安装python3.6，pip，配置pipenv虚拟环境

* 1.登录步骤省略
* 2.安装3.6有2个方式
* * 1.源码安装
* * 2.直接安装RPM包。
* * * PS:参考链接   https://segmentfault.com/a/1190000009922582#articleHeader3
         参考最后的github地址直接安装。等待较久。
* * 3.需要说明部分。安装好的项目在/usr/local/python3.6/bin中，然后添加软链接
```Java
  ln -s /usr/local/python3.6/bin/python3 /user/bin/python3  这个安装python3后存在
  ls -s /usr/local/python3.6/bin/pip3 /user/bin/pip3  成功
```
