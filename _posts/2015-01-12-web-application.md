---
layout: post
title: "web开发环境配置"
description: ""
category: 
tags: []
---
{% include JB/setup %}

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

<script src="https://google-code-prettify.googlecode.com/svn/loader/run_prettify.js"></script>

谈到web，最简单的就是静态web，基于html+js在本地即可实现。然而要想有用户交互，则必须加入动态解析过程，流行的动态语言有jsp（java server Pages）和php（Hypertext Preprocessor）。这两种语言都需要服务器进行解析。由此其开发环境也就变得复杂。我们将介绍两种文本、
开发环境。

##JSP环境

###tomcat+eclipse web应用开发环境配置

1 下载安装tomcat，地址：http://tomcat.apache.org/download-60.cgi 

windows32位系统下载：apache-tomcat-6.0.35-windows-x86.zip，解压放到指定目录就可以，无需安装。

2 下载安装eclipse， 地址：http://www.eclipse.org/downloads/ 

下载eclipse-jee-indigo-SR1-win32.

3 下载tomcat插件，可以搜索tomcatPluginV321.zip

下载后解压放到eclipse安装目录的plugins目录下，启动eclipse就可以看到下图所示的按钮

4 配置tomcat

window-->Preferences-->Tomcat

设置tomcat的版本和安装目录    

<p><img src="/img/webapp1.png"></p>

设置完成后就可以在eclipse里面直接启动或关闭tomcat服务了。

<p><img src="/img/webapp2.png"></p>

5 配置Server runtime environments

window --> Preferences --> Server --> Runtime Environments

配置很简单，点击add按钮，选择添加就可以了。如下图    

<p><img src="/img/webapp3.png"></p>

6 创建Web应用   

<p><img src="/img/webapp4.png"></p> 

创建一个Dynamic Web Project

在创建的项目的WebContent目录下创建一个index.jsp文件。如下图所示

<p><img src="/img/webapp5.png"></p>

7 发布Web应用

右键单击项目 选择Run As --> Run on Server 点击finish完成发布   

<p><img src="/img/webapp6.png"></p>  

点击finish完成发布工作，发布后在Eclipse中会自动打开发布的项目
    
以上就是通过Eclipse和Tomcat发布web应用的全过程。   

##LAMP配置

###简介
什么是LAMP

LAMP是一种Web网络应用和开发环境，是Linux, Apache, MySQL, Php/Perl的缩写，每一个字母代表了一个组件，每个组件就其本身而言都是在它所代表的方面功能非常强大的组件。

LAMP这个词的由来最早始于德国杂志“c't Magazine”，Michael Kunze在1990年最先把这些项目组合在一起创造了LAMP的缩写字。这些组件并不是开始就设计为一起使用的，但是，这些软件都是开源的，可以很方便的随时获得并免费使用，这就导致了这些组件经常在一起使用。这些组件的兼容性也在不断完善，为了改善不同组件之间的协作，已经创建了某些扩展功能，在一起的应用情形变得非常普便，因而成为目前最流行的web应用基础架构。

###LAMP的组件

平台由四个组件组成，呈分层结构，每一层都提供了整个架构的一个关键部分：

Linux：Linux 处在最底层，提供操作系统。它的灵活性和可定制化的特点意味着它能够产生一种高度定制的平台，让其它组件在上面运行。其它组件运行于Linux 之上，但是并不一定局限于 Linux，也可以在 Microsoft Windows, Mac OS X 或 UNIX上运行。

Apache：Apache位于第二层，它是一个Web 服务平台，提供可让用户获得 Web 页面的机制。Apache 是一款功能强大、稳定、可支撑关键任务的Web服务器，Internet 上超过 50％ 的网站都使用它作为 Web 服务器。

MySQL：MySQL 是最流行的开源关系数据库管理系统，是LAMP的数据存储端。在 Web 应用程序中，所有帐户信息、产品信息、客户信息、业务数据和其他类型的信息都存储于数据库中，通过 SQL 语言可以很容易地查询这些信息。

PHP：PHP 是一种被广泛应用的开放源代码的多用途脚本语言，它可嵌入到 HTML中，尤其适合 web 开发。可以使用 PHP 编写能访问 MySQL 数据库中的数据和 Linux 提供的一些特性的动态内容。

###配置过程

具体配置过程详见：<a href="http://www.cnblogs.com/mchina/archive/2012/11/28/2778779.html">CentOS 6.3下源码安装LAMP(Linux+Apache+Mysql+Php)环境</a>