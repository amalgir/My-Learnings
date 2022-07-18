# Java SpringBoot

***

## Contents

1) [Introduction](#id1)
2) [SpringBoot Auto-Configuration](#id2)

***

<div id="id1"></div>

### 1) Introduction

* Spring framework  is a popular java EE framework for building web  and enterprise applications
* Spring Boot is an extension of Spring Framework
* Main goal of spring boot is to create production ready spring applications without requiring developers to write the same boilerplate configuration again and again
* Spring Boot internally uses all Spring framework libraries

***

#### Features of Spring Boot

* Spring Boot starters
* Spring Boot autoconfiguration
* Externalized Configuration
* Spring Boot actuator
* Easy to use embedded servlet container support

Spring Framework has a lot of configurations . Spring Boot resolves that by automatically configuring many things

**Spring Boot Starters**  --> So we dont need to add many dependencies. Starter dependencies can be added using single dependency `spring-boot-starter-data-jpa`. Adding this dependency will add all dependencies required to work with spring data jpa. 
Another exapmle is `spring-boot-starter-web` --> adds spring mvc, web mvc, tomcat..


**Spring Boot auto-configuration** -->attempts to automatically configure the Spring application based on the jar dependencies that we have added


**Externalized configuration** --> allows developer to use same app in different environment like dev environment, qa, uat or production by using properties or yaml file for configuration. (Spring Boot allows to have different profile/these files for different environment)

**Spring Boot actuator** --> provides various rest endpoints to view various detail like -
* view the application bean configuration details
* view the application URL mappings
* view environment details
* view configuration parameter values
* view the registered health check metrics

**Easy to use embedded servlet container support** --> provides default tomcat servlet to deploy our app

***

#### Different ways to create spring Boot Project

1) **_Using spring initializer_**
   * Website: https://start.spring.io/
   * Go to this website and create


2) **_using spring starter project in STS Eclipse_**
   *  In Eclipse, File-> New-> Spring starter Project

3) **_Spring Boot CLI (command line interface)_**
    * install Spring Boot CLI and follow Spring Boot CLI docs


**_Using spring initializer_**

* Go to website and fill details
* Add dependencies -> if we need web (to create spring mvc web application or Spring Rest API application, type web and select `Spring web`
* If we need sql --> sql driver from dependency, postgre sql --> postgresql driver
* Click `Explore` to view folder structure
* Click `Generate` to get zip file
* Then unzip the file
* import the unzipped one in IDE with file--> import option

![Spring Initializer](/Images/SpringBoot/spring_initializer.jpg)

![Spring Dependency Adding](/Images/SpringBoot/spring_initializer_web.png)

![Spring Folder Structure](/Images/SpringBoot/spring_initializer_explore.jpg)

#### Intellij

* Install plugin Spring assistant
* Then New Project
* From left panel, select spring initializer or spring assistant
* Give details like in initializer
* Select dependecies (select web) and click ok
* Springboot project is created
 
**Faced some issues**  --> Didnt run, showed red marks as import error
* solved my `Build` --> `Rebuild Project`
* Then error came --> updated pom java version source and target which intellij automatically did after asking
* Updated intellij to latest version
* Now run java class file to see spring boot running

![Intellij](/Images/SpringBoot/springboot_framework_intellij.jpg)

***
***

<div id="id2"></div>

### 2) SpringBoot Auto-Configuration

####Theory

* When we use Spring MVC, we need to configure -Component scan, Dispatcher server, View resolver, Web jars for delivering static content
* When we use Hibernate/JPA , we need to configure - data source, entity manager factory/session factory, transaction manager
* SpringBoot automates these things

* While choosing dependency, we added web which adds this one in pom file 
```xml
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

* Add this logging level in `application.properties` file in  `src/main/resources`
   > `logging.level.org.springframework.web=debug`

* Changing this logging level to this `logging.level.org.springframework=debug` gives some more logs where we can see dispatcherServlet logs - meaning springboot has autoconfigured everything

* spring-webmvc.jar file has dispatcherServlet class files.

* There will be a section called `Negative matches:` in debug logs where we can see what all dependencies are not auto-configured. If we add some to pom, then springboot detects it and autoconfigure
