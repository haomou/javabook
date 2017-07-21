## 9.2 WEB程序介绍

JSP，Servlet是由Sun公司制定的用java 开发WEB 应用程序的规范，并且JSP规范建立在Servlet规范之上（先有Servlet规范后有jsp规范， jsp本质上就是Servlet）。目前最新版本为Servlet4.0，JSP2.4。

* **SERVLET： **Servlet是一个可以部署到webServer可以被客户端访问的Java类。
* **JSP：** JavaServerPage的简写,文件后缀为jsp。JSP页面相当于DHTML\(html+css+js\)+JAVA，编译时JSP被编译成Servlet。

规范是由Sun公司制定的，其目的是形成一种编程技术规范，让从事JAVA开发WEB应用程序的公司都遵循这样一种规范。而实际上我们开发出来的WEB应用程序是不能直接执行的，必须部署到WEB服务器，通过访问网页的形式才可执行，那么既然要通过WEB服务器解析，服务器是不是也要实现该规范呢？答案是肯定的，其关系如下图9-5所示。

![](/assets/9-5.png)

