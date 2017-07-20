当时的跨平台技术主要有两种：

* 编译执行，如 C/C++程序，需要将源代码放到特定平台下编译，生成对应的可执行程序执行。缺点：并不是真正意义上的跨平台。

* 解释执行，如 html， javaScript 和现在流行的 php 等，需要使用特定的解释器把代码一行行解释为机器码执行。优点：可以跨平台。

缺点：执行速度慢，暴露源程序。

SUN 公司在综合自己的设计需求之后，分析以上的跨平台原理 之后，设计了 JAVA 自己的跨平台技术—半编译半解释，保留了编译执行和解释执行方案的优点，同时采用 JVM 又可解决垃圾回收、内存管理 、安全检查等问题。 各跨平台方案比较， 如图 1-1。

![](/assets/搜狗截图20170720155113.png)

图 1-1 JAVA 跨平台比较

JAVA 半编译半解释的原理是先将 JAVA 源代码编译成中间字节码.class文件，然后通过平台的 JVM（JAVA 虚拟机）加载、解释字节码执行。虽然编译器与字节码是与平台无关的，但解释器是与平台有关的，若要执行JAVA 程序必须在相应平台下安装 JAVA 虚拟机

### 1.1.1 建立 JAVA 平台

正如上所诉，搭建 JAVA 平台需要 JAVA 编译器和 JAVA 解释器，如果只是执行 JAVA 程序，则只安装 JAVA 解释器就够了。 Sun 公司将 JAVA 编译器与 JRE 打包发行，命名为 JAVA SDK（Java Software develop kit）。JVM ： Java Virtual Machine， Java 虚拟机， Java 解释器的官方叫法，包含：类加载器，字节码效验器， Java 解释器。它是与平台相关的，我们说各个平台的 JDK 版本不同，其实重点说的就是 JVM 版本的不同。

* JAVA
* • JAVA源代码
* • .class字节码
* • JVM执行
* •（JVM不是跨平台的）

* C / C++

* • C/C++程序
* •可执行文件
* Html / PHP / JAVA Script
* • Html/php程序
* • 可执行机器码

JRE ： Java Runtime Environment， Java 运行时环境，包含 JVM 与 Java运行支持类库与文件\(运行支持类库与文件您可以理解为 C 语言的内置函数\)，如果您的电脑不需要开发 Java 程序，那么只要安装 JRE 即可。

* 下载 JDK

由于 Sun 公司在 2009 年被 ORACLE 公司收购，到 ORACLE 官网www.oracle.com 找到 JDK 板块即可下载。

☞ 如果是 windows 操作系统，下载对应 exe 文件，安装，注意选择安装目录，待会配置环境变量用到。

☞ 如果是类 Linux 操作系统，则根据 linux 平台，下载 bin 安装包或rpm 安装包，若是 bin 安装包，执行以下命令：

chmod u+x jdk-6u27-linux-i586.bin //修改权限

./jdk-6u27-linux-i586.bin //安装，

安装完后会在当前目录产生 java 文件夹。 若是 rpm 安装包，执行以下命令：

rpm –ivh jdk-6u21-linux-i586.rpm

安装完后会在/user 下产生 java 目录。

* 配置环境变量

Windows 环境下， 在【我的电脑】右键【属性】 -&gt;【高级】 -&gt;【环境变量】，单击【环境变量】，如图 1-2：

![](/assets/搜狗截图20170720155355.png)单击新建按钮，新建环境变量名： JAVA\_HOME，变量值为 jdk 安装路径，如：“C:\Program Files\jdk1.6.0\_2”；同样，新建环境变量名： CLASSPATH ，变量值设置为“.;%JAVA\_HOME%\lib\dt.jar;%JAVA\_HOME%\lib\tools.jar”；找到 Path 环境变量，编辑， 在最前面添加“%JAVA\_HOME%\bin;”，如图1-3 所示。

![](/assets/搜狗截图20170720155427.png)

☞ Linux 环境下，在全局用户配置文件/etc/profile 或个人配置文件~/.bashrc 中最后添加如下内容：

export JAVA\_HOME=/home/liangshihong/jdk1.6.0\_12

export PATH=$JAVA\_HOME/bin:$PATH

export CLASSPATH=.:$JAVA\_HOME/lib/dt.jar:$JAVA\_HOME/lib/tools.jar

此时，在控制台下输入： java –version 若有正常信息输出，则 JAVA平台搭建成功。

1.1.2 编写 JAVA 程序

编写 JAVA 程序最常用的 IDE（Integrated Development Environment，集成开发环境）就是 Eclipse， JBuilder， NetBeans 等等。这三者各有优点和不足，读者可就自己爱好选择，作者经常使用的是 NetBeans 和 Eclipse。这里，我们并不对各个开发工具做多介绍，而是用原生的方法编译执行一个JAVA 程序，分析一下 JAVA 平台是如何工作的。

* 首先，用记事本或写字板编写如下程序：

```
class Test{
public static void main (String args[ ]){
    int arc = args.length;
    if (arc>0){
        for (int i =0;i<arc;i++)
            System.out.println(args[i]);
        }else{
            System.out.println("hello， master!");
            System.out.println("your application have no args!");
        }
    }
}
```

保存为 Test.java 文件，注意文件扩展名为.java。注意：一定要先在文件对话框中找到文件夹选项，若是 win7 系统和 xp 系统位置不同，如下图1-4 所示：

![](/assets/搜狗截图20170720155510.png)

然后将“隐藏已知文件扩展名”去掉选中状态，如下图 1-5 所示：

![](/assets/搜狗截图20170720155519.png)

然后查看刚才保存的文件，确保文件后缀名为.java。 同时注意编程规范性：

☞ 文件名和类名一致，类名首字母必须大写，建议采用驼峰式大小写（camel case） 规范， JAVA 语言严格区分大小写。

☞ 类名中只能出现字母，数字，下划线和$符号，并且不能以数字开头， java 类名不能是 java 关键字，或称保留字，比如 public,class。

☞ Java 关键字表格如下表 1-1 所示：

表 1-1 关键字列表

* 基本数据类型 Boolean， byte， int， char， long， float， double
* 访问控制符 Private， public， protected， volatile
* 与类相关 Abstract， class， interface， extends， implements
* 与对象相关 New， instance of， this， super， null
* 与方法相关 Void， return， super， this
* 控制逻辑 If， else， switch， case， default， for， do， while， break，
* continue， true， false
* 异常处理 Try， catch， throw， throws
* 其他 Package， import， synchronized， native， final， static
* 停用的关键字 Goto， const

* Windows 环境，【开始】 &gt;【运行】中输入 cmd，进入 dos 命令行窗口 。

进入文件保存的目录，如 d:\java\Test.java，则输入如下命令：

* d: //切换盘符
* cd java //进入目录
* dir //列出该目录下所有文件

* 即可看到 Test.java 文件。

  linux 环境，直接打开控制台，进入文件目录。然后输入 javac Test.java，

将源代码编译为中间字节码文件（.class），然后就可以在解释器（JVM）中运行了。输入如下命令： java Test，控制台会输出如下：

hello， master!

your application have no args!

若输入如下命令： java Test hello world，带入参数 hello world，则会输出： hello world

