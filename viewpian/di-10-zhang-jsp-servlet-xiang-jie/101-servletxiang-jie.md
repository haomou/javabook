## 10.1 Servlet详解

前面介绍了WEB访问应答机制，并给出了一个Servlet示例，相信读者对于这块知识应该有了整体的认识，下面我们将详细讲解Servlet部分的知识，首先看一下Servlet类与普通Java类的区别，如下表10-1所示。

**表10-1 Servlet类与Java类**

| **Servlet类** | **Java类** |
| :--- | :--- |
| 继承HttpServlet | 一般继承Object类 |
| 必须在WebServer中才能运行 | 不需要WebServer支持也能运行 |
| 可以处理客户端请求 | 不能处理客户端请求 |
| 启动不需要main函数 | 启动需要main函数 |
| 由容器创建（new）实例 | 一般我们自己创建实例 |
| 由容器调用doGet或者doPost方法 | 程序员自己调用 |

 在JDK中Servlet的继承结构如下图10-1所示。

![](/assets/10-1.png)

一般我们自定义的Servlet继承自HttpServlet，其实我们也可以继承自GenericServlet或者实现Servlet接口，如果这样，就需要程序员做很多底层的工作，而这些工作HttpServlet已帮我们做好，所以Sun建议你继承自HttpServlet。

