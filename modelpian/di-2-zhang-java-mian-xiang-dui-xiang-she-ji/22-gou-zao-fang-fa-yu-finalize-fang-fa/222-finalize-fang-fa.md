### 2.2.2 finalize 方法



如上所诉，一半不建议使用 finalize 方法，除非特殊情况，如用其他

代码编写的 Class\(比如 JNI， C++的 new 方法分配的内存\)，垃圾回收器并

不能对这些部分进行正确的回收，这时就需要我们覆盖默认的方法来实现

对这部分内存的正确释放和回收\(比如 C++需要 delete\)。

关于 JAVA 垃圾回收器（ GC）相关知识如下：

 JAVA 的 GC 只负责内存相关的清理，所有其它资源的清理必须由程序

员手工完成。 否则会引起资源泄露，有可能导致程序崩溃。

 调用 GC 并不保证 GC 实际执行。

 finalize 抛出的未捕获异常只会导致该对象的 finalize 执行退出。

 用户可以自己调用对象的 finalize 方法，但是这种调用是正常的方法调

用，和对象的销毁过程无关。

 JVM 保证在一个对象所占用的内存被回收之前，如果它实现了 finalize

方法，则该方法一定会被调用。 Object 的默认 finalize 什么都不做，为

了效率， GC 可以认为一个什么都不做的 finalize 不存在。

 对象的 finalize 调用链和 clone 调用链一样，必须手工构造。

方法示例如下：

```
protected void finalize() throws Throwable {
    super.finalize();    
}
```



#### JAVA中的对象销毁过程



在对象的销毁过程中，按照对象的 finalize 的执行情况，可以分为以

下几种，系统会记录对象的对应状态：

 Unfinalized， 没有执行 finalize，系统也不准备执行。

 Finalizable， 可以执行 finalize，系统会在随后的某个时间执行 finalize。

 Finalized， 该对象的 finalize 已经被执行了。

GC 怎么来保持对 finalizable 的对象的追踪呢。 GC 有一个 Queue，叫

做 F-Queue，所有对象在变为 finalizable 的时候会加入到该 Queue，然后等

待 GC 执行它的 finalize 方法。这时我们引入了对对象的另外一种记录分类，

系统可以检查到一个对象属于哪一种。

 Reachable， 从活动的对象引用链可以到达的对象。包括所有线程当前

栈的局部变量，所有的静态变量等等。

 finalizer-reachable， 除了 reachable 外，从 F-Queue 可以通过引用到达

的对象。

 unreachable， 其它的对象。

对象的状态转换图，如图 2-1 所示。

![](/assets/对象销毁过程.png) 首先，所有的对象都是从 Reachable+Unfinalized 状态开始的。

 当从当前活动集到对象不可达时，对象可以从 Reachable 状态变到

F-Reachable 或者 Unreachable 状态。

 当对象为非 Reachable+Unfinalized 时， GC 会把它移入 F-Queue，状态

变为 F-Reachable+Finalizable。

 任何时候， GC 都可以从 F-Queue 中拿到一个 Finalizable 的对象，标记

它为 Finalized，然后执行它的 finalize 方法，由于该对象在这个线程中

又可达了，于是该对象变成 Reachable 了（并且 F inalized）。而 finalize

方法执行时，又有可能把其它的 F-Reachable 的对象变为一个 Reachable

的，这个叫做对象再生。

 当一个对象在 Unreachable+Unfinalized 时，如果该对象使用的是默认

的 Object 的 finalize，或者虽然重写了，但是新的实现什么也不干。为

了性能， GC 可以把该对象直接变到 Reclaimed 状态直接销毁，而不用

加入到 F-Queue 等待 GC 做进一步处理。

 从状态图看出，不管怎么折腾，任意一个对象的 finalize 只至多执行一

次，一旦对象变为 Finalized，就怎么也不会在回到 F-Queue 去了。当

然没有机会再执行 finalize 了。

 当对象处于 Unreachable+Finalized 时， GC 可以安全的回收该对象的

内存了。进入 Reclaimed。

#### 注意

所有 finalizable 的对象的 finalize 的执行是不确定的，既不确定由哪个

线程执行，也不确定执行的顺序。 使用时注意：

 尽量不要用 finalize，太复杂了，还是让系统照管比较好。可以定义其

它的方法来释放非内存资源。

 如果用，尽量简单。 同时避免对象再生，这个是自己给自己找麻烦。

 可以用来保护非内存资源被释放。即使我们定义了其它的方法来释放

非内存资源，但是其它人未必会调用该方法来释放。在 finalize 里面可

以检查一下，如果没有释放就释放好了，晚释放总比不释放好。

 即使对象的 finalize 已经运行了，不能保证该对象被销毁。要实现一些

保证对象彻底被销毁时的动作，只能依赖于 java.lang.ref 里面的类和

GC 交互了。

