## 在oentos7上面对gunicron进行操作
### 安装相关的参考MD文件，下面说说其他的命令。本文的gunicorn安装在虚拟环境。所以先启动虚拟环境
``` C
# 启动虚拟环境
source /home/pythonVenv/TestVenv/bin/activate
# 安装psmisc，需要使用psmisc来看gunicorn的进程树
yum install psmisc
# 查看相关gunicorn的进程树
pstree -ap|grep gunicorn
# 删除命令,CD到*.pid文件
kill -HUP `cat rocket.pid`
kill `cat rocket.pid`
# 创建rocket.pid文件,监控8002端口，用80端口的不要急。这里用80会失败。一直提示找不到。知道原因的兄弟麻烦留言告诉我。
# run是flask的run文件
gunicorn run:app -p rocket.pid -b 127.0.0.1:8002 -D
gunicorn --bind 127.0.0.1:8002 run
# 这样gunicorn就运行成功了,通过下面命令可以查看
curl 127.0.0.1:8002
# 配置nginx
vi /etc/nginx/conf.d/default.conf
# 修改以下内容
server_name 127.0.0.1;  //显示的端口或者ip
location / {
    proxy_set_header Host $http_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_pass http://127.0.0.1:8002;   //监控8002的gunicorn
}
# 启动nginx
systemctl start nginx   
```
