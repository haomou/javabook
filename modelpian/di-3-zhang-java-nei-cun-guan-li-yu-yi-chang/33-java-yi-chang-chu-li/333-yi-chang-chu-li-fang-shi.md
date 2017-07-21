####  3.3.3 异常处理方式

异常处理主要有三种： 

（1）对于运行时异常可以不做处理。 

（2）使用 try-catch-finally 语句捕获异常； 

（3）通过 throws 子句声明自己的异常，并用 throw 语句来抛出它

Java 的异常处理是通过5个关键词来实现的：try，catch，throw，throws和 finally。用 try 来执行一段程序，如果出现异常，系统抛出（throws）一 个异常，你可以通过它的类型来捕捉（catch）它，或最后（finally）由缺省处理器来处理，finally 结构使代码总会执行，而不管有无异常发生。使用finally可以维护对象的内部状态，并可以清理非内存资源。如下示例 。

```
try{
    程序块；
}catch(异常 1){对异常 1 的处理}
 catch(异常 2){
  对异常 2 的处理;
  throw(e); // 用户自己抛出新的异常
}finally{ 最终缺省处理代码；}
```

 如下具体程序，我们故意造出被零除和数组越界的异常，并处理。

```
public class MyExTest {
    public static void main(String[] args){
        try{
            int a =0;
            a = a/a;
            int[] c = {1};
            int d = c[1];
        }catch(ArithmeticException e){
            System.out.println("被零除!");
        }catch(ArrayIndexOutOfBoundsException e){
            System.out.println("数组越界!");
            e.printStaceTrace(); // 打印出异常追踪信息
        }finally{
            System.out.println("关闭资源，默认处理!");
        }
    }
}
```

使用时注意try和catch必须配套使用，可以没有finally，但是如果有必须要处理的问题可以放到finally中处理。下面介绍throw和throws的用法和区别。

* ##### **THROW**

throw语句用来明确地抛出一个“异常”。首先，必须得到一个Throwable的实例的控制柄，通过参数传到catch子句。该异常实例可以用new操作符来创建，下面是throw语句的通常形式： 

throw ThrowableInstance; 

具体事例如下：

```
class ThrowDemo{
    public static void demoproc(){
        try {
            throw new NullPointerException("抛出异常示例");
        }catch(NullPointerException e) {
            System.out.println("捕捉内部过程的异常");
            throw e;
        }
    }
    public static void main(String args[]) {
        try {
            demoproc();
        }catch(NullPointerException e) {
            System.out.println("捕捉抛出异常: " + e);
        }
    }
}
```

输出结果： 

捕捉内部过程的异常 

捕捉抛出异常:java.lang.NullPointerException: 抛出异常示例 

其中 throw new NullPointerException\("抛出异常示例"\)是用户自己生成了一个异常对象实例，并将该异常抛出。

* ##### **THROWS**

throws用来标明一个成员函数可能抛出的各种异常。对大多数Exception子类来说，Java编译器会强迫你声明在一个成员函数中抛出的异常的类型。如果异常的类型是Error或Runtime-Exception，或是它们的子类，则这个规则不起作用，因为这些在程序的正常部分中是不期待出现的。 如果你想明确地抛出一个RuntimeException，你必须用throws语句来声明它的类型，如下面一个示例。

```
class ThrowsDemo{
    static void procedure( ) throws IllegalAccessException{
        System.out.println("内部过程");
        throw new IllegalAccessException("抛出异常示例");
    }
    public static void main(String args[]){
        try{
            procedure( );
        }catch (IllegalAccessException e){
            System.out.println("捕捉异常 " + e);
        }
    }
}
```

输出结果为：   
内部过程 

捕捉异常 java.lang.IllegalAccessException: 抛出异常示例

