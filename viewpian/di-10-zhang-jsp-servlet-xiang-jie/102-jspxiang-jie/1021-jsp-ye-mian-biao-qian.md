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

1. include指令

使用include指令可以在JSP中包含一个静态的文件，同时解析这个文件中的JSP语句。 格式：

```
<%@ include file="relativeURL" %>
<%@ include file="相对位置" %>
```

说明：包含的file文件的路径一般都是相对路径，不需要端口、 协议或域名，如"error.jsp"，"/templates/onlinestore.html"， "/beans/calendar.jsp"等。包含文件中不能使用&lt;html&gt;、&lt;/html&gt;、&lt;body&gt;、&lt;/body&gt; 标记，因为这将会影响原 JSP 文件中同样的标记， 有时会导致错误。

1. taglib指令

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
jsp:plugin：根据浏览器类型为Java插件生成OBJECT或EMBED标记
```

1.jsp:include动作，该动作把指定文件插入正在生成的页面。其语法如下：

```
<jsp:include page="relative URL" flush="true" />
```

前面已经介绍过include指令，它是在JSP文件被转换成Servlet的时候引入文件，而这里的jsp:include动作不同，插入文件的时间是在页面被请求的时候。jsp:include动作的文件引入时间决定了它的效率要稍微差一点，而且被引用文件不能包含某些JSP代码（例如不能设置HTTP头）， 但它的灵活性却要好得多。如下例在test.jsp页面引入其他页面。

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
<html>
<head>
    <title>test</title>
</head>
<body>
    <ol>
        <li><jsp:include page="news/Item1.html" flush="true"/></li>
        <li><jsp:include page="news/Item2.html" flush="true"/></li>
    </ol>
</body>
</html>
```

2.jsp:useBean动作，用来装载一个将在JSP页面中使用的JavaBean。 这个功能非常有用，因为它使得我们既可以发挥Java组件重用的优势，同时也避免了损失JSP区别于Servlet的方便性。jsp:useBean动作最简单的语法为：

```
<jsp:useBean id="name" class="package.class" />
```

这行代码的含义是：“创建一个由class属性指定的类的实例，然后把它绑定到其名字由id属性给出的变量上”。不过，就象我们接下来会看到的，定义一个scope属性可以让Bean关联到更多的页面。此时，jsp:useBean动作只有在不存在同样id和scope的 Bean时才创建新的对象实例，同时， 获得现有Bean的引用就变得很有必要。 获得Bean实例之后，要修改Bean的属性既可以通过 jsp:setProperty动作进行，也可以在Scriptlet中利用id属性所命名的对象变量，通过调用 该对象的方法显式地修改其属性。这使我们想起，当我们说“某个Bean有一个类型为X的属性foo”时，就意味着“这个类有一个返回值类型为X的getFoo方法，还有一个setFoo方法以X类型的值为参数”。

有关jsp:setProperty动作的详细情况在后面讨论。但现在必须了解的是，我们既可以通过jsp:setProperty动作的value属性直接提供一个值，也可以通过param属性声明Bean的属性值来自指定请求参数，还可以列出Bean属性表明它的值应该来自请求参数中的同名变量。 

在JSP表达式或Scriptlet中读取Bean属性通过调用相应的getXXX方法实现，或者更一般地，使用jsp:getProperty动作。 

注意：包含Bean的类文件应该放到服务器正式存放Java类的目录下， 而不是保留给修改后能够自动装载的类的目录。例如，对于Java Web Server来说，Bean和所有Bean用到的类都应该放入classes目录，或者封装进jar文件后放入lib目录，但不应该放到servlets下。

下面是一个很简单的例子，它的功能是装载一个Bean，然后设置/读取它的message属性。

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN"＞
<html>
<head>
    <title>test</title>
</head>
<body>
    <jsp:useBean id="test" class="com.test.TestBean" />
    <jsp:setProperty name="test" property="message" value="hi!" />
    <h1>
        Message:
        <jsp:getProperty name="test" property="message" />
    </h1>
</body>
</html>
```

 该页面用到了一个TestBean，TestBean的代码如下：

```
package com.test;
public class TestBean {
    private String message = "No message";
    public String getMessage() { 
        return(message);
    }
    public void setMessage(String message) {
        this.message = message;
    }
}
```

 使用Bean最简单的方法是先用下面的代码装载Bean：

```
 <jsp:useBean id="name" class="package.class" />
```

然后通过jsp:setProperty和jsp:getProperty修改和提取Bean的属性。 不过有两点必须注意。 

第一，我们还可以用下面这种格式实例化Bean：

```
<jsp:useBean ...>
Body
</jsp:useBean>
```

说明：只有当第一次实例化Bean时才执行Body部分，如果是利用现有的Bean实例则不执行Body部分。正如下面将要介绍的，jsp:useBean并非总是意味着创建一个新的Bean实例。 

第二，除了id和class外，jsp:useBean还有其他三个属性，即：scope， type，beanName。下面简要说明这些属性的用法。 

**id 属性，**命名引用该Bean的变量。如果能够找到id和scope相同的 Bean实例，jsp:useBean动作将使用已有的Bean实例而不是创建新的实例。

**class属性，**指定Bean的完整包名路径。 

**scope属性，**指定Bean在哪种上下文内可用，可以取下面的四个值之一：page，request，session和application。 默认值是 page，表示该Bean只在当前页面内可用（保存在当前页面的PageContext内）。 request表示该Bean在当前的客户请求内有效（保存在ServletRequest对象内）。 session表示该Bean对当前HttpSession内的所有页面都有效。最后，如果取值 application，则表示该Bean对所有具有相同ServletContext的页面都有效。scope之所以很重要，是因为jsp:useBean只有在不存在具有相同id和scope的对象时才会实例化新的对象；如果已有id和scope都相同的对象则直接使用已有的对象，此时 jsp:useBean开始标记和结束标记之间的任何内容都将被忽略。

**type属性，**指定引用该对象的变量的类型，它必须是Bean类的名字、 超类名字、该类所实现的接口名字之一。请记住变量的名字是由id属性指定的。 

**beanName属性，**指定Bean的名字。如果提供了type属性和beanName属性，允许省略class属性。

3. jsp:setProperty动作，jsp:setProperty用来设置已经实例化的Bean对象的属性，有两种用法。

首先，你可以在jsp:useBean元素的外面（后面）使用jsp:setProperty， 如下所示：

```
<jsp:useBean id="myName" ... />
 ...
<jsp:setProperty name="myName" property="someProperty" ... />
```

此时，不管jsp:useBean是找到了一个现有的Bean，还是新创建了一个Bean实例，jsp:setProperty都会执行。 

第二种用法是把 jsp:setProperty放入jsp:useBean元素的内部，如下所示：

```
<jsp:useBean id="myName" ... >
 ...
<jsp:setProperty name="myName" property="someProperty" ... /></jsp:useBean>
```



