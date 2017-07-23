### 9.2.3 WEB访问与应答机制

本书之所以先给出JSP/Servlet示例，再讲解原理是为了让读者有一种先入为主的感觉，这样便于读者理解与入门。

用户在浏览器的地址栏中输入地址，或者填写表单上面的数据，然后 提交，当键入回车或者点击提交按钮之后，这些数据被送到了服务器上面， 这就需要有一个服务器的地址，服务器的地址就称为 URL（统一资源定位符），这样用户就可以请求（request）服务器上的资源。

当服务器收到用户的请求（request）之后，就会调用相应的程序来运行，程序运行的结果称为响应\(response\) , 这些结果就是一些 HTML标记（超文本），这些结果会从服务器发送到客户端，客户端浏览器接收这些数据，然后解析呈现出来，我们就最终看到了网页效果。浏览器与服务器之间通信的时候使用HTTP协议（超文本传输协议）来进行通信，协议就是规定，客户端与服务器端都必须遵守的约定。

#### URL解释

URL的组成部分如下图9-7所示。

![](/assets/9-7.png)

* **http：**说明采用协议
* **ip：**指定服务器的地址，在Internet上通常是域名，域名需要通过域 名服务器解析成IP地址，127.0.0.1表示本机ip。 
* **8080：**服务器的端口号，又叫服务号，监听号；Http协议默认的端口号是80端口，如果web服务器开启的是80端口，那么我们访问的时候，不需要使用端口号。 
* **应用程序目录：**可以用request.getContextPath\(\)获得,就是WebApp的名称，也称为虚拟路径。 
* **url-pattern： **就是servlet监听的url模式，可以用request.getServletPath\(\) 得到。

#### HTTP协议介绍

HTTP（HyperTextTransferProtocol）是超文本传输协议的缩写，它是分布式，协作式，超媒体系统应用之间的通信协议。是万维网（world wide web）交换信息的基础。该协议允许将超文本标记语言 \(HTML\)文档从 Web 服务器传送到Web浏览器。HTML是一种用于创建文档的标记语言，这些文档包含到相关信息的链接。您可以单击一个链接来访问其它文档、图像或多媒体对象，并获得关于链接项的附加信息。 

现在普遍使用的是1997年形成的HTTP/1.1，它除了比1.0传输数据更快，还提供了身份认证、状态管理和Cache 缓存等机制。只要你在浏览器上输入一个 URL ，最前面的http://就表示使用HTTP来访问指定位置的信息。 

HTTP协议访问机制如下图 9-8所示。

![](/assets/9-8.png)

从OSI（Open System Interconnection，开放系统互连）七层网络模型的层次上来看，数据在网络中的传输模型如下图 9-9 所示。

![](/assets/9-9.png)

HTTP由两部分组成：请求和响应。你在Web浏览器中输入一个URL时，浏览器将根据你的要求创建并发送请求，该请求包含所输入的 URL以及一些与浏览器本身相关的信息当服务器收到这个请求时将返回一个响应，该响应包括与该请求相关的信息以及位于指定 URL 的数据直到浏览器解析该响应并显示出网页为止。

HTTP请求的格式如下所示：

＜ request-line ＞ 请求行，用来说明请求类型，要访问的资源和 HTTP 版本 

＜ headers ＞ 请求头\(header\)，用来说明服务器要使用的附加信息（详见附录2） 

＜ blank line ＞ 空行 

＜ request-body ＞ 主体\(body\)，任意的其他数据

HTTP 协议的请求方法有 GET、POST、HEAD、PUT、DELETE、 OPTIONS、TRACE、CONNECT。这里介绍最常用的GET 方法和 POST方法。

**GET：**当客户端要从服务器中读取文档时，使用GET方法。GET方法要求服务器将URL定位的资源放在响应报文的数据部分，回送给客户端。 使用GET方法时，请求参数和对应的值附加在URL后面，利用一个问号（“?”）代表URL的结尾与请求参数的开始，传递参数长度受限制。例如， /index.jsp?id=100&op=bind。 

**POST：**当客户端给服务器提供信息较多时可以使用POST方法。POST方法将请求参数封装在 HTTP 请求数据中，以名称/值的形式出现，可以传输大量数据。

#### GET请求示例

```
GET / HTTP/1.1
Accept: */*
Accept-Language: zh-cn
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1;
SV1; .NET CLR 2.0.50727; .NET CLR 3.0.04506.648; .NET CLR
3.5.21022)
Host: www.google.cn
Connection: Keep-Alive
```

说明:请求的第一部分说明了该请求是一个GET请求.该行的第二部分是一个斜杠\(/\)，用来说明请求的是该域名的根目录。该行的最后一部分说明使用的是HTTP1.1版本\(另一个可选荐是 1.0\)。第2行是请求的第一个首部,HOST将指出请求的目的地。User-Agent,服务器端和客户端脚本都能访 问它,它是浏览器类型检测逻辑的重要基础.该信息由你的浏览器来定义,并 且在每个请求中自动发送。Connection,通常将浏览器操作设置为Keep-Alive。 第三部分,空行,即使不存在请求主体,这个空行也是必需的。

#### POST请求示例

```
POST / HTTP1.1
Host:www.wrox.com
User-Agent:Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1;SV1; .NET CLR 2.0.50727; .NET CLR 3.0.04506.648; .NET CLR 3.5.21022)
Content-Type:application/x-www-form-urlencoded
Content-Length:40
Connection: Keep-Alive
```

说明:请求行开始处的GET改为POST,以表示不同的请求类型。 Content-Type说明了请求主体的内容是如何编码的。浏览器始终以 application/x-www-form-urlencoded的格式编码来传送数据,这是针对简单URL编码的 MIME 类型。Content-Length说明了请求主体的字节数。最后请求主体.名称-值对的形式。

 HTTP 响应的格式如下所示：

＜ status-line ＞ 响应行，标识服务器端对客户端请求的处理结果，详见附录 3 

＜ headers ＞ 响应头，类似于请求头的 key：value 形式 

＜ blank line ＞ 空行 

＜ response-body ＞ 主体（body），任意的其他数据

 下面用telnet工具访问百度网页演示一下HTTP请求与相应过程，如下图9-10所示。

![](/assets/9-10.png)

如图中橘黄色线标注所示，该行为用户输入的命令，其中GET表示方法，/表示相对于[www.baidu.com:80](www.baidu.com:80)服务器的请求路径，HTTP/1.1表示采用的协议。 该演示中使用的是GET方法请求 URL为[http://www.baidu.com:80/](http://www.baidu.com:80/)， 使用的协议是HTTP/1.1，当然也可以用 HTTP/1.0。

橘黄色线以下部分为服务器的相应内容，默认访问[www.baidu.com:80/](www.baidu.com:80/)返回的是index.html页面，其中HTTP状态码 200,找到资源,并且一切正常。Date:生成响应的日期和时间。Content-Type:指定了MIME类型的HTML\(text/html\),编码类型是UTF-8。然后返回的是HTML文件代码。

