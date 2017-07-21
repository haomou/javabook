###  9.2.1 WEB服务器

目前支持 JSP/Servlet 的 WEB服务器有很多，比较常用的有 GlassFish， Jetty，Tomcat 等，作者比较常用的是Tomcat服务容器，最近发行的7.0.29以上版本都已支持 Web Socket 通信，程序员们可以借此开发网页聊天等更 强大功能的程序。下面主要介绍 Tomcat 服务器，其它服务容器类似。 Tomcat 最初是由 Sun 公司的软件构架师詹姆斯·邓肯·戴维森开发的。 后来变为开源项目，并由 Sun 贡献给 Apache 软件基金会。Tomcat 是 JSP/Servlet 规范的一个实现；是 WebServer 的一种,它又称为 Servlet 引擎， WEB 包容器。它的运行只需要 jre\(jdk 中包含 jre\),它有多个 OS 版本，可 跨平台，最重要的是 Tomcat 是由 java 开发，因此兼容性应该相当好。 在安装使用 Tomcat 之前，用户必须先配置好 JAVA 环境变量，因为 Tomcat 中并不包含 JRE。下面我们介绍如何使用 Tomcat。

