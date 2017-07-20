$$$$2.3.2 继承

继承是一种联结类的层次模型，并且允许和鼓励类的重用，它提供了一种明确表述共性的方法。对象的一个新类可以从现有的类中派生，这个过程称为类继承。新类继承了原始类的特性，新类称为原始类的派生类（子类），而原始类称为新类的基类（父类）。派生类可以从它的基类那里继承方法和实例变量，并且类可以修改或增加新的方法使之更适合特殊的需要。这也体现了大自然中一般与特殊的关系。

继承性很好的解决了软件的可重用性问题。比如说，所有的Windows应用程序都有一个窗口，它们可以看作都是从一个窗口类派生出来的。但是有的应用程序用于文字处理，有的应用程序用于绘图，这是由于派生出了不同的子类，各个子类添加了不同的特性。

下面给出一个详细的示例：



```
class Money {
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

                public static void main(String[] args) {
                            RMB rmb = new RMB("RMB",10,new Date());
                            rmb.sayWorld();
                            super.sayWorld();
                            Money USD = new RMB("USD", 10, new Date());
                            ((RMB)USD).sayWorld();
                            }
      }
```

说明：

** this **用以指代一个对象自身。它的作用主要是将自己这个对象作为参数，传送给别的对象中的方法。

** super  **用来取用父类中的方法和变量数据。

如上所示，RMB继承自Money类，或者说Money派生出RMB类，我们称Money为RMB的父类或基类，称RMB为Money的子类。

关于类的继承要注意以下几点：

1.子类继承父类的所有非私有属性及方法，若父类中有定义为 static 的静态属性，则子类与父类共同使用这一份属性变量，若有一个值改变了，  另一个也会变化。若父类有定义的 static 方法，则该方法不能被重 写。

2.若子类重写父类方法，则子类调用父类方法时采用（ super.方法名） 的方法调用。调用本类的方法，则直接写方法名或 this.方法名。 若子类没有重写父类方法，则直接写方法名也可以调用父类方法。

3.子类重写父类方法建议使用： @Override 标注， 因为此标注会自动检查，防止子类出现非技术性失误，如打错符号。

4.子类继承父类，同时子类可以有自己的属性和方法。

5.可以声明父类指向子类的对象。但是声明的是什么类型，就只能调用本类型的属性和方法，而实际执行的是所创建对象类型的方法，这一点又叫多态性。其次， 创建的什么类型，就可以强转为什么类型， 如上\\(\\(RMB\\)USD\\)， 将 USD 强制转换为 RMB。然后就可以调用 RMB 类的方法。

6.JAVA 为了免去 C++由于多重继承而衍生的问题，限定类的继承只能单一继承。但实际上又有多重继承的需要， 可以采用接口（ interface）这个概念来解决这个问题。（详细见后面章节介绍）

