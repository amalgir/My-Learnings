# Java SpringBoot

***

## Contents

1) [Introduction](#id1)

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
* Select dependecies and click ok
* Springboot project is created
 
