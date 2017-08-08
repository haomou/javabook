## 10.2 JSP详解

JSP（Java Server Pages）是由Sun Microsystems公司倡导、许多公司参与一起建立的一种动态网页技术标准。JSP技术有点类似 ASP技术，它是在传统的网页HTML文件\(\*.htm,\*.html\)中插入Java程序段\(Scriptlet\)和JSP标记\(tag\)，从而形成JSP文件\(\*.jsp\)。用 JSP开发的Web应用是跨平台的，既能在Linux下运行，也能在其他操作系统上运行，它是建立在servlet规范之上，现在版本为 2.5（servlet3.0，jsp2.5）。

下面先给出一个JSP示例：

```
<%@ page language="java" contentType="text/html; charset=utf-8" import="java.util.Date,java.text.DateFormat,java.text.SimpleDateFormat"%>
<html>
<head>
    <title>第一个 jsp 页面</title>
</head>
<body>
    <% DateFormat df = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
    Date nowDate = new Date(); %>
    现在时间是:<%= df.format(nowDate) %>
</body>
</html>
```

**说明：**

* &lt;%@ page %&gt;是指令元素，language是page指令的属性，表示使  用的语言，只能是java，contextType表示本文档的类型，charset指定编码  类型，import表示导入本页面使用的java类。
* &lt;% %&gt;之间嵌入的是一般的JAVA代码程序。
* &lt;%= %&gt;是输出表达式，在页面打印“=“后面的表达式结果。

JSP规范是建立在Servlet规范之上的，其实JSP本质上就是Servlet， 这是因为每个JSP都会转译为Servlet。 我们将上面的程序保存为 test.jsp，放入Tomcat的webapps目录下新建test目录，在conf/Catalina/localhost目录下新建test.xml文件，内容如下：

```
<?xml version="1.0" encoding="UTF-8"?>
<Context antiJARLocking="true" docBase="/test" path="/test">
    <Manager className="org.apache.catalina.session.PersistentManager" saveOnRestart="false">
        <Store className="org.apache.catalina.session.FileStore"/>
    </Manager>
</Context>
```

其中，docBase指定相对于webapps目录的相对路径，当然也可以写绝对路径，path指定访问的URL相对路径。然后启动Tomcat，待系统部署完毕之后，访问[http://127.0.0.1:8088/test/test.jsp](http://127.0.0.1:8088/test/test.jsp)，即可看到页面显示：

现在时间是:2012-10-16 08:46:21

进入tomcat的work目录，这个目录存放的临时文件，包括jsp转译后的servlet文件。打开work\Catalina\localhost\test\org\apache \jsp目录，发现有两个文件：

test\_jsp.class               test\_jsp.java

test\_jsp.java就是JSP文件转译生成的Servlet类。然后这个java类经过编译变为test\_jsp.class文件，所以我们请求执行的本质上是 test\_jsp.class文件。访问运行流程如下图10-4所示:

![](/assets/10-4.png)

第一次请求：

* 第一步:首先将jsp转译为.java;
* 第二步：把java编译为class。因为存在这样的过程，所以第一访问部署的jsp比较慢。

第二次请求：不存在转译与编译的过程直接访问上次生成的class类， 速度变快。





