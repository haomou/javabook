####  3.3.2 异常处理机制

JAVA中异常类的结构层次如图3-5所示。

![](/assets/3-5.png)

##### 解释说明

* **ERROR类**

 Error类型的异常与Java虚拟机本身发生的错误有关，用户程序不需要处理这类异常。

* **EXCEPTION类**

程序产生的错误由Exception的子类表示，用户程序应该处理这类异 常。Exception中定义了许多异常类，每个异常类代表了一种执行错误，类中包含了对应于这种运行错误的信息和处理错误的方法等内容。当程序执行期间发生一个可识别的执行错误时，如果该错误有一个异常类与之相对应，那么系统就会产生一个相应的该异常类的对象。一旦一个异常对象产生了，系统中就一定有相应的机制来处理它，从而保证用户程序在整个执行期间不会产生死机、死循环等异常情况。Java语言采用这种异常处理机制来保证用户程序执行的安全性。部分常见错误如下表3-2所示。 

                                                                                                   **表 3-2 常见异常**

| **名称** | **含义** |
| :--- | :--- |
| ArithmeticException | 算术错误 |
| ArrayIndexOutOfBandsException | 数组越界 |
| ArrayStoreException | 数组存储空间不足 |
| IOException | 输入输出错误 |
| FileNotFoundException | 指定文件不存在 |
| NullPointerException | 访问一个空对象成员 |
| MalformedURLException | URL格式错 |
| NumberFormatException | 数据格式错误 |



