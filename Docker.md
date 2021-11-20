# Dockerfile关键字描述

FROM -- 基础镜像，当前新镜像是基于哪个镜像的

MAINTAINER	-- 镜像维护者的姓名和邮箱地址

RUN -- 容器构建时需要运行的命令

EXPOSE -- 当前容器对外暴露出的端口

WORLDIR -- 指定在创建容器后，终端默认登陆的进来工作目录，一个落脚点

ENV -- 用来构建镜像过程中设置环境变量

ADD -- 将宿主机目录下的文件拷贝进镜像且ADD命令会自动处理URL和解压tar压缩包

COPY -- 类似ADD，拷贝文件和目录到镜像中。将从构建上下文目录中<源路径>的文件/目录复制到新的一层的镜像内的<目标路径>位置

VOLUME -- 容器数据卷，用于数据保存和持久化工作

CMD --指定一个容器启动时要运行的命令。Dockerfile中可以有多个CMD指令，但只有最后一个生效，CMD会被docker run之后的参数替换。

ENTRYPOINT	--指定一个容器启动时要运行的命令。 ENTRYPOINT的目的和CMD一样，都是在指定容器启动程序及参数

ONBUILD --当构建一个被继承的Dockerfile时运行命令，父镜像在被子继承后父镜像的onbuild被触发

#  Docker自定义PHP镜像



### 1、获取一个centos镜像作为基础镜像,我这里安装的是centos7
```
docker pull centos:7

docker run --net host -itd --name nginx centos:7 bash
```
(注意以下需要联网安装nginx、php，所以需要加入--net:host)


### 2、进入centos的镜像
```
docker exec -it 镜像id bash
```
#### 用yum安装以下内容：
```
yum install -y wget gcc gcc-c++ make openssl-devel
```
#### 并下载以下内容：
```
cd /usr/local/src
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo

wget ftp://ftp.pcre.org/pub/pcre//pcre-8.39.tar.gz
wget https://www.php.net/distributions/php-8.0.0.tar.gz
wget http://nginx.org/download/nginx-1.18.0.tar.gz
```
### 3、更新yum源
```
yum update
```

### 4、解压源码包后并删除，建议删除，删除的目的是不要让最后的镜像过于的大；
```
tar xf nginx-1.18.0.tar.gz
tar xf php-8.0.0.tar.gz
tar xf pcre-8.39.tar.gz
rm -f nginx-1.18.0.tar.gz php-8.0.0.tar.gz pcre-8.39.tar.gz
```

### 5、编译安装nginx：
#### 1）创建nginx用户
```
groupadd -r www
useradd -r -g www www
```
#### 2）编译安装nginx
```
cd nginx-1.18.0

./configure --prefix=/usr/local/nginx --user=www --group=www --with-http_ssl_module --with-http_stub_status_module --with-pcre=/usr/local/src/pcre-8.39

make && make install
```
#在nginx的配置文件里加上这一行很关键，这样nginx可以在docker启动的时候在后台运行！
```
echo "daemon off;" >> /usr/local/nginx/conf/nginx.conf
```

