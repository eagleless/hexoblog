---
title: Maven之appfuse模板
category: [maven]
date: 2016-08-28 18:09:55
tags: [appfuse,maven]
---
Appfuse是由Matt Raible开发的一个指导性的入门级J2EE框架，它对如何集成流行的Spring、Hibernate、iBatis、struts、Xdoclet、junit 等基础框架给出了示范。提供了对Taperstry和JSF的支持。
<!--more-->
>   常用命令

|命令|功能|
| ------------- |:-------------|
|mvn appfuse:gen-model|根据数据库的表生成java类|
|mvn appfuse:gen|根据 POJOs.生成并安装Tests, DAO, Managers, Controllers and Views|
|mvn appfuse:full-source|把运行所需要的org.appfuse中的依赖类转换成你的包名称|
|mvn eclipse:eclipse|生成eclipse的项目的配置文件，用户可以直接把项目导入到eclipse中|
|mvn jetty:run-war|打包并且发布你的应用程序到Jetty, 查看在 http://localhost:8080|
|mvn appfuse:install|把生成的源代码及配置文件写入到src中|
|mvn integration-test|启动TOMCAT(或别的服务器)进行测试|
|mvn appfuse:remove|删除appfuse:gen.生成的代码mvn|
|appfuse:clean|清除target下的所有内容|

>   生成实体类

mvn appfuse:gen-model

>   生成dao、service等

    mvn appfuse:gen -Dentity=com.joiest.model.MqConfig
    mvn appfuse:gen -Dentity=YbtTransaction

>   使用appfuse创建maven项目

使用maven创建项目

    mvn archetype:create -DgroupId=com.joiest -DartifactId=webtest -DarchetypeArtifactId=maven-archetype-webapp

_说明：DartifactId:项目名称   DgroupId：包结构_

生成项目文件生成.classpath,.project,.setting文件

    mvn eclipse:eclipse

更改appFuse的代码生成方式，修改pom中
修改生成代码方式，找到 

      <genericCore>${amp.genericCore}</genericCore> 
      <fullSource>${amp.fullSource}</fullSource> 
修改成：

       <genericCore>false</genericCore> 
      <fullSource>true</fullSource> 
注意，这里必须吧pom.xml中的genericCore属性设为false 否则只会生成Action 
数据库配置信息(mysql在最底下)

执行项目创建命令后，进入项目主目录后，更改AppFuse到全源代码模式

    mvn appfuse:full-source

生成Model类

    mvn appfuse:gen-mode


    mvn appfuse:gen -Dentity=com.joiest.model.YbtAccount 

把生成的配置文件写入到src目录下的配置文件中

    mvn appfuse:install

下载项目的依赖jar包到本地，并进行集成测试

    mvn

打包并运行项目

    mvn jetty:run-war

通过浏览器访问admin/admin

    http://localhost:8080

修改pom.xml

    <artifactId>maven-eclipse-plugin</artifactId>
    <version>2.4</version>


配置repositories,M2_REPO

运行服务器查看生成的crud实例

    mvn jetty:run


>   下面是创建不同种类项目的Archetype Command：

**_JSF Basic_**

    mvn archetype:create -DarchetypeGroupId=org.appfuse.archetypes -DarchetypeArtifactId=appfuse-basic-jsf -DremoteRepositories=http://static.appfuse.org/releases-DarchetypeVersion=2.0 -DgroupId=com.mycompany.app -DartifactId=myproject 

**_Spring MVC Basic_**

    mvn archetype:create -DarchetypeGroupId=org.appfuse.archetypes -DarchetypeArtifactId=appfuse-basic-spring -DremoteRepositories=http://static.appfuse.org/releases-DarchetypeVersion=2.0 -DgroupId=com.mycompany.app -DartifactId=myproject 

**_Struts 2 Basic_** 
  
    mvn archetype:create -DarchetypeGroupId=org.appfuse.archetypes -DarchetypeArtifactId=appfuse-basic-struts -DremoteRepositories=http://static.appfuse.org/releases-DarchetypeVersion=2.0 -DgroupId=com.mycompany.app -DartifactId=myproject 

**_Tapestry Basic_** 

    mvn archetype:create -DarchetypeGroupId=org.appfuse.archetypes -DarchetypeArtifactId=appfuse-basic-tapestry -DremoteRepositories=http://static.appfuse.org/releases-DarchetypeVersion=2.0 -DgroupId=com.mycompany.app -DartifactId=myproject 

**_JSF Modula_**

    mvn archetype:create -DarchetypeGroupId=org.appfuse.archetypes -DarchetypeArtifactId=appfuse-modular-jsf -DremoteRepositories=http://static.appfuse.org/releases-DarchetypeVersion=2.0 -DgroupId=com.mycompany.app -DartifactId=myproject 

**_Spring MVC Modular_**

    mvn archetype:create -DarchetypeGroupId=org.appfuse.archetypes -DarchetypeArtifactId=appfuse-modular-spring -DremoteRepositories=http://static.appfuse.org/releases-DarchetypeVersion=2.0 -DgroupId=com.mycompany.app -DartifactId=myproject 

**_Struts 2 Modular_**

    mvn archetype:create -DarchetypeGroupId=org.appfuse.archetypes -DarchetypeArtifactId=appfuse-modular-struts -DremoteRepositories=http://static.appfuse.org/releases-DarchetypeVersion=2.0 -DgroupId=com.mycompany.app -DartifactId=myproject 

**_Tapestry Modular_** 

    mvn archetype:create -DarchetypeGroupId=org.appfuse.archetypes -DarchetypeArtifactId=appfuse-modular-tapestry -DremoteRepositories=http://static.appfuse.org/releases-DarchetypeVersion=2.0 -DgroupId=com.mycompany.app -DartifactId=myproject 

**_Core(backend only)_**

    mvn archetype:create -DarchetypeGroupId=org.appfuse.archetypes -DarchetypeArtifactId=appfuse-core -DremoteRepositories=http://static.appfuse.org/releases-DarchetypeVersion=2.0 -DgroupId=com.mycompany.app -DartifactId=myproject
