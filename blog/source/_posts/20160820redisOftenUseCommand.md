---
title: redis常用命令大全
category: [handbook]
date: 2016-08-20 22:30:10
tags: [redis,java]
---

Key、服务器相关的一些常用redis命令。
速查：http://www.cnblogs.com/kissdodog/p/3599047.html

<!--more-->
#	Key相关命令

keys * 取出当前所有的key

exists name 查看n是否有name这个key

del name 删除key name

expire confirm 100 设置confirm这个key100秒过期

ttl confirm 获取confirm 这个key的有效时长

select 0 选择到0数据库 redis默认的数据库是0~15一共16个数据库

move confirm 1 将当前数据库中的key移动到其他的数据库中，这里就是把confire这个key从当前数据库中移动到1中

persist confirm 移除confirm这个key的过期时间

randomkey 随机返回数据库里面的一个key

rename key2 key3 重命名key2 为key3

type key2 返回key的数据类型

#	服务器相关命令

ping PONG返回响应是否连接成功

echo 在命令行打印一些内容

select 0~15 编号的数据库

quit  /exit 退出客户端

dbsize 返回当前数据库中所有key的数量

info 返回redis的相关信息

config get dir/* 实时传储收到的请求

flushdb 删除当前选择数据库中的所有key

flushall 删除所有数据库中的数据库

	redis-cli KEYS "pattern" | xargs redis-cli DEL
