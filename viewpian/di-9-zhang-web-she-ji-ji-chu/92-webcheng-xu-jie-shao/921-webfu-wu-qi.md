### 9.2.1 WEB服务器

目前支持 JSP/Servlet 的 WEB服务器有很多，比较常用的有 GlassFish， Jetty，Tomcat 等，作者比较常用的是Tomcat服务容器，7.0.29以上版本已支持 Web Socket 通信，程序员们可以借此开发网页聊天等更 强大功能的程序。目前最新版本为9.0.0.M17 \(alpha\)。下面主要介绍 Tomcat 服务器，其它服务容器类似。 

Tomcat最初是由Sun公司的软件构架师詹姆斯·邓肯·戴维森开发的。 后来变为开源项目，并由Sun贡献给Apache软件基金会。Tomcat 是JSP/Servlet规范的一个实现；是WebServer的一种,它又称为Servlet引擎， WEB包容器。它的运行只需要jre\(jdk 中包含 jre\),它有多个OS版本，可跨平台，最重要的是Tomcat 是由 java 开发，因此兼容性相当好。 

在安装使用Tomcat之前，用户必须先配置好JAVA环境变量，因为Tomcat中并不包含JRE。下面我们介绍如何使用Tomcat。

* 下载Tomcat，进入官网：[http://tomcat.apache.org](http://tomcat.apache.org)，下载对应操作系统的软件包。 
* 解压文件，进入bin目录，Windows系统双击startup.bat 启动Tomcat， Linux系统执行./startup.sh启动Tomcat，Windows系统会弹出控制台窗口，输出信息。 
* 打开浏览器，在地址栏中输入：[http://127.0.0.1:8080](http://127.0.0.1:8080)，则会显示Tomcat欢迎界面。

#### Tomcat目录说明

bin 目录：存放 tomcat 的启动和关闭的命令。 

conf 目录：存放 tomcat 的配置文件。 

lib 目录：tomcat 运行所需要的 jar 包。 

logs 目录：tomcat 运行产生的日志文件。 

temp 目录：存放临时文件。 

webapps 目录：Tomcat 的主要 Web 发布目录，默认情况下把.war 文件 放于此目录。 

work 目录：存放 JSP 编译后产生的 class 文件。

#### Tomcat配置说明

 1. 配置端口：conf目录下的server.xml文件，如下行：

&lt;Connector enableLookups="false" port="80" protocol="HTTP/1.1" redirectPort="8443"/&gt;

 其中：port项配置监听端口号。

 2. Tomcat管理账户：conf目录下的tomcat-users.xml文件，配置如下：

Tomcat6：&lt;user username="admin" password="" roles="admin,manager"/&gt;

Tomcat7：

&lt;role rolename="manager-gui"/&gt;配置角色

&lt;user username="admin" password="" roles="manager-gui"/&gt;配置用户 

3. 用户开发的WEB应用程序放置在webapps目录下 

4. Work中是临时文件，包括jsp转译后生成的servlet代码，编译后生成的class类文件等。





