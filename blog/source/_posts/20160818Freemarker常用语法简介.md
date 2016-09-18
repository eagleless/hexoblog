---
title: Freemarker常用语法简介
date: 2016-08-18 20:32:48
category: [handbook]
tags: [freemarker,java]
---

布尔值、当前时间。直接在ftl里使用内置对象:Request,Session,Application,RequestParameters,Parameters。

<!--more-->
>   list处理

    <#list testMap?keys as testKey> 
           < option value="${testKey}" > 
                  ${testMap[testKey]} 
         </option> 
    </#list>

1.sequence?first 返回sequence的第一个值。 

2.sequence?last  返回sequence的最后一个值。 

3.sequence?reverse 将sequence的现有顺序反转，即倒序排序 

4.sequence?size    返回sequence的大小 

5.sequence?sort    将sequence中的对象转化为字符串后顺序排序 

6.sequence?sort_by(value) 按sequence中对象的属性value进行排序 

item_index:当前变量的索引值
item_has_next:是否存在下一个对象
也可以使用<#break>指令跳出迭代

>   String字符串处理

1.substring（start,end）从一个字符串中截取子串 

    ${"abcde"?substring(0,2)}   ab
start:截取子串开始的索引，start必须大于等于0，小于等于end 
end: 截取子串的长度，end必须大于等于0，小于等于字符串长度，如果省略该参数，默认为字符串长度

    ${"abcde"?substring(2)} cde
2.cap_first 将字符串中的第一个单词的首字母变为大写。

    ${"abcde"?cap_first}
3.uncap_first将字符串中的第一个单词的首字母变为小写。

    ${"ABCDE"?uncap_first}
4.capitalize将字符串中的所有单词的首字母变为大写

    ${"ABCDE fd"?capitalize}    Abcde Fd
5.date,time，datetime将字符串转换为日期 

    [#assign date1="2015-10-25"?date("yyyy-MM-dd")]
    [#assign date2="18:56:40"?time("HH:mm:ss")]
    [#assign date3="2009-10-12 9:28:20"?datetime("yyyy-MM-dd HH:mm:ss")]
6.ends_with 判断某个字符串是否由某个子串结尾，返回布尔值。

    ${"string"?ends_with("ing")?string} 返回结果为true 
7.html 用于将字符串中的<、>、&和“替换为对应得&lt;&gt;&quot:&amp
8.index_of（substring,start）在字符串中查找某个子串，返回找到子串的第一个字符的索引，如果没有找到子串，则返回-1。 
Start参数用于指定从字符串的那个索引处开始搜索，start为数字值。 
如果start大于字符串长度，则start取值等于字符串长度，如果start小于0， 则start取值为0。

    ${"string"?index_of("ing")}
9.length返回字符串的长度
10.lower_case将字符串转为小写 
11.upper_case将字符串转为大写
12.contains 判断字符中是否包含某个子串。返回布尔值

    ${"string"?contains("ing")?string}
13.number将字符串转换为数字 

    ${"111.21"?number}
14.replace用于将字符串中的一部分从左到右替换为另外的字符串

    ${"striabg"?replace("ab","n")}
15.split使用指定的分隔符将一个字符串拆分为一组字符串

    [#list "This|is|split"?split("|") as s] ${s},[/#list]
16.trim 删除字符串首尾空格 ${"  String "?trim}

>   数字处理

Freemarker中预订义了三种数字格式：number,currency（货币）和percent(百分比)其中number为默认的数字格式转换

    [#assign tempNum=20]  
    ${tempNum}      
    ${tempNum?string.number}或${tempNum?string("number")}  结果为20  
    ${tempNum?string.currency}或${tempNum?string("currency")}  结果为￥20.00  
    ${tempNum?string. percent}或${tempNum?string("percent")}  结果为2,000% 

    ${num?string('0.00')}
如果小数点后不足两位，用 0 代替

    ${num?string('#.##')}
如果小数点后多余两位，就只保留两位，否则输出实际值
输出为：1239765.46

    ${num?string(',###.00')}
输出为：1,239,765.46
整数部分每三位用 , 分割，并且保证小数点后保留两位，不足用 0 代替

    ${num?string(',###.##')}
输出为：1,239,765.46
整数部分每三位用 , 分割，并且小数点后多余两位就只保留两位，不足两位就取实际位数，可以不不包含小数点

    ${num?string('000.00')}
输出为：012.70
整数部分如果不足三位（000），前面用0补齐，否则取实际的整数位

    ${num?string('###.00')}
等价于

    ${num?string('#.00')}
输出为：12.70
整数取实际的位数

数字格式化插值可采用#{expr;format}形式来格式化数字,其中format可以是:
mX:小数部分最小X位
MX:小数部分最大X位
如下面的例子:

    <#assign x=2.582/>
    <#assign y=4/>
    #{x; M2} <#-- 输出2.58 -->
    #{y; M2} <#-- 输出4 -->
    #{x; m1} <#-- 输出2.6 -->
    #{y; m1} <#-- 输出4.0 -->
    #{x; m1M2} <#-- 输出2.58 -->
    #{x; m1M2} <#-- 输出4.0 -->

>   Boolean值处理

    ${foo?string("yes", "no")}

>   ${.now?date}

使用.now为当前时间
FreeMarker会将 java.sql.Date java.sql.Time java.sql.Timestamp 类型的变量自动识别为 date time datetime。所以当变量是以上三种类型时，FreeMarker会自动匹配设置的格式，不需要在变量的后面加上?date ?time ?datetime 。
FreeMarker无法自动识别 java.util.Date 类型应该显示哪种格式，这时需要明确的指定其要显示的格式，否则FreeMarker将会抛出异常。

>   map

hash?keys 返回hash里的所有key,返回结果为sequence 
hash?values 返回hash里的所有value,返回结果为sequence

    [#assign user={"name":"hailang", "sex":"man"}]
    [#assign userkeys = user?keys]
    [#list userkeys as k]
        ${k}=${user[k]},
    [/#list]


#	Request & Session & Application
>	用于获取Request对象中的attribute对象。
>   例如：${Request["method"]}是直接在页面输出属性值。
>   相当于request.getAttribute("method");
>	如果要进行判断	[#if Request["method"] = "edit"]do something[/#if]

_**Session对应HttpSession,Application对应ServletContext,用法参考Request。**_

#	RequestParameters

用于获取Request对象的parameter,例如${RequestParameters["method"]}相当于request.getParameter("method");

#	Parameters

属性获取，依次从RequestParameters、Request、Session、Application对象中获取对应属性参数，一旦获取则不再往下寻找。例如：Parameters["method"]

