### 2.3.4 多态

多态性是指允许不同类的对象对同一消息作出响应。比如同样的加法，

把两个时间加在一起和把两个整数加在一起肯定完全不同。又比如，同样

的选择-编辑-粘贴操作，在字处理程序和绘图程序中有不同的效果。

多态性包括参数化多态性和包含多态性。多态性语言具有灵活、抽象、

行为共享、 代码共享的优势，很好的解决了应用程序函数同名问题。

实现多态，有二种方式：覆盖（重写），重载。“重载”是指同一样东

西在不同的地方具有多种含义；而“覆盖”是指它随时随地都只有一种含

义，只是原先的含义完全被后来的含义取代了。

 覆盖，是指子类重新定义父类的虚函数（ Java 语言中, 所有的方法默认

都是"虚函数". 只有以关键字 final 标记的方法才是非虚函数）的做法。

 重载，是指允许存在多个同名函数，而这些函数的参数表不同（或许

参数个数不同，或许参数类型不同，或许两者都不同）。



###### 覆盖的方法如下例：

public class RMB extends Money {

public Date year;

public RMB\(String k, int v, Date y\) {

super\(k, v\);

this.year = y;

}

@Override // 重写父类方法

public void sayHello\(\) {

System.out.println\("hello USD!"\);

}

public void sayWorld\(\) {

sayHello\(\);

kind = "asdsa";

super.sayHello\(\);

System.out.println\("world!" + kind\);

}

public static void main\(String\[\] args\) {

Money USD = new RMB\("USD", 10, new Date\(\)\);

USD.sayHello\(\); // 实际调用的是 RMB 类中的方法

USD = new URO\("USD", 10\);

USD.sayHello\(\); // 实际调用的是 URO 类中的方法

}

}

class URO extends Money {

public URO\(String k, int v\) {

super\(k, v\);

}

@Override // 重写父类方法

public void sayHello\(\) {

System.out.println\("hello URO!"\);

}

}

class Money {

public static String kind;

int value;

private boolean isBroken;

public Money\(String k, int v\) {

this.value = v;

this.kind = k;

}

public void sayHello\(\) { // 父类方法

System.out.println\("hello!" + kind\);

}

}

###### 重载的方法如下例：

public class RMB extends Money {

public Date year;

public RMB\(String k, int v, Date y\) {

super\(k, v\);

this.year = y;

}

public RMB\(String k, int v\) {

super\(k, v\);

this.year = new Date\(\);

}

public RMB\(String k,Date y\) {

super\(k, 10\);

this.year = y;

}

public static void main\(String\[\] args\) {

RMB USD = new RMB\("USD", 10, new Date\(\)\);

RMB USD1 = new RMB\("USD", 10\);

RMB USD2 = new RMB\("USD", new Date\(\)\);

// 会根据不同的参数，调用不同的构造方法

}

}



