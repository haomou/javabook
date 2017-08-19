### 10.2.2 JSP内置对象

JSP有9大内置对象，分别是：Request，Response，Out，Session， Application，Cookie，Config，Page，Exception。下面分别一一介绍：

* **Request对象**

该对象封装了用户提交的信息，通过调用该对象相应的方法可以获取 封装的信息，即使用该对象可以获取用户提交的信息。如果 Request对象 获取客户提交的汉字字符时，会出现乱码问题，必须进行特殊处理。

首先，将获取的字符串用ISO-8859－1进行解码，并将解码结果保存 到一个字节数组中，然后再将这个数组转化为字符串对象即可。如下：

```
String textContent=request.getParameter("boy");
byte b[]=textContent.getBytes("ISO-8859-1");
textContent=new String(b);
```

Request常用的方法简介：

getParameter\(String strTextName\) 获取表单提交的信息。示例：

```
String strName＝request.getParameter("name");
```

 getProtocol\(\) 获取客户使用的协议。 示例：

```
String strProtocol=request.getProtocol();
```

 getServletPath\(\) 获取客户提交信息的页面。 示例：

```
String strServlet=request.getServletPath();
```

 getMethod\(\) 获取客户提交信息的方式，get\|post。 示例：

```
String strMethod = request.getMethod();
```

 getHeader\(\) 获取HTTP头文件中的accept、accept-encoding和Host的值。 示例：

```
String strHeader = request.getHeader("accept");
```

 getRermoteAddr\(\) 获取客户的 IP 地址。 示例：

```
String strIP = request.getRemoteAddr();
```

 getRemoteHost\(\) 获取客户机的名称。 示例：

```
String clientName = request.getRemoteHost();
```

 getServerName\(\) 获取服务器名称。 示例：

```
String serverName = request.getServerName();
```

 getServerPort\(\) 获取服务器的端口号。 示例：

```
int serverPort = request.getServerPort();
```

 getParameterNames\(\) 获取客户端提交的所有参数的名字。 示例：

```
Enumeration enum = request.getParameterNames();
while(enum.hasMoreElements()){
    String s=(String)enum.nextElement();
    out.println(s);
}
```

* **Response对象**

 对客户的请求做出动态的响应，向客户端发送数据。常用如下两种情况：

1. 动态响应contentType属性当一个用户访问一个JSP页面时，如果该页面用page指令设置页面的contentType属性时text/html，那么JSP引擎将按照这个属性值做出反应 。 如果要动态改变这换个属性值来响应客户，就需要使用Response对象的 setContentType\(String s\)方法来改变contentType的属性值。 格式：response.setContentType\(String s\); 参数 s 可取 text/html,application/x-msexcel,application/msword等。 
2. Response 重定向在某些情况下，当响应客户时，需要将客户重新引导至另一个页面， 可以使用Response的 sendRedirect\(URL\)方法实现客户的重定向。例如：response.sendRedirect\("index.jsp"\);

* ** Session 对象**

Session对象是一个JSP内置对象，它在第一个JSP页面被装载时自动创建，完成会话期管理。从一个客户打开浏览器并连接到服务器开始，到客户关闭浏览器离开这个服务器结束，被称为一个会话。当一个客户访问一个服务器时，可能会在这个服务器的几个页面之间切换，服务器应当通过某种办法知道这是一个客户，就需要Session对象。

当一个客户首次访问服务器上的一个JSP页面时，JSP引擎产生一个Session对象，同时分配一个String类型的ID号，JSP引擎同时将这换个ID号发送到客户端，存放在Cookie中，这样Session对象，直到客户关闭浏览器后，服务器端该客户的Session对象才取消，并且和客户的会话对应关系消失。当客户重新打开浏览器再连接到该服务器时，服务器为该客户再创建一个新的Session对象。常用方法如下：

| 方法名 | 功能 |
| :--- | :--- |
| public String getId\(\)  | 获取Session对象编号 |
| public void setAttribute\(String key,Object obj\)  | 设置session属性，key/object |
| public Object getAttribute\(String key\) | 获取Session对象指定key属性值 |
| public Boolean isNew\(\) | 判断是否是一个新session |
| public void invalidate\(\) | 销毁session |

* **Application对象**

