---
title: Ubuntu 14.04下源码安装 Nginx 和 PHP5
date: 2016-06-06
tags: [PHP, Nginx] 
categories: PHP
---

### 源码编译安装 Nginx
1. 安装依赖
```shell
sudo apt-get install libpcre3 libpcre3-dev zlib1g-dev libssl-dev build-essential
```
2. 下载并解压 Nginx 源码
```shell
wget http://nginx.org/download/nginx-1.11.0.tar.gz
sudo tar -zxvf nginx-1.11.0.tar.gz -C /usr/local/src/
```
3. 编译并安装
```shell
cd /usr/local/src/nginx-1.11.0
sudo ./configure
sudo make && sudo make install
```
4. 配置开机启动
```shell
sudo wget https://raw.githubusercontent.com/JasonGiedymin/nginx-init-ubuntu/master/nginx -O /etc/init.d/nginx
sudo chmod +x /etc/init.d/nginx
sudo update-rc.d -f nginx defaults
```

### 源码编译安装 PHP5
1. 安装依赖
```shell
sudo apt-get install libxml2-dev libcurl3-openssl-dev libpng12-dev
```
2. 下载并解压 PHP 源码
```shell
wget http://cn2.php.net/distributions/php-5.6.22.tar.gz
sudo tar -zxvf php-5.6.22.tar.gz -C /usr/local/src/
```
3. 编译并安装
```shell
cd /usr/local/src/php-5.6.22
sudo ./configure \
    --prefix=/usr/local/php \
    --with-config-file-path=/usr/local/etc \
    --with-fpm-user=www-data \
    --with-fpm-group=www-data \
    --enable-fpm \
    --enable-zip \
    --enable-soap \
    --enable-pcntl \
    --enable-shmop \
    --enable-bcmath \
    --enable-shared \
    --enable-sockets \
    --enable-sysvsem \
    --enable-sysvmsg \
    --enable-opcache \
    --enable-sysvshm \
    --enable-mbstring \
    --enable-inline-optimization \
    --disable-debug \
    --disable-rpath \
    --with-pdo-mysql=mysqlnd \
    --with-mysqli=mysqlnd \
    --with-mysql=mysqlnd \
    --with-libxml-dir \
    --with-gettext \
    --with-openssl \
    --with-iconv \
    --with-mhash \
    --with-zlib \
    --with-curl \
    --with-gd
sudo make && sudo make install
```
4. 配置php-fpm开机启动
```shell
sudo cp ./sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
sudo chmod +x /etc/init.d/php-fpm
sudo update-rc.d -f php-fpm defaults
```

### 参考资料
* [nginx-init-ubuntu](https://github.com/JasonGiedymin/nginx-init-ubuntu)
* [Unix 系统下的 Nginx 1.4.x](http://php.net/manual/zh/install.unix.nginx.php#install.unix.nginx)
