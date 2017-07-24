### 2.1.2 类修饰符

类修饰符是用以指明类的性质的关键字。用户在自定义类时，指定不  
同的修饰符，就可以让类具备不同的存取权限。一个类总能访问和调用它  
自己定义的成员变量和方法，但在这个类之外的其他类能否访问和调用，  
除与类的修饰符有关外，还与类的成员变量和方法的控制符有关。类修饰符有：abstruct、static、public、protected、private、

基本的  
类修饰符有 public,public， abstract 和 final 三个。

访问修饰符public,private,protected,以及不写（默认）时的区别？ 

答：

修饰符	当前类	同 包	子 类	其他包

public	√	√	√	√

protected	√	√	√	×

default	√	√	×	×

private	√	×	×	×

类的成员不写访问修饰时默认为default。默认对于同一个包中的其他类相当于公开（public），对于不是同一个包中的其他类相当于私有（private）。受保护（protected）对子类相当于公开，对不是同一包中的没有父子关系的类相当于私有。Java中，外部类的修饰符只能是public或默认，类的成员（包括内部类）的修饰符可以是以上四种。

