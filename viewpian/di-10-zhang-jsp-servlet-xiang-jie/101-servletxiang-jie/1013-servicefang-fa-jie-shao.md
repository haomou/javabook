### 10.1.3 service方法介绍

 一般我们编写的Servlet不覆盖service方法，而是重写doGet与doPost方法。关于这一点我们可以查看HttpServlet源代码如下：

```
protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException{
    //得到请求的类别 get post
    String method = req.getMethod(); 
    if(method.equals(METHOD_GET)){//如果请求类别是 get
        doGet(req, resp);
    }else if(method.equals(METHOD_POST)){
        doPost(req, resp);
    }    
}
```

因为HttpServlet中已经重写了service方法，并且根据请求类别调用自己的doGet与doPost方法，这是我们只要重写doGet与doPost即可。



