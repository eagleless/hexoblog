---
title: Log4j之FileAppender
date: 2016-11-05 23:13:14
tags: [log]
---
DailyRollingAppender按日分割日志。RollingAppender按文件大小分割日志。
<!--more-->
#   DailyRollingAppender

使用FileAppender可以将log信息输出到文件中，但是如果文件太大了读起来就很不方便了。这时就可以使用DailyRollingAppender。可以把log信息输出到按照日期来区分的文件中。配置文件就会每天产生一个文件，每个log文件只记录当天的log信息。

    log4j.appender.A2=org.apache.log4j.DailyRollingFileAppender
    log4j.appender.A2.file=dglog
    log4j.appender.A2.DatePattern='.'yyyy-MM-dd
    log4j.appender.A2.layout=org.apache.log4j.PatternLayout
    log4j.appender.A2.layout.ConversionPattern=%5r %-5p %c{2} -%m%n

#   RollingAppender
文件大小到达指定尺寸的时候产生一个新的文件。

    log4j.appender.R=org.apache.log4j.RollingFileAppender
    log4j.appender.R.File=../logs/dglog.log
    #Controller the maximum log file size
    log4j.appender.R.MaxFileSize=100KB
    #Archive log files(one backup file here)
    log4j.appender.R.MaxBackupIndex=1
    log4j.appender.R.layoutorg.apache.log4j.PatternLayout
    log4j.appender.R.ConversionPattern=%p %t %c - %m%n

这个配置文件指定了输出源R，是一个轮转日志文件。最大的文件是100KB，当一个文件达到最大尺寸时，log4j会自动把example.log重名民为dglog.log.1，然后重建一个新的dglog.log文件依次轮转。