#### 3）测试nginx启动
修改nginx.conf；这个可以参考各种网上的资料；下面会给一个例子
```
/usr/local/nginx/sbin/nginx -t     #检查没配置文件
/usr/local/nginx/sbin/nginx         #启动nginx
```
### 8、编译安装php
#### 1）准备php的依赖包
```
yum install -y bison bison-devel zlib-devel libmcrypt-devel mcrypt mhash-devel libxml2-devel libcurl-devel bzip2-devel readline-devel libedit-devel libjpeg libpng freetype libjpeg-devel libpng-devel freetype-devel bzip2-devel curl-devel sqlite-devel libc-client-devel libxslt-devel
```
#### 2）编译安装php，如果过程中报错，提示缺少什么安装包，就用yum安装。
```
cd php-8.0.0

./configure --prefix=/usr/local/php --with-zlib-dir --with-freetype-dir --enable-mbstring --with-libxml-dir=/usr/local/libxml --enable-soap --enable-calendar --with-curl --with-mcrypt --with-zlib --with-gd  --disable-rpath --enable-inline-optimization --with-bz2 --with-zlib --enable-sockets --enable-sysvsem --enable-sysvshm --enable-pcntl --enable-mbregex --enable-exif --enable-bcmath --with-mhash --enable-zip --with-pcre-regex --with-mysql --with-pdo-mysql --with-mysqli --with-jpeg-dir=/usr/local/libjpeg --with-png-dir=/usr/local/libpng --enable-gd-native-ttf --with-openssl --with-fpm-user=www --with-fpm-group=www --with-libdir=lib64 --enable-ftp --with-imap --with-imap-ssl --with-kerberos --with-gettext --with-xmlrpc --with-xsl --enable-opcache --enable-fpm --enable-xml --enable-shmop --enable-session --enable-ctype --with-iconv-dir --with-iconv

make && make install
```
#### 3）配置环境变量
```
vim /etc/profile
```
如果提示没有vim这个命令，则安装 或者用vi
yum install -y vim*
添加到最后
```
PATH=$PATH:/usr/local/php/bin
export PATH
```
#### 更新环境变量
```
source /etc/profile
```
#### 查看版本
```
php -v
```
#### 4)准备php配置文件
```
cp php.ini-production /etc/php.ini
cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf
cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf
cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
chmod +x /etc/init.d/php-fpm
```
#### 启动php-fpm
```
/etc/init.d/php-fpm start
```
或者
```
service php-fpm start
```
##### 查看php-fpm是否启动
ps -ef|grep php

重启php-fpm服务
/etc/init.d/php-fpm restart

#### 5）修改php-fpm.conf配置文件
跟nginx里加一行的效果一样，为了启动docker时，php可以在后台运行
;daemonize = yes的注释去掉，并把yes改为no
为了同一个用户可以访问web的权限统一修改为www（宿主的web文件访问权限也是www）
修改为user=www group=www

#### 6) 开始在 PHP 中使用 Redis 前，我们需要确保已经安装了redis服务，且你的机器上能正常使用PHP。 接下来让我们安装 PHP redis 驱动，下载地址为:https://github.com/phpredis/phpredis/releases。
```
cd /usr/local/src

wget https://github.com/phpredis/phpredis/archive/5.3.2.tar.gz
tar -zxvf 5.3.2.tar.gz
cd phpredis-5.3.2
/usr/local/php/bin/phpize              # php安装后的路径
./configure --with-php-config=/usr/local/php/bin/php-config
make && make install
```
如果执行phpize时报错： Cannot find autoconf. Please check your autoconf installation and the $PHP_AUTOCONF environment variable. Then, rerun this script.


安装依赖 autoconf
```yum -y install autoconf```

将redis.so添加到php.ini中
```
echo 'extension=redis.so' >> /usr/local/php/etc/php.ini
```
/usr/local/php/etc/php.ini 就是你PHP 指向的php.ini路径，不懂可以
```php –ini``` 查看
重启php-fpm服务
```/etc/init.d/php-fpm restart```

查看redis扩展是否安装成功

```php -m | grep redis```
输出redis就是代表安装成功

测试:
vim testRedis.php
```
<?php
    //连接本地的 Redis 服务
   $redis = new \Redis();
   $redis->connect('127.0.0.1', 6379);
   $redis->auth('连接密码');
   echo "Connection to server sucessfully";
   //查看服务是否运行
   echo "Server is running: " . $redis->ping();
```
保存退出
php testRedis.php
出现以下内容代表成功连接
Connection to server sucessfullyServer is running: 1

#### 7)安装swoole依赖
```
cd /usr/local/src
curl -o ./swoole.tar.gz https://github.com/swoole/swoole-src/archive/master.tar.gz -L
tar zxvf swoole.tar.gz
mv ./swoole-src-master /usr/local/swoole
cd /usr/local/swoole
phpize
./configure --enable-openssl --enable-http2
make && sudo make install
```
最后，编译安装成功后，修改 php.ini 加入
```extension=swoole.so```
最后，php-m查看是否已安装成功

### 9、创建镜像
退出容器
```
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```
-a :提交的镜像作者；

-c :使用Dockerfile指令来创建镜像；

-m :提交时的说明文字；

-p :在commit时，将容器暂停。****