---
title: MarkDown语法
date: 2016-08-10 16:16:01
category: [handbook]
tags: [markdown]
---
# Markdown语法说明中文版
http://www.appinn.com/markdown/

<!--more-->
```java
public class HelloWorld{
    public static void main(String[] args){
        System.out.println("HelloWorld");
    }
}
```

# Markdown表示h1-h6使用语法
类 Atx 形式则是在行首插入 1 到 6 个 # ，对应到标题 1 到 6 阶
	# 这是 H1
	## 这是 H2
	###### 这是 H6

# 链接语法
Markdown 支持两种形式的链接语法： 行内式和参考式两种形式。

不管是哪一种，链接文字都是用 [方括号] 来标记。

要建立一个行内式的链接，只要在方块括号后面紧接着圆括号并插入网址链接即可，如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可。

#	[百度一下,你就知道](www.baidu.com) 
	[百度一下,你就知道](www.baidu.com"百度标题")

#	[Markdow图片](http://image.baidu.com/search/detail?ct=503316480&z=0&ipn=d&word=%E5%9B%BE%E7%89%87&hs=0&pn=7&spn=0&di=147138333760&pi=&rn=1&tn=baiduimagedetail&ie=utf-8&oe=utf-8&cl=2&lm=-1&cs=1257261666%2C1562029974&os=2547077022%2C2864557078&simid=4212753602%2C624021646&adpicid=0&ln=30&fr=ala&fm=&sme=&cg=&bdtype=0&oriquery=&objurl=http%3A%2F%2Fpic3.nipic.com%2F20090709%2F2893198_075124038_2.jpg&fromurl=ippr_z2C%24qAzdH3FAzdH3Fooo_z%26e3Bgtrtv_z%26e3Bv54AzdH3Ffi5oAzdH3FnAzdH3F0nAzdH3F8klvkdw8vvvbw8bu_z%26e3Bip4s&gsm=0)

	[Markdow图片](http://image.baidu.com/search/detail?ct=503316480&z=0&ipn=d&word=%E5%9B%BE%E7%89%87&hs=0&pn=7&spn=0&di=147138333760&pi=&rn=1&tn=baiduimagedetail&ie=utf-8&oe=utf-8&cl=2&lm=-1&cs=1257261666%2C1562029974&os=2547077022%2C2864557078&simid=4212753602%2C624021646&adpicid=0&ln=30&fr=ala&fm=&sme=&cg=&bdtype=0&oriquery=&objurl=http%3A%2F%2Fpic3.nipic.com%2F20090709%2F2893198_075124038_2.jpg&fromurl=ippr_z2C%24qAzdH3FAzdH3Fooo_z%26e3Bgtrtv_z%26e3Bv54AzdH3Ffi5oAzdH3FnAzdH3F0nAzdH3F8klvkdw8vvvbw8bu_z%26e3Bip4s&gsm=0)

#	**Markdown Blod加粗显示**
	**Markdown Blod加粗显示**

# _Markdown Italic斜体_
	_Markdown Italic斜体_

#	有序列表和无序列表
Markdown 支持有序列表和无序列表。无序列表使用星号、加号或是减号作为列表标记;有序列表则使用数字接着一个英文句点。
	*	Red
	*   Green
	*   Blue

	1.  Bird
	2.  McHale
	3.  Parish

#	Blockquote段落
Markdown Blockquote段落结构Web界面可以使用Flask框架来搭建，GUI界面可以使用TK，PyQT，wxPython等GUI库来编写，从学习成本来说，命令行界面是最容易上手，这一篇我们来聊一聊命令行界面的实现。
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.


#	分割线
你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。
	* * *

	***

	*****

	- - -

	---------------------------------------

