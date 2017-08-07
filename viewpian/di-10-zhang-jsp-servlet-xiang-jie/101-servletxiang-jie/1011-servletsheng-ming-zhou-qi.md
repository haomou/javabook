### 10.1.1 Servlet生命周期

事物的生命周期指的是从事物的产生、发展、消亡的过程。在编程中有变量的生命周期，对象（类的实例）的生命周期。以前对象的创建，发展\(调用方法使用\)都是程序员用代码控制的，现在 Servlet的创建是由WebServer完成的。

Servlet接口中定义了五个与生命周期有关的方法，其源代码如下：

```
package javax.servlet;
import java.io.IOException;
public interface Servlet {
    public void init(ServletConfig config) throws ServletException;
    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException;
    public void destroy(); 
    public ServletConfig getServletConfig();
    public String getServletInfo();
}
```



