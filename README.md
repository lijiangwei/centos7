# Linux服务器CentOS7常用软件安装教程

## gitlab

### 安装
新建 /etc/yum.repos.d/gitlab-ce.repo，内容为

    [gitlab-ce]
    name=Gitlab CE Repository
    baseurl=https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el$releasever/
    gpgcheck=0
    enabled=1

再执行

    yum makecache
    yum install gitlab-ce

### 汉化

    # 确认版本号，安装对应版本的汉化包：
    cat /opt/gitlab/embedded/service/gitlab-rails/VERSION

    # 下载gitlab中文源码
    git clone https://gitlab.com/xhang/gitlab.git

    # 先停止gitlab
    gitlab-ctl stop

    # 10.6.4版本的汉化补丁（10.6.4是英文稳定版，10.6.4-zh是中文版，两个 diff 结果便是汉化补丁）
    cd gitlab
    git diff v10.6.4 v10.6.4-zh > ../10.6.4-zh.diff

    # 应用汉化补丁
    cd /opt/gitlab/embedded/service/gitlab-rails
    git apply diff文件保存的目录/10.6.4-zh.diff

    # 启动gitlab
    gitlab-ctl start

    # 初始化gitlab
    gitlab-ctl reconfigure

### 使用自己的nginx服务器
[nginx配置](https://docs.gitlab.com/omnibus/settings/nginx.html#using-an-existing-passenger-nginx-installation)

## nginx

### 安装

    # nginx镜像源
    rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

    # 安装
    yum install nginx -y

    # 启动
    systemctl start nginx

    # 开机启动
    systemctl enable nginx

    # 取消开机启动
    systemctl disable nginx

### 配置

    # 配置文件目录
    cd /etc/nginx

    # 支持php文件
    # 安装php和php-fpm程序
    yum install php
    # php7-fpm镜像
    rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
    #  编辑默认的 php7-fpm 配置文件
    vim /etc/php-fpm.d/www.conf


    #修改配置文件
    location ~ \.php$ {
        #php-fpm的默认端口是9000
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

## svn

### 安装
    # 安装
    yum install subversion

    # 启动
    svnserve -d -r /usr/share/svn --config-file=/usr/share/svn/appebn/conf/svnserve.conf


### 配置
* 用户配置文件目录 /usr/share/svn/appebn/conf/passwd
* 用户权限配置目录 /usr/share/svn/appebn/conf/authz

## dzzoffice--协同办公

### 安装
[下载源码](https://github.com/zyx0814/dzzoffice/releases/tag/2.0beta)

上传到web服务器，访问安装页面

    http://域名/dzzoffice/

## vsftpd--ftp服务器

### 安装

    yum install vsftpd

### 配置    

[ftp服务器配置教程](https://blog.csdn.net/Wyxtnbp/article/details/78372707)

## nextcloud--私有云

## wordpress--搭建网站、博客
[安装教程](https://cn.wordpress.org/txt-download/)
1. 去官网下载源代码
2. 上传到要部署的webserver目录
3. 浏览器访问http://host/wordpress/wp-admin/index.php

## gogs

### 安装
[下载安装包](https://github.com/gogits/gogs/releases/download/v0.11.43/linux_amd64.zip)

[安装教程](https://blog.mynook.info/post/host-your-own-git-server-using-gogs/)

## nodejs

### 安装最新版nodejs
    curl https://rpm.nodesource.com/setup_8.x | bash -



