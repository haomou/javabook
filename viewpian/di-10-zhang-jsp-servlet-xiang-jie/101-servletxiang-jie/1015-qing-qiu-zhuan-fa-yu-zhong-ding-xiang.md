### 10.1.5 请求转发与重定向

在现实项目开发中，一个Servlet往往处理不了所有业务，这时我们需要多个Servlet协同工作处理，这就好比去医院看病，如果病情简单的话一个大夫看看就可以了，但如果病情复杂的话需要好几个大夫查看确认。在WEB请求中就涉及到请求转发和重定向。

请求转发就是将当前请求转发到另外一个Servlet处理，本Servlet可以做一些前期处理，也可以传递参数给下一个Servlet，也可以什么不做直接转发，示例如下：

```
public void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    System.out.println("我是第一个 Servlet！");
    request.setAttribute("name", "chero");
    RequestDispatcher rd = request.getRequestDispatcher("/MyServlet2");
    rd.forward(request, response);
}
```

注意：本例中传递参数使用的是request对象的attribute（属性），与参数（parameter）不同的是，参数是由服务器放入的程序中只能读取，不能写入；而属性可以读写，而且可以放入对象。 

在MyServlet2中处理如下：

```
public void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    System.out.println("name = " + request.getParameter("name"));
}
```

请求转发特点如下: 

1. 请求转发需要requestDispatcher的支持，通过request.getRequestDispatcher方法得到RequestDispatcher对象。 RequestDispatcher的forward方法传递request与response。 
2. request数据从第一个servlet到第二个servlet不会丢失，因为使用的是同一个request。 
3. 请求转发只能在一个webApp内部转发。 
4. 如果请求的第一个servlet 方法是doGet，那么转发给其它Servlet的方法也是doGet，也就是说，所有的请求方法类别一致。 

关于重定向示例如下:

```
public void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    System.out.println("我是第一个 Servlet！");
    response.sendRedirect("/MyServlet2");
}
```

重定向的特点如下： 

1. 不需要requestDispatcher，使用response.sendRedirect（）方法， 不能传递request对象。 
2. request数据从第一个servlet到第二个servlet会丢失，因为使用的不是同一个request对象。 
3. 重定向可以定向到其它应用程序。 
4. 不管第一个请求是get还是post，定向后全部变为默认的get。 
5. 与请求转发不同的是，请求转发处理完，地址栏url路径为第一个（servlet）资源路径；重定向为最后一个url路径。 

重定向与请求转发的区别： 

1. 请求转发不需要加webApp名称。重定向需要添加webApp名称，但如果是定向到一个程序内部，这时可以不添加，但资源路径不 能再写“/”。 
2. 请求转发只能在一个web应用程序内部转发，重定向可以到其他应用程序。 
3. 请求转发后面调用的方法类别与前面相同，而重定向全部会变为get请求，与之前的没关系。
4. 请求转发是一次请求（只有一个request对象），重定向是多次请求（生成多个request对象）。



