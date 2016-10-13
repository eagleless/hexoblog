---
title: SpringMvc静态资源处理
date: 2016-10-13 10:01:52
tags: [spring]
---
处理静态资源，我想这可能是框架搭建完成之后Web开发的”头等大事“了。
<!--more-->
还记得Spring MVC中的DispatcherServlet吗？它是Spring MVC中的前置控制器，若配置的拦截路径为“/”，那么所有的请求都将被它拦截。对静态资源的访问也属于一个请求，那么也会被它拦截，然后进入它的匹配流 程，我们知道它是根据HandlerMapping的配置来匹配的。而对于静态资源来说，默认的Spring MVC是没有注册匹配规则的，此时若你去请求一个静态资源，则会报404错误。

>   如何处理静态资源的请求呢？

我们可以配置一个处理静态资源的HandlerMapping
```xml
<bean id="resourceHttpRequestHandler" class="org.springframework.web.servlet.resource.ResourceHttpRequestHandler">  
    <property name="locations" value="classpath:/META-INF/resources/"></property>     
</bean>  
  
<bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">  
    <property name="mappings">  
        <props>  
            <prop key="/resources/**">resourceHttpRequestHandler</prop>  
        </props>  
    </property>  
</bean>
```

另外，还可以使用mvc命名空间的resources标签来配置

    <mvc:resources mapping="/resources/**" location="/resources/" />

>   直接用容器的DefaultServlet

比如我们将资源文件都放在resouces目录下，那么只需要在web.xml中配置：

     <servlet-mapping>  
        <servlet-name>default</servlet-name>  
        <url-pattern>/resource/*</url-pattern>  
    </servlet-mapping>  

并将它放在所有Servlet的最前面（为了让它最先匹配），这样的话性能上应该比较好

所以，综上所述，性能最好的应该是直接利用容器的DefaultServlet，让它最先拦截静态资源请求，这样就避免了后续的转发等操作，提高了 性能，但是无法访问classpath下的资源文件。而通过mvc:resources标签可以简单配置匹配规则和资源文件路径，应该说是最简单快捷的一 种方式，当然这大概也是mvc命名空间设计的初衷。