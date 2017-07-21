#### 3.3.4 用户自定义异常

自定义异常是那些不能由 Java 系统监测到的异常（下标越界，被0除等），而是由用户自己定义的异常。用户定义的异常同样要用 try--catch捕获，但必须由用户自己抛出，格式为：

throw new MyException

由于异常是一个类，用户定义的异常必须继承自Throwable或Exception类，建议用Exception类。如：

```
public class MyException extends Exception{
    //类体 
};
```

下面给出一个完整的实例：

```
package com.test;
public class MyEx extends Exception {
    public MyEx(String msg){
        super(msg);
    }
    public static void demoproc() throws MyEx {
        try {
            throw new MyEx("抛出异常示例");
        } catch (MyEx e) {
            System.out.println("捕捉内部过程的异常");
            throw e;
        }
    }
    public static void main(String args[]) {
        try {
            demoproc();
        } catch (MyEx e) {
            System.out.println("捕捉抛出异常: " + e);
        }
    }
}
```

输出结果：

捕捉内部过程的异常

捕捉抛出异常: com.campus.flashCraw ler.MyEx: 抛出异常示例

