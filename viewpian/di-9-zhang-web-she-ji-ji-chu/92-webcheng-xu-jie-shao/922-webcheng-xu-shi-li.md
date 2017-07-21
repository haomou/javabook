### 9.2.2 WEB程序实例

为了帮助读者理解，这里给出一个WEB程序实例，同时希望读者学习使用IDE快速开发WEB应用程序。目前开发WEB程序的IDE主要有MyEclipse和NetBeans，两者各有优劣之处，作者使用的是NetBeans最新版本。 

首先打开NetBeans，新建项目，选择Java Web&gt;&gt; Web应用程序，点击下一步，填入项目名称和项目目录，点击下一步，服务器选择 Tomcat， Java EE 选择Java EE5，进入下一步，本例只是简单地Servlet示例，不需要添加框架，直接点击下一步，新建项目完成。如下图9-6所示。

![](/assets/9-6.png)

如上图所示，新建项目后，你会发现源包内容是空的，这时新建包并新建文件MyServlet类，Servlet类用于提供服务，需要继承自 HttpServlet。重写覆盖 doGet 与 doPost 方法如下：

```
public class MyServlet extends HttpServlet {
     @Override
     public void doGet(HttpServletRequest request,HttpServletResponse response) throws ServletException,IOException 
     {
           PrintWriter out = response.getWriter(); //客户端对象 out
           out.write("<html>"); 
           out.write("<head>");
           out.write("<title>Wangwang Servlet Demo</title>");
           out.write("</head>");
           out.write("<body>");
           out.write("this is get Method, I'm bailang hello!");
           out.write("</body>");
           out.write("</html>");
           System.out.println("这里是服务器端打印，在 tomcat 控制台查看");
     }
     @Override
     public void doPost(HttpServletRequest request,HttpServletResponse response) throws ServletException,IOException 
     {
           PrintWriter out = response.getWriter();
           out.write("<html>");
           out.write("<head>");
           out.write("<title>Wangwang Servlet Demo</title>");
           out.write("</head>");
           out.write("<body>");
           out.write("this is post Method, I'm bailang hello!");
           out.write("</body>");
           out.write("</html>");
     }
}
```

 然后在web.xml中配置Servlet，以拦截请求，在之前增加如下内容：

```
<servlet>
    <servlet-name>myServlet</servlet-name>//servlet 标示符
    <servlet-class>com.test.MyServlet</servlet-class>//packageName+classname 不能改变
</servlet>
<servlet-mapping>
    <servlet-name>myServlet</servlet-name>//servlet 标示符，与上面保持一致
    <url-pattern>/myServlet</url-pattern>//匹配 URL 路径
    <url-pattern>/myServlet1</url-pattern>//支持匹配多个 URL 路径
</servlet-mapping>
```

此时，一个Servlet程序已经编写完了，在右栏项目上单击右键选择清理并构建，NetBeans会在项目目录中dist目录下生成.war文件，可以将该目录拷贝到上面介绍的WEB容器的webapps目录下，然后启动服务器即可自动部署。然而在NetBeans中我们可以直接在右栏项目上点击右键选择部署，即可启动Tomcat并自动部署。通过访问[http://127.0.0.1:8080/myServlet](http://127.0.0.1:8080/myServlet)或 [http://127.0.0.1:8080/myServlet1](http://127.0.0.1:8080/myServlet1)即可看到输出内容，关于WEB程序的访问和应答模式我们在下一节将详细讲解。

