2.3.2 继承

继承是一种联结类的层次模型，并且允许和鼓励类的重用，它提供了一种明确表述共性的方法。对象的一个新类可以从现有的类中派生，这个过程称为类继承。新类继承了原始类的特性，新类称为原始类的派生类（子类），而原始类称为新类的基类（父类）。派生类可以从它的基类那里继承方法和实例变量，并且类可以修改或增加新的方法使之更适合特殊的需要。这也体现了大自然中一般与特殊的关系。

继承性很好的解决了软件的可重用性问题。比如说，所有的Windows应用程序都有一个窗口，它们可以看作都是从一个窗口类派生出来的。但是有的应用程序用于文字处理，有的应用程序用于绘图，这是由于派生出了不同的子类，各个子类添加了不同的特性。

下面给出一个详细的示例：

class Money {

```
          public String kind;

           int  value; //默认是友好类的

           private boolean isBroken; // 私有函数不被继承

   public Money\(String k,int v\){

                      this.value = v;

                      this.kind = k;

                           }

    public void sayHello\(\){

                   System.out.println\("hello!"\);

             }

         }
```

       public class RMB extends Money{

                       public Date year;

                       public RMB\(String k,int v,Date y\){

                                        super\(k,v\); //调用父类构造函数

                                        this.year = y;

                                   }

                        public void sayWorld\(\){

                                         super.sayHello\(\); //或者直接写

                                         sayHello\(\);

                                        System.out.println\("world!"\);

                                  } 

                         

                      @override

                      public void sayHello\(\){

                                 System.out.println\("hello!"\);

                                  }

