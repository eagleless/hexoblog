---
title: 阿里云安装jdk、mysql、tomcat
date: 2016-12-09 20:50:34
tags: [aliyun]
---
CentOS 7.2 64位安装jdk、mysql、tomcat
<!--more-->
#   安装rzsz

    yum list lrzsz*
    yum install lrzsz -y

#   安装jdk
因为yum list的jdk都是openjdk,需下载rpm包再安装

    rpm -ivh jdk-7u45-linux-x64.rpm
    vi /etc/profile

    export JAVA_HOME=/usr/java/jdk1.7.0_45
    export PATH=$JAVA_HOME/bin:$PATH
    export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

#   安装mysql

`安装rpm包`

    rpm -Uvh http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm

`查看当前可用的mysql安装资源`

    yum repolist enabled | grep "mysql.*-community.*"

`安装mysql-server跟mysql-client`

    yum -y install mysql-community-server

`加入开机启动`

    systemctl enable mysqld

`启动mysql服务进程`

    systemctl start mysqld

`重置密码`

    mysql_secure_installation

`配置mysql远程连接`

    mysql -uroot -p
    use mysql

将host设置为%表示任何ip都能连接mysql，当然您也可以将host指定为某个ip

    update user set host='%' where user='root' and host='localhost';
    flush privileges;        #刷新权限表，使配置生效

关闭远程连接

    update user set host='localhost' where user='root';


