### 10.1.2  ServletConfig接口介绍

GenericServlet实现了ServletConfig接口，而且细心地读者可能会发现Servlet中init\(\)方法的参数是ServletConfig接口。Config即配置的意思， GenericServlet就是Servlet配置。ServletConfig包含web.xml中配置的Servlet节点的信息。

封装一个&lt;servlet&gt;节点配置的所有信息，有三个重要方法：

servletConfig.getServletName\(\)：得到 servletName 

servletConfig.getInitParameter\(“username”\)：得到初始化参数值 

servletConfig.getServletContext\(\)：得到ServletContext类的实例application对象。

关于在 web.xml 中的配置方法如下，在&lt;/WebApp&gt;之前添加如下内容：

```
<servlet> 
    <servlet-name>myServlet</servlet-name>//servlet 标示符
    <servlet-class>com.test.MyServlet</servlet-class>
    <init-param>
        <paraName>username</paraName>
        <paraValue>chero</paraValue>
    </init-param>
    <init-param>
        … …
    </init-param>
</servlet>
<servlet-mapping>
    <servlet-name>myServlet</servlet-name>//servlet 标示符，与上面保持一致
    <url-pattern>/myServlet</url-pattern>//匹配URL路径
</servlet-mapping>
```

 要获取初始化参数，可以利用getInitParameterNames方法，使用示例如下：

```
Enumeration<String> names = config.getInitParameterNames();
while (names.hasMoreElements()) {
    String name = names.nextElement();
    System.out.println(name + " = " + config.getInitParameter(name));
}
```



