### 10.2.1 JSP页面标签

一般的JSP文件有3部分组成：HTML模版，元素，注释。

#### **HTML模板**

HTML模版一般指的是开发是由美工人员提供的HTML页面，这是一个静态页面，内容为基本的HTML代码。

#### **元素**

元素分为 3 种，包括脚本元素，指令元素与动作元素。

* **脚本元素，**一般包含3种形式：声明，表达式，小脚本。

1.声明，声明中一般用来声明一个变量或方法。它的代码在中，记住有个感叹号。一般声明很少使用，更不会声明方法，如果需要方法，我们一般封装在JavaBean中，需要的时候访问调用。

2.表达式，表达式最后没有分号，其效果可以用小脚本中的out对象打印代替。

```
a= <%= a %> out: <%out.print(a);%><br>
b = <%= b %> out: <%out.print(b);%><br>
10+20=<%= sum(10, 20)%> out: <%out.print(sum(10, 20));%>
```

3.小脚本，其中编写的就是普通的java代码。包括流程控制等语句。注意：在声明与小脚本中都可以声明变量。区别：转译后的java 类不同，声明部分声明的变量属于转译后的java类是全局的；小脚本声明的变量属于\_jspService 方法，是局部的。

* 指令元素，一些影响整个JSP页面的属性设置，比如编码格式等。 JSP指令的语法为:        

```
<%@ 指令名称 属性 1="属性值 1" … 属性 n="属性值 n"%>  
<%@ 指令名称 属性 n="属性值 n"%>  
```

指令元素包括3种指令，page指令，include指令，taglib指令。

1.page指令

page指令用于定义JSP文件中的全局属性，\[\]表示属性可选。格式：

```
<%@ page [language="脚本语言种类”] [import="包或类"]
[contentType="MIME 类型"] [session="true/false"] [buffer="缓冲区
大小"] [autoFlash="true/false"] [isThreadSafe="true/false"]
[info="text"] [errorPage="异常事件页面 URL"]
[isErrorPage="true/false"] %>
```

**language：**定义页面使用的脚本语言，默认值为Java

**import：**用于导入一些JSP页面中要用到的Java包或类，可以有多个，用 ","隔开，默认情况下自动导入java.lang.\*, javax.servlet.\*, javax.servlet.jsp.\* , javax.servlet.http.\* 

**contentType：**设置JSP页面的MIME类型，默认值为"type='text/html;charset=ISO-8859-1'"， 设置值的方式为"MIME类型"或"MIME类型;charset=编码" 

**session：**设置是否允许JSP页面中使用session对象和session有效范围内的对象。 

**buffer：**它的值为none或指定的数字，用于设置输出缓冲区的大小，默认值为8Kb值为none表示没有缓冲。 

**autoFlash：**设置当缓冲区已满时，是否会自动刷新缓冲区，如果值为false，当缓冲区溢出时就会出现异常;当buffer的值为none 时，此属性的值不能设为false,此属性的默认值为true

**isThreadSafe：**设置JSP页面是否可以多线程访问，如果为true， 则此JSP页面可同时响应多个客户请求，如果值为false,则在某个时刻内只能处理一个客户的请求，此属性默认值为true 

**info：**设置JSP页面的信息字符串

**errorPage：**指出当出现异常时转向页面的URL 

**isErrorPage：**设置当前页面是否为出错页面，如果为true则可以使用exception对象，否则不行，默认值false

2. include指令

使用include指令可以在JSP中包含一个静态的文件，同时解析这个文件中的JSP语句。 格式：

```
<%@ include file="relativeURL" %>
<%@ include file="相对位置" %>
```

说明：包含的file文件的路径一般都是相对路径，不需要端口、 协议或域名，如"error.jsp"，"/templates/onlinestore.html"， "/beans/calendar.jsp"等。包含文件中不能使用&lt;html&gt;、&lt;/html&gt;、&lt;body&gt;、&lt;/body&gt; 标记，因为这将会影响原 JSP 文件中同样的标记， 有时会导致错误。

3. taglib指令

定义一个标签库及其自定义标签的前缀。 格式：

```
<%@ taglib uri="URIToTagLibrary" prefix="tagPrefix" %>
```

例子：

```
<%@ taglib uri="WEB-INF/struts-html.tld" prefix="html" %>
```

说明： uri：可以是一个相对或绝对路径prefix：在自定义标签之前的前缀，比如中的public， 如果这里不写public，那么就是不合法的。请不要使用jsp、jspx、 java、javax、servlet、sun和sunw作为前缀，已被sun公司声明保留。

* ** 动作元素：** JSP动作利用XML语法格式的标记来控制Servlet引擎的行为。利用JSP动作可以动态地插入文件、重用 JavaBean组件、把用户重定向到另外的页面、为Java插件生成HTML代码。JSP动作包括：

```
jsp:include：在页面被请求的时候引入一个文件。
jsp:useBean：寻找或者实例化一个JavaBean。
jsp:setProperty：设置JavaBean的属性。
jsp:getProperty：输出某个JavaBean的属性。
jsp:forward：把请求转到一个新的页面。
jsp:plugin：根据浏览器类型为Java插件生成OBJECT或EMBED标记。
```

 1. jsp:include动作，该动作把指定文件插入正在生成的页面。其语法如下：

```
＜jsp:include page="relative URL" flush="true" /＞
```

前面已经介绍过include指令，它是在JSP文件被转换成Servlet的时候引入文件，而这里的jsp:include动作不同，插入文件的时间是在页面被请求的时候。jsp:include动作的文件引入时间决定了它的效率要稍微差一点，而且被引用文件不能包含某些JSP代码（例如不能设置HTTP头）， 但它的灵活性却要好得多。如下例在test.jsp页面引入其他页面。

```
＜!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN"＞
＜html＞
＜head＞
    ＜title＞test＜/ title＞
＜/head＞
＜body＞
    ＜ol＞
        ＜li＞＜jsp:include page="news/Item1.html" flush="true"/＞
        ＜li＞＜jsp:include page="news/Item2.html" flush="true"/＞
    ＜/ol＞
＜/body＞
＜/html＞
```