服务器启动后就产生了这个Application对象，当客户再所访问的网站的各个页面之间浏览时，这个Application对象都时同一个，直到服务器关闭。但是与Session对象不同的时，所有客户的Application对象都时同一个，即所有客户共享这个内置的Application对象。常用方法如下：

| 方法名 | 功能 |
| :--- | :--- |
| setAttribute\(String key,Object obj\)  | 设置Application属性，key/object |
| getAttribute\(String key\) | 获取Session对象指定key属性值 |

* **Out对象**

 Out对象时一个输出流，用来向客户端输出数据。Out对象用于各种数据的输出。其常用方法如下：

| 方法名 | 功能 |
| :--- | :--- |
| out.print\(\) | 输出各种类型数据 |
| out.newLine\(\) | 输出一个换行符 |
| out.close\(\) | 关闭流 |
| void clear\(\) | 除输出缓冲区的内容，但是不输出到客户端 |
| void clearBuffer\(\) | 清除输出缓冲区的内容，并输出到客户端 |
| void flush\(\) | 输出缓冲区里面的数据。 |
| int getBufferSize\(\) | 取以kb为单位的目前缓冲区大小。 |
| int getRemaining\(\) | 取以kb为单位的缓冲区中未被占用的空间大小。 |
| boolean isAutoFlush\(\) | 是否自动刷新缓冲区。 |

* **Config对象**

 配置对象，config对象用来存放Servlet初始的数据结构。常用方法：

| 方法名 | 功能 |
| :--- | :--- |
| String getInitParameter\(String name\)  | 返回名称为name的促使参数的值。 |
| Enumeration getInitParameters\(\) | 返回这个JSP所有的促使参数的名称集合。 |
| ServletContext getContext\(\) | 返回执行者的servlet上下文。 |
| String getServletName\(\) | 返回servlet的名称。 |

* **Page对象**

JSP网页本身，page对象是当前页面转换后的Servlet类的实例。从转换后的Servlet类的代码中，可以看到这种关系：Object page= this;在JSP页面中，很少使用page对象。

* **PageContext对象**

页面上下文对象，JSP引入了一个名位PageContext的类，通过它可以访问页面的许多属性。PageContext类拥有getRequest，getResponse，getOut， getSession等方法，pageContext变量存储与当前页面相关联的PageContext对象的值。如果方法需要访问多个与页面相关的对象，传递pageContext要比传递request，response，out等的独立引用更容易（虽然两种方式都能达到同样的目的）。常用方法如下：

| 方法名 | 功能 |
| :--- | :--- |
| void setAttribute\( String name, Object value, int scope \) ;voidsetAttribute\( String name, Object value \) | 在指定的共享范围内设置属性 |
| Object getAttribute\( String name, int scope \) ;Object getAttribute\( String name \)  | 取得指定共享范围内以name为名字的属性值 |
| Object findAttribute\( String name \)  | 按页面、请求、会话和应用程序共享范围搜索已命名的属性 |
| void removeAttribute\( String name, int scope \) ;void removeAttribute\( String name \)  | 移除指定名称和共享范围的属性 |
| void forward\( String url \) ; | 将页面导航到指定的URL |
| Enumeration getAttributeNamesScope\( int scope \)  | 取得指定共享范围内的所有属性名称的集合 |
| int getAttributeScope\( String name \) | 取得指定属性的共享范围 |
| ErrorData getErrorDate\(\) | 取得页面的errorData对象 |
| Exception getException\(\) | 取得页面的exception对象 |
| ExpressionEvaluator getExpressionEvaluator\(\) | 取得页面的expressionEvaluator对象 |
| JspWriter getOut\(\) | 取得页面的out对象 |
| Object getPage\(\) | 取得页面的page对象 |
| ServletRequest getRequest\(\) | 取得页面的request对象 |
| ServletResponse getResponse\(\) | 取得页面的response对象 |
| ServletConfig getConfig\(\) | 取得页面的config对象 |
| ServletContext getServletContext\(\) | 取得页面的servletContext对象 |
| HttpSession getSession\(\) | 取得页面的session对象 |
| VariableResolver getVariableResolver\(\) | 取得页面的variableResolver对象 |
| void include\(String url, boolean flush\)；void include\(String url\) | 包含其他的资源，并指定是否自动刷新 |



