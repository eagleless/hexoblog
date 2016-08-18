---
title: Freemarker内置对象
date: 2016-08-18 20:32:48
categorys: [handbook]
tags: [freemarker,java]
---

直接在ftl里使用内置对象:Request,Session,Application,RequestParameters,Parameters。

<!--more-->

#	Request & Session & Application
>	用于获取Request对象中的attribute对象。
>	例如：${Request["method"]}是直接在页面输出属性值。相当于request.getAttribute("method");
>	如果要进行判断	[#if Request["method"] = "edit"]do something[/#if]

_**Session对应HttpSession,Application对应ServletContext,用法参考Request。**_

#	RequestParameters

用于获取Request对象的parameter,例如${RequestParameters["method"]}相当于request.getParameter("method");

#	Parameters

属性获取，依次从RequestParameters、Request、Session、Application对象中获取对应属性参数，一旦获取则不再往下寻找。例如：Parameters["method"]

