
AtomicInteger 是一个 Java concurrent 包提供的一个原子类，通过这个类可以对 Integer 进行一些原子操作。这个类的源码比较简单，主要是依赖于 sun.misc.Unsafe 提供的一些 native 方法保证操作的原子性。

Unsafe 可以直接操控内存和线程，是一个比较危险的类。在 Java 里我们是无法直接使用这个类的，得通过反射机制获取。

我们会通过一个 Demo 来对 AtomicInteger 的源码进行解析，同时简单解释一下其中涉及到的 Unsafe 类方法。
```java
public class AtomicIntegerTest {

	public static void main(String[] args) {
		AtomicInteger atomicInteger = new AtomicInteger();
		atomicInteger.get();
	}
}
```
在这个 Demo 里面，我们需要关注以下两点：

1. AtomicInteger 在初始化的时候执行了哪些操作
1. getAndIncrement 是如何保证其操作的原子性的

AtomicInteger 在初始化的时候执行了哪些操作呢？由于代码比较简单，我们直接来看 AtomicInteger 的成员变量和静态代码块
```java
// setup to use Unsafe.compareAndSwapInt for updates
private static final Unsafe unsafe = Unsafe.getUnsafe();
private static final long valueOffset;

static {
    try {
        valueOffset = unsafe.objectFieldOffset
            (AtomicInteger.class.getDeclaredField("value"));
    } catch (Exception ex) { throw new Error(ex); }
}

private volatile int value;
```
从上图可以看出，AtomicInteger 主要有两个静态变量和一个成员变量，在初始化的时候会通过静态代码块给 valueOffset 赋值。

value 这个不用说，就是用来存储实际数值的；Unsafe 类我们之前有提到过，在这里也不做赘述了。

那么，valueOffset 这个静态变量又是用来做什么的呢？这时候我们就得看看它的赋值来源了。根据 API 文档，Unsafe 的 objectFieldOffset 方法可以获取成员属性在内存中的地址相对于对象内存地址的偏移量。说得简单点就是找到这个成员变量在内存中的地址，便于后续通过内存地址直接进行操作。
所以，valueOffset 其实就是用来定位 value，后续 Unsafe 类可以通过内存地址直接对 value 进行操作。

接着，我们再来看 AtomicInteger 的构造方法：
```java
/**
 * Creates a new AtomicInteger with initial value {@code 0}.
 */
public AtomicInteger() {
}
```
这是一个空方法，所以 AtomicInteger 在调用其默认构造方法的时候没有执行任何操作，一切都是默认值。

所以，综合静态代码和构造方法，AtomicInteger 在初始化的时候会定位其成员变量 value 的内存地址，后续通过内存地址直接对其进行操作。

了解了 AtomicInteger 的初始化逻辑，接下来我们再来看看 getAndIncrement 方法，可以看到还是依赖于 Unsafe 类。
```java
/**
 * Atomically increments by one the current value.
 *
 * @return the previous value
 */
public final int getAndIncrement() {
    return unsafe.getAndAddInt(this, valueOffset, 1);
}
```
我们再来看看 getAndAddInt 方法
```java
public final int getAndAddInt(Object var1, long var2, int var4) {
    int var5;
    do {
        var5 = this.getIntVolatile(var1, var2);
    } while(!this.compareAndSwapInt(var1, var2, var5, var5 + var4));

    return var5;
}
```
这时候会发现它里面又调用了 getIntVolatile 和 compareAndSwapInt 方法，而这两个方法都是 native 方法，具体说明可以参照 Unsafe 的 API 文档。

getIntVolatile 的主要作用是通过对象 var1 和成员变量相对于对象的内存偏移量 var2 来直接从内存地址中获取成员变量的值，所以 var5 就是当前 AtomicInteger 的值。

而 compareAndSwapInt (简称CAS) 的主要逻辑如下：

1. 通过对象 var1 和成员变量的内存偏移量 var2 来定位内存地址
1. 判断当前地址的值是否等于 var5
    1. 不等于：返回 false
    1. 等于：把当前地址的值替换成 var5 + var4 并返回 true

所以，综合来说，getAndAddInt 方法的主要逻辑如下：

1. 根据对象 var1 和内存偏移量 var2 来定位内存地址，获取当前地址值
1. 循环通过 CAS 操作更新当前地址值直到更新成功
1. 返回旧值

[原文](https://zhuanlan.zhihu.com/p/37302263)