---
title: 阿里云服务器搭建nextcloud个人网盘
date: 2017-11-23 21:40:00
tags: nextcloud
categories: tech
---
本文介绍了阿里云服务器上搭建个人网盘的过程，其中服务器的系统采用ubuntu16.04，搭建博客使用软件nextcloud，同时最终绑定域名。
<!--more-->
# 安装LAMP环境
## Apache安装
1. 使用root账号登陆
1. 安装环境：使用如下命令安装
    ```
    apt update && 
    apt-get install apache2 libapache2-mod-php7.0 && 
    apt-get install php7.0-gd php7.0-json php7.0-mysql php7.0-curl php7.0-mbstring && 
    apt-get install php7.0-intl php7.0-mcrypt php-imagick php7.0-xml php7.0-zip
    ```
1. 安装NextCloud，[下载地址]()  
    1. 下载NextCloud到一个目录
    1. 解压文件，`unzip *`
    1. 复制到 Apache2 根目录`cp -rv nextcloud /var/www/`
    1. 配置Apache2：创建子目录配置文件，`vim /etc/apache2/sites-available/nextcloud.conf`，写入如下内容：  
        ```
        Alias /nextcloud "/var/www/nextcloud/"
        <Directory /var/www/nextcloud/>
            Options +FollowSymlinks
            AllowOverride All
            Satisfy Any
            <IfModule mod_dav.c>
                Dav off
            </IfModule>
            SetEnv HOME /var/www/nextcloud
            SetEnv HTTP_HOME /var/www/nextcloud
        </Directory>
        ```
    1. 链接子目录配置文件: `ln -s /etc/apache2/sites-available/nextcloud.conf /etc/apache2/sites-enabled/nextcloud.conf`
    1. 更改网站默认目录：`vim /etc/apache2/sites-available/000-default.conf` ,修改以下内容：`DocumentRoot /var/www/nextcloud`
    1. 添加模块：  
        ```
        a2enmod rewrite
        a2enmod headers
        a2enmod env
        a2enmod dir
        a2enmod mime
        ```
    1. 配置根目录权限：`chown -R www-data:www-data /var/www/nextcloud/`
    1. 创建详细配置脚本：`vim script`，添加如下内容：
        ```
        #!/bin/bash
        ocpath='/var/www/nextcloud'
        htuser='www-data'
        htgroup='www-data'
        rootuser='root'
        printf "Creating possible missing Directories\n"
        mkdir -p $ocpath/data
        mkdir -p $ocpath/updater
        printf "chmod Files and Directories\n"
        find ${ocpath}/ -type f -print0 | xargs -0 chmod 0640
        find ${ocpath}/ -type d -print0 | xargs -0 chmod 0750
        printf "chown Directories\n"
        chown -R ${rootuser}:${htgroup} ${ocpath}/
        chown -R ${htuser}:${htgroup} ${ocpath}/apps/
        chown -R ${htuser}:${htgroup} ${ocpath}/config/
        chown -R ${htuser}:${htgroup} ${ocpath}/data/
        chown -R ${htuser}:${htgroup} ${ocpath}/themes/
        chown -R ${htuser}:${htgroup} ${ocpath}/updater/
        chmod +x ${ocpath}/occ
        printf "chmod/chown .htaccess\n"
        if [ -f ${ocpath}/.htaccess ]
            then
            chmod 0644 ${ocpath}/.htaccess
            chown ${rootuser}:${htgroup} ${ocpath}/.htaccess
        fi
        if [ -f ${ocpath}/data/.htaccess ]
            then
            chmod 0644 ${ocpath}/data/.htaccess
            chown ${rootuser}:${htgroup} ${ocpath}/data/.htaccess
        fi
        ```
    1. 运行脚本：`chmod +x script && ./script`
    1. 重启服务：`service apache2 restart`
至此Apache安装完毕
---
## 安装数据库
1. 安装mysql：`apt-get install mysql-server mysql-client`
1. 初始化安全配置：`mysql_secure_installation`，填写相关信息。
## 设置远程访问
1. 解除绑定ip地址：`vim /etc/mysql/my.cnf`，找到`bind-address=127.0.0.1`，删除这一行。如果没有这行代码，那就去`vim /etc/mysql/mysql.conf.d/mysqld.cnf`找到`bind-address=127.0.0.1`，删除这一行。
1. 授权用户远程连接：
    1. 先进入mysql，`mysql -u root -p`输入root用户密码
    1. 创建数据库`create database nextcloud;` 
# 配置nextcloud
## 初始化nextcloud：在浏览器中输入`http://服务器ip`，出现如下界面：  
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flsa8229w0j20uq0p51as.jpg)  
这是我的配置：  
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flsaajhmf0j20fo0mwk0o.jpg)  
创建用户完成之后的界面：  
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flsabq7x0xj21hb0ppjsz.jpg)

---
---
---
2017年11月24日14:41更新：  

---
今天看到了一种新的方式安装nextcloud，既简单又方便，配置迅捷：
# 安装snap
1. 查看是否安装，`snap --version`，如果没安装的话直接安装，`apt install snap`
1. 搜索nextcloud软件`snap find nextcloud`
1. 使用`snap install nextcloud`安装nextcloud
1. 安装成功后直接在浏览器中输入公网ip即可
1. 在弹出的界面中填写相关信息完成安装
# 配置nextcloud
## 绑定域名  
首先在域名解析平台上解析域名，将域名绑定为阿里云服务器公网ip，然后就可以使用域名访问nextcloud。中途会出现信任该域名的提示，点击确认即可。
## 启用ssl安全连接  
启用 Let’s encrypt 的 SSL 证书，使用 nextcloud.enable-https lets-encrypt 命令：在终端中会出现一系列信息，确认无误后按y即可，然后会要求输入电子邮箱（主要用于以后找回密码）和域名，填写后enter即可。出现以下信息即可：
```
Attempting to obtain certificates... done
Restarting apache... done
```
再次访问界面会出现如下情况：  
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flt6lx4atyj20d400wglk.jpg)