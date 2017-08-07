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

其中比较重要的方法为init（初始化）、service（提供服务）、destroy （销毁）。下面给出一个继承自HttpServlet的Servlet示例：

```
public class MyServlet2 extends HttpServlet {
    //构造方式是创建实例对象是调用
    public MyServlet2() {
        super();
        System.out.println("实例化:创建对象");
    }
    //创建对象后紧接执行初始化方法
    @Override
    public void init(ServletConfig config) throws ServletException {
        System.out.println("初始化,对象创建后调用");
        String servletName = config.getServletName();
        System.out.println("servletName = " + servletName);
    }
    @Override
    public void service(ServletRequest arg0, ServletResponse arg1) throws ServletException, IOException {
        System.out.println("服务，客户端每次访问时调用");
    }
    @Override
    public void destroy() {
        System.out.println("销毁，程序停止时调用");
    }
    @Override
    protected void finalize() throws Throwable { 
        System.out. println ("不可用，垃圾回收车收集内存时调用。");
    }
}
```

当客户端请求服务器时，如果URL匹配到该Servlet在web.xml中配置的规则时，该Servlet会被WebServer调用，并完成初始化（init方法）， 其过程如下图10-2所示。

![](/assets/10-2.png)

其中： 

* 构造方法（实例化）与init\(初始化\)方法是一起执行的，可能是在第一次访问时执行，或者web程序启动时执行。当在web.xml配饰文件中加上上&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;时，两个方法在web应用程序启动时调用。 
* init\(\)调用一次，一般第一次访问Servlet时调用。service\(\)调用多次，每次访问时调用。也有可能调用0次。
* destroy\(\)调用一次，应用程序关闭时调用（服务器关了，应用 程序也会关闭；而程序关闭，服务器则不一定关闭）。

 Servlet在运行过程中一般经过以下五个生命阶段，如图10-3所示。

![](/assets/10-3.png)

1. 实例化或称创建，创建对象，分配内存空间，由容器完成。

2. 初始化，指的是调用init方法，在对象实例化后执行。完成初始servlet要使用的资源，给变量赋初值等工作。

3. 服务，调用service方法，根据用户请求做出相应。 

4. 销毁，调用destroy方法，释放初始化占用的资源。 

5. 标记实例为不可用状态，等待JVM垃圾回收车回收内存。



