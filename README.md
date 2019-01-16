#nginx

debian7 / 8/9安装稳定版nginx

Debian版本代号分别为5.0的 lenny，6.0的 squeeze ，7.0的 wheezy 和8.0的 jessie，至于还没发布的9.0则为 stretch，你只需要根据你使用的版本更换对应的版本代号即可
编辑 /etc/apt/sources.list ，添加以下两行：（注意代号前后都有空格）

deb http://nginx.org/packages/debian/ 版本代号 nginx

deb-src http://nginx.org/packages/debian/ 版本代号 nginx

例如 Debian 7.0 即为：

deb http://nginx.org/packages/debian/ wheezy nginx

deb-src http://nginx.org/packages/debian/ wheezy nginx

而Debian 8.0 就变成

deb http://nginx.org/packages/debian/ jessie nginx

deb-src http://nginx.org/packages/debian/ jessie nginx

除了使用VIM编辑器添加之外，还可以使用echo命令导入：

echo deb http://nginx.org/packages/debian/ wheezy nginx >> /etc/apt/sources.list

echo deb-src http://nginx.org/packages/debian/ wheezy nginx >> /etc/apt/sources.list


然后，还需要更新并导入升级Key，否则无法使用；

wget http://nginx.org/keys/nginx_signing.key && apt-key add nginx_signing.key && apt-get update && apt-get install nginx

现在，终于安装使用上最新的Nginx了。

centos7安装最新nginx
-----
下载对应当前系统版本的nginx包(package)

wget  http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

建立nginx的yum仓库

rpm -ivh nginx-release-centos-7-0.el7.ngx.noarch.rpm

下载并安装nginx

yum install nginx

启动nginx服务

systemctl start nginx

配置:默认的配置文件在 /etc/nginx 路径下，使用该配置已经可以正确地运行nginx；如需要自定义，修改其下的 nginx.conf 等文件即可。

nginx的另外配置：https://www.srgb.xyz/2018/09/02/nginx_rewrite/

nginx Failed to read PID from file /run/nginx.pid: Invalid argument 解决方法：
`````
mkdir -p /etc/systemd/system/nginx.service.d 
printf "[Service]\nExecStartPost=/bin/sleep 0.1\n" > /etc/systemd/system/nginx.service.d/override.conf 
````````
然后 
``````
systemctl daemon-reload 
systemctl restart nginx.service
``````````

nginx1.12.2版本的安装方法：
``````
rpm --import https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7
rpm -ivh  https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```````
或者
```````
rpm -Uvh  https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
`````````
安装nginx
`````
yum -y install nginx
````````
从中下载最新的epel-release rpm
```````
http://dl.fedoraproject.org/pub/epel/7/x86_64/
`````````
安装epel-release rpm：
`````
# rpm -Uvh epel-release*rpm
`````
安装nginx rpm包：
`````
# yum install nginx
``````
或者进入目录下载需要的版本（见安装1.8.1的安装说明）

安装1.4.2版本：
``````
rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
```````
或者
``````
rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
```````
然后进入下载目录选择需要的版本安装，如：安装1.8.1版本：
`````
yum install -y http://nginx.org/packages/centos/7/x86_64/RPMS/nginx-1.8.1-1.el7.ngx.x86_64.rpm
````````
