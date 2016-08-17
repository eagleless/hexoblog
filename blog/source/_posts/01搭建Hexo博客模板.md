---
title: Hexo+Github搭建
date: 2016-08-10 17:37:58
category: [note]
tags: [git,hexo]
---

## 搭建参考地址
http://jianbing.github.io/2016/03/03/set-up-blog/
<!--more-->
## 修改主题为yilia-l
http://kiritor.github.io/2016/04/28/yilia-l/
## Hexo Landscape主题的字体和JS库优化
http://www.jianshu.com/p/ffcdc4fec6ec

deploy:
	type: git
	repository: git@github.com:eagleless/eagleless.github.io.git          
	branch: master
***

# 生成SSH密钥过程
1.查看是否已经有了ssh密钥：cd ~/.ssh
如果没有密钥则不会有此文件夹，有则备份删除
2.生存密钥：
$ ssh-keygen -t rsa -C "fox520527088@163.com"
按3个回车，密码为空。

Your identification has been saved in /home/tekkub/.ssh/id_rsa.
Your public key has been saved in /home/tekkub/.ssh/id_rsa.pub.
The key fingerprint is:
………………

最后得到了两个文件：id_rsa和id_rsa.pub

3.添加密钥到ssh：ssh-add 文件名
需要之前输入密码。
4.在github上添加ssh密钥，这要添加的是“id_rsa.pub”里面的公钥。
打开https://github.com/ ，登录添加SSHKey。

***

## 常用hexo命令
```
hexo n "HelloWorld"
hexo g
hexo d
hexo g -d
```