## 10.2.3 JSP处理Cookie

Cookie是Web服务器保存在用户硬盘上的一段文本。Cookie允许一个Web站点在用户电脑上保存信息并且随后再取回它。举例来说，一个Web站点可能会为每一个访问者产生一个唯一的ID，然后以Cookie文件的形式保存在每个用户的机器上。如果用户使用IE浏览器访问Web，用户就会看到所有保存在自己硬盘上的Cookie。它们最常存放的地方是： C:/Windows/Cookies。Cookie是以“关键字 key=值value”的格式来保存记录的。

*  调用Cookie对象的构造函数就可以创建Cookie 对象。Cookie对象的构造函数有两个字符串参数：Cookie名字和Cookie值。

```
Cookie c = new Cookie("username","john");
```

* 将Cookie对象传送到客户端，在JSP中，如果要将封装好的Cookie对象传送到客户端，可使用Response对象的addCookie\(\)方法。

```
response.addCookie(c)。
```

* 读取保存到客户端的Cookie，使用Request对象的getCookie\(\)方法， 执行时将所有客户端传来的Cookie对象以数组的形式排列，如果要取出符合需要的Cookie对象，就需要循环比较数组内每个对象的关键字。

```
Cookie[] c = request.getCookies();
if(c != null){
    for(int i = 0;i < c.length;i++){
        if("username".equals(c.getName())){
            out.println(c.getValue());
        }
    }
}
```

* 设置Cookie对象的有效时间，调用Cookie对象的setMaxAge\(\)方法便可以设置Cookie对象的有效时间

```
Cookie c = new Cookie("username","john");
c.setMaxAge(3600);
```

Cookie对象的典型应用时用来统计网站的访问人数。由于代理服务器、缓存等的使用，唯一能帮助网站精确统计来访人数的方法就是为每个访问者建立一个唯一ID。使用Cookie，网站可以完成一下工作。

*  测定多少人访问过

*  测定访问者有多少是新用户（即第一次来访），多少是老用户

*  测定一个用户多久访问一次网站

当一个用户第一次访问时，网站在数据库中建立一个新的 ID，并把ID通过Cookie传送给用户。用户再次来访时，网站把该用户ID对应的计数器加1，得到用户的来访次数。



