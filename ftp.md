## 在oentos7上面安装ftp
### 账号密码登录后，查看系统版本
``` C
cat /etc/os-release
```
### 1.1 安装 VSFTPD
``` C
# 先检查是否安装
rpm -q vsftpd
# 没有就安装
yum install -y vsftpd
# 查看安装路径
whereis vsftpd
# 查看ftp服务状态
systemctl status vsftpd.service
# 删除ftp，查看版本号
rpm -qa | grep vsftpd
# 我的版本是vsftpd-3.0.2-22.el7.x86_64， rpm -e 进行删除
rpm -e vsftpd-3.0.2-22.el7.x86_64
# 删除相关配置文件
cd /etc
rm -rf vsftpd
```
##### Complete! 出现表示安装完成
### 1.2 启动 VSFTPD
``` C
# 启动
systemctl start vsftpd.service
# 监听端口
netstat -nltp | grep 21
# 开机启动
systemctl enable vsftpd.service
```
### 1.3 配置ftp文件，设置非匿名访问
``` C
# 编辑配置文件
vi /etc/vsftpd/vsftpd.conf
```
#### 需要更改的配置
``` C
# 把YES改成NO
anonymous_enable=NO
# 去掉前面的#
chroot_local_user=YES
chroot_list_user=YES
chroot_list_file=/home # 并且设置成访问路径
# 最后添加下面一行代码
allow_writeable_chroot=YES
# 然后重启
systemctl restart vsftpd.service
```
### 1.4 添加账户
``` C
# 添加用zaylor，-s表示不允许ssh登录，/sbin/nologin：不允许此用户登录系统，但可以登录FTP
useradd -s /sbin/nologin zaylor
passwd zaylor
# 输入密码
# 设置路径权限
chown -R zaylor /home/project
chown -R 755 /home/project
```
参考链接：https://blog.csdn.net/Han_Wen2015/article/details/76794842
链接涉及的不够全面，还参考了其他的。成功配置。
