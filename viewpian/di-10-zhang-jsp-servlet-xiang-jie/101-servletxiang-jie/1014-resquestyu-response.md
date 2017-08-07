### 10.1.4 Resquest与Response

在service方法中传入了一组参数HttpServletRequest和HttpServletResponse，由于B/S架构的程序是请求/应答模式，这种模式在 JAVA中对应的实体类就是如上的实现Http协议的类。request表示请求，其最重要的一个功能是封装客户端请求参数，它由 WebServer生成。前面提到Web应用程序必须部署到Web服务器中才能运行，WebServer提供对WebApp的支持，那提供了那些支持呢？（1）帮我们管理Servlet的生命周期（比如创建servlet对象，调用servlet的init,service,destroy等方法）；（2）帮我们生成 request的实例，它将客户端传过来的请求参数数据，放入到request对象的parameter参数当中，我们可以通过request的一些方法得到请求参数的数值。

关于WEB请求最常用的方法是使用表单和URL重写。 

懂一点html的读者都知道form标签，这个标签主要用于提交用户请求，并附加表单中的信息，格式如下：

```
<form action="/MyServlet" method="get">
    UserName:<input name="userName"><br>
    Money:<input name="money"><br>
    <input type="submit" value="提交">
</form>
```

其中请求的URL由action属性值指定，请求方法由method属性值指 定，请求参数就是表单中填写的信息。Input标签中的name属性指定参数名，输入的值为该参数值，当点击提交按钮，向服务器发送请求，并附加参数信息。当form表单是get请求时Servlet端调用doGet方法，post请求时调用doPost方法，默认是get请求。对于没有输入值的请求参数值返回“ ”字符串，对于根本不存在的请求参数返回null。

另外一种请求的方法是重写URL，就是在URL中带入参数信息，语法格式为：

```
http://202.38.73.47:8080/MyServlet?参数名 1=参数值 1&参数名 2=参数值
```

在使用form表单时，若使用get方法，我们也能在浏览器的地址栏看到这种请求格式，说明get方法也是采用URL带入参数的，但这种方法只适合传入少量参数。 但是在我们编写doGet或则doPost方法时，当我们不知道客户端请求参数名称时，也就无法得到起数值，这时我们可以利用request.getParameterNames\(\)方法得到客户端所有请求参数名称的集合。当然HttpServletRequest还有一些其他比较重要的方法，如下表10-2所示。

**表 10-2 HttpServletRequest常用方法**

| **方法** | **说明** |
| :--- | :--- |
| request.getContextPath\(\) | 得到web应用程序名称（虚拟路径），一般默认为项目名，创建项目时可以设置。 |
| request.getServletPath\(\) | 如果请求的是servlet，那么返回的该servlet在web.xml中配置的url-pattern；如果是jsp，返回jsp文件名。 |
| request.getRequestURI\(\) | 请求的相对路径，request.getContextPath\(\)+request.getServletPath\(\) |
| request.getRequestURL\(\) | 请求的全部路径，绝对路径 |
| request.getMethod\(\) | 请求类别，默认是get请求，只有使用form表单提交才可以使用post请求 |
| request.getRemotePort\(\) | 客户端请求端口 |
| request.getRemoteAddr\(\) | 得到客户端的IP地址 |
| request.getServerName\(\) | 得到服务器名称 |
| request.getServerPort\(\) | 得到服务器端口号 |
| request.getRealPath\(“/”\) | 得到当前Web应用程序的绝对路径 |
| request.getHeader\("User-Agent"\) | 得到客户端浏览器的信息 |
| request.getRequestDispatcher\("&lt;url-pattern&gt;"\) | 得到请求转发对象 |
| request.getHeaderNames\(\) | 得到所有请求头名称的Enumeration |

Service方法中的HttpServletResponse对象主要用于向客户端发送数据， 呈现响应内容。HttpServletResponse对象可以向客户端发送三种类型的数据:a.响应头 b.状态码 c.数据。

* 设置响应头主要是控制客户端的编码方式，有两种方法如下，它们作  用相同。
  response.setContentType\("text/html;charset=UTF-8"\);
  response.setHeader\("Content-type","text/html;charset=UTF-8"\);

* 在向客户程序发送任何文档内容之前调用方法设置状态代码。可以使用HttpServletResponse接口的setStatus，sedRedirect或 sendError方法设置状态码。状态代码由3位数字组成，第一个数字定义了响应的类别,后面两位数字没有具体的分类。在servlet中建议使用HttpServletResponse中定义的常量来引用状态代码。1. 设置一般状态码可以使用setStatus（int）方法，参数可以为int 类型状态代码，也可以为HttpServletResponse中定义的常量；2.设置302和404状态代码：sendRedirect（String url）和 sendError  （int code，String msg）方法，二者会抛出IOException异常。

状态代码302命令浏览器连接到新的url。sendRedirect方法生成302响应及Location报头，给出新的url放入Location报头之前，系统自动将相对url转换为绝对url。状态代码404用于服务器没有找到文档的情况 。sendError方法发送状态代码及小段简短信息，信息被自动安排在HTML文档中发送给用户。

返回数据到客户端，可以使用2种方式向客户端写入信息。

1. 使用OutputStream向客户端写入数据，示例代码如下：

```
response.setHeader("Content-type","text/html;charset=UTF-8");
String data = "你好！";
OutputStream stream = response.getOutputStream();
stream.write(data.getBytes("UTF-8"));
```

 2. 使用Writer向客户端写入信息，示例代码如下：

```
response.setCharacterEncoding("UTF-8");
response.setHeader("Content-type","text/html;charset=UTF-8");
PrintWriter writer = response.getWriter();
writer.write("你好！");
```

还有一种比较常用的是下载文件，其示例代码如下：

```
String path = this.getServletContext.getRealPath(“/ 你好.jpg”);
String fileName = path.subString(path.lastIndexOf(“\\”));
Response.setHeader(“content-disposition”,”attachment;filename”+URLEncoder.encode(fileName,”UTF-8”));
//设置响应头，告诉浏览器，该响应是下载响应，如果文件名包含中文，必须使用 URL 编码
```



