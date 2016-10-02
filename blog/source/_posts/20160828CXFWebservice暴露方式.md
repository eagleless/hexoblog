---
title: CXFWebservice暴露方式
date: 2016-08-28 22:39:18
tags: [webservice,java]
---
使用注解和XML方式暴露REST风格webservice，使用JAX-WS暴露SOAP风格webservice。
使用wsdl2java根据wsdl生成java源码。
<!--more-->

>   REST风格 注解方式

```java
//接口使用注解
@WebService
@Path("/users")
//方法声明如下
@GET    
@Path("{lastname}")    
List<Person> findByLastName(@PathParam("lastname") String lastName);     
@GET    
List<Person> getPeople();

```

>   REST风格 XML配置方式

使用了JAX-RS，无需在接口中声明任何注解
`src/main/webapp/WEB-INF/cxf-servlet.xml`中添加

    <jaxrs:serviceBeans>
        <ref bean="userManager"/>
    </jaxrs:serviceBeans>

`http://localhost:8080/services/api/users.json`
也可以这样访问`http://localhost:8080/services/api/users`
但必须给User添加@XmlRootElement注解

>   暴露SOAP WebService

SOAP:Simple Object Access Protocol简单对象访问协议
接口UserService使用@WebService注解

```java
    @WebService
    public interface UserService{
        //...
    }
```
实现类UserServiceImpl使用

```java
    @Service("userManager")
    @WebService(serviceName = "UserService",  endpointInterface = "com.joiest.service.UserService")
    public class UserServiceImpl implements UserService{
        //...
    }
```

最好提供无参构造器，以满足JAX-WS
`src/main/webapp/WEB-INF/cxf-servlet.xml` 中添加

    <jaxws:endpoint id="userService" implementor="#userManager" address="/UserService"/>

运行mvn jetty:run 
http://localhost:8080/services/UserService?wsdl
即可查看userService的wsdl描述

>   wsdl2java生成java源码

```bash
wsdl2java -s E:\myToolsApi\studyTools\tools\webservice\cxf\gen_src\src -uri http://localhost:8088/cxfws/services/Hellows?wsdl

wsimport –s . client http://localhost:8088/cxfws/services/Hellows?wsdl

wsimport -s . http://127.0.0.1:8088/cxfws/services/Hellows?wsdl

wsdl2java -s . -uri http://localhost:8088/cxfws/services/Hellows?wsdl
```
