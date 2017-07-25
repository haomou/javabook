### 2.3.5 接口

接口（ interface）可看成一个空的抽象的类，只声明了一组类的若干

同名变量和方法，而不考虑方法的具体实现。

Java 的接口也是面向对象的一个重要机制。它的引进是为了实现多继

承，同时免除 C++中的多继承那样的复杂性。前面讲过，抽象类中包含一

个或多个抽象方法，该抽象类的子类必须实现这些抽象方法。接口类似于

抽象类，只是接口中的所有方法都是抽象的。这些方法由实现这一接口的

不同类具体完成。在使用中，接口类的变量可用来代表任何实现了该接口

的类的对象。这就相当于把类根据其实现的功能来分别代表，而不必顾虑

它所在的类继承层次。这样，可以最大限度地利用动态绑定来隐藏实现细

节。

接口还可以用来实现不同类之间的常量共享，若在接口中定义变量，

必须为该变量赋值，同时该变量会默认为 final 类型，相当于常量。 接口的

实现需要使用 implements 关键字。

###### 接口的示例如下：

public interface Cash {

public static String hh = "111";

public void sayHello\(\);

}

public class RMB implements Cash{

public Date year;

@Override // 实现父类方法

public void sayHello\(\) {

System.out.println\("hello USD!"\);

}

public static void main\(String\[\] args\) {

System.out.println\("hh" + hh\);

Cash RMB = new RMB\(\);

RMB.sayHello\(\); // 会调用 RMB 的方法，类似多态

Cash URO = new URO\(\);

URO.sayHello\(\); // 会调用 URO 的方法，类似多态

}

}

class URO implements Cash{

@Override // 实现父类方法

public void sayHello\(\) {

System.out.println\("hello URO!"\);

}

}

