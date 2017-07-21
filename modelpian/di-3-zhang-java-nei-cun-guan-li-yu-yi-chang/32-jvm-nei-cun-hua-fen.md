## 3.2 JVM 内存划分

JVM会把申请的内存从逻辑上主要划分为七个区域：方法区，堆与栈， PC 指针，常量池，本地方法栈，直接内存区等。在控制台下，输入jconsole命令，即可查看当前JVM内存分配等状态。

为了便于讲解下面举一个例子：

```
class Money {    
    public String kind;
    public int value;
    public Money(String k,int v){ // 定义构造方法
        this.kind = k;
        this.value = v;
    }
    public void pay(){
        System.out.printfln(“坐公交”);
    }
}
public class Home {
    public static void main(String[] args){
        Money rmb = new Money(“人民币”,10); // 自动调用定义的构造方法
        int var = 20;
    }
}
```

如上，我们称整个money类为类结构，保存在JVM方法区中。rmb和var称为变量，rmb是复杂类型的变量，即是类类型，其中new Money\(“人民币”,10\);创建了一个对象，而rmb变量的值是该对象，保存在JVM内存堆上，其本身是指向该对象的一个引用，保存在 JVM内存栈上；var是简单类型变量，保存在JVM内存栈上。如下图3-4所示。

![](/assets/3-4.png)

