---
title: Linux之less命令
category: [linux]
date: 2016-08-22 23:16:03
tags: [linux,java]
---
Linux中的less命令主要用来浏览文件内容，与more命令的用法相似，不同于more命令的是，less命令可往回卷动浏览以看过的部分。

<!--more-->

参考：http://www.xitongzhijia.net/xtjc/20141209/32242.html
less 的用法比起 more 更加的有弹性。在 more 的时候，我们并没有办法向前面翻， 只能往后面看，但若使用了 less 时，就可以使用 ［pageup］ ［pagedown］ 等按键的功能来往前往后翻看文件，更容易用来查看一个文件的内容！除此之外，在 less 里头可以拥有更多的搜索功能，不止可以向下搜，也可以向上搜。

#   1．命令格式
　　less［参数］ 文件
#   2．命令功能
less与more类似,但使用less可以随意浏览文件，而more仅能向前移动，却不能向后移动，而且 less 在查看之前不会加载整个文件。
#   3．命令参数
    -b 《缓冲区大小》 设置缓冲区的大小
    -e 当文件显示结束后，自动离开
    -f 强迫打开特殊文件，例如外围设备代号、目录和二进制文件
    -g 只标志最后搜索的关键词
    -i 忽略搜索时的大小写
    -m 显示类似more命令的百分比
    -N 显示每行的行号
    -o 《文件名》 将less 输出的内容在指定文件中保存起来
    -Q 不使用警告音
    -s 显示连续空行为一行
    -S 行过长时间将超出部分舍弃
    -x 《数字》 将“tab”键显示为规定的数字空格
    /字符串：向下搜索“字符串”的功能
    ？字符串：向上搜索“字符串”的功能
    n：重复前一个搜索（与 / 或 ？ 有关）
    N：反向重复前一个搜索（与 / 或 ？ 有关）
    b 向后翻一页
    d 向后翻半页
    h 显示帮助界面
    Q 退出less 命令
    u 向前滚动半页
    y 向前滚动一行
    空格键 滚动一行
    回车键 滚动一页
    [pagedown］： 向下翻动一页
    ［pageup］： 向上翻动一页

#   4．使用实例
>  实例1：查看文件

    [yxgly@ZC_VM_10_100_138_183 ~]$ less 2016.log 
    a2016


    b2015


    c3333333333333
    2016.log (END) 
　　
>  实例2：ps查看进程信息并通过less分页显示

    [yxgly@ZC_VM_10_100_138_183 ~]$ ps -ef |less
    UID        PID  PPID  C STIME TTY          TIME CMD
    root         1     0  0 Jul30 ?        00:00:00 /sbin/init
    root         2     0  0 Jul30 ?        00:00:00 [kthreadd]
    root         3     2  0 Jul30 ?        00:00:00 [migration/0]
    root         4     2  0 Jul30 ?        00:00:03 [ksoftirqd/0]
    root         5     2  0 Jul30 ?        00:00:00 [migration/0]
    root         6     2  0 Jul30 ?        00:00:03 [watchdog/0]
    root         7     2  0 Jul30 ?        00:38:46 [events/0]
    root         8     2  0 Jul30 ?        00:00:00 [cgroup]
    root         9     2  0 Jul30 ?        00:00:00 [khelper]
    root        10     2  0 Jul30 ?        00:00:00 [netns]
    root        11     2  0 Jul30 ?        00:00:00 [async/mgr]
    root        12     2  0 Jul30 ?        00:00:00 [pm]
    root        13     2  0 Jul30 ?        00:00:08 [sync_supers]
    root        14     2  0 Jul30 ?        00:00:08 [bdi-default]
    root        15     2  0 Jul30 ?        00:00:00 [kintegrityd/0]
    root        16     2  0 Jul30 ?        00:00:16 [kblockd/0]
    root        17     2  0 Jul30 ?        00:00:00 [kacpid]
    root        18     2  0 Jul30 ?        00:00:00 [kacpi_notify]
    root        19     2  0 Jul30 ?        00:00:00 [kacpi_hotplug]
    root        20     2  0 Jul30 ?        00:00:00 [ata_aux]
    root        21     2  0 Jul30 ?        00:00:00 [ata_sff/0]
    root        22     2  0 Jul30 ?        00:00:00 [ksuspend_usbd]
    root        23     2  0 Jul30 ?        00:00:00 [khubd]
    root        24     2  0 Jul30 ?        00:00:00 [kseriod]
    root        25     2  0 Jul30 ?        00:00:00 [md/0]

>   实例3：查看命令历史使用记录并通过less分页显示

    [yxgly@ZC_VM_10_100_138_183 ~]$ history | less
    54  cd logs/
    55  ll
    56  rm catalina.out 
    57  ll
    58  cd ..
    59  ll
    60  cd work/Catalina/localhost/
    61  ll
    62  rm -rf *
    63  cd ..
    64  ll
    65  cd bin/
    66  ll
    67  vi startup.sh 
    68  ll
    69  cd ..
    70  cd conf/
    71  ll
    72  vi server.xml 
    73  cd ..
    74  cd yangkai/

>   实例4：浏览多个文件

    [yxgly@ZC_VM_10_100_138_183 ~]$ less 2016.log 2015.log 
    a2016


    b2015


    c3333333333333

2016.log (file 1 of 2) (END) - Next: 2015.log

:n

    2015
    2015
    ~
    ~
    ~
    ~
    ~
    2015.log (file 2 of 2) (END) 

> 　　_说明：
> 　　输入 ：n后，切换到 log2014.log
> 　　输入 ：p 后，切换到log2013.log_

#   5．附加备注

>   全屏导航

    ctrl + F - 向前移动一屏
    ctrl + B - 向后移动一屏
    ctrl + D - 向前移动半屏
    ctrl + U - 向后移动半屏

> 　单行导航

    j - 向前移动一行
    k - 向后移动一行
    3.其它导航
    G - 移动到最后一行
    g - 移动到第一行
    q / ZZ - 退出 less 命令

>   其它有用的命令

    v - 使用配置的编辑器编辑当前文件
    h - 显示 less 的帮助文档
    &pattern - 仅显示匹配模式的行，而不是整个文件

>   标记导航

    当使用 less 查看大文件时，可以在任何一个位置作标记，可以通过命令导航到标有特定标记的文本位置：
    ma - 使用 a 标记文本的当前位置
    ‘a - 导航到标记 a 处

