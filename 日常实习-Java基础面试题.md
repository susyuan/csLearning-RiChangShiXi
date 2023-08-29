# 日常实习-Java基础面试题



# 基础概念与常识





# 基本语法





# 基本数据类型



# 变量

# java语言有哪些特点

- 面向对象：三大特性

- 支持多线程：四种创建多线程方式（C++ 语言没有内置的多线程机制，因此必须调用操作系统的多线程功能来进行多线程程序设计，而 Java 语言却提供了多线程支持

- 平台无关： 一次编写到处运行，因为用**java虚拟机机制**，不同平台运行不需要重新编译；JVM对各种OS做了定制，java文件编译生成.class文件给JVM使用
- 可靠性，（具备异常处理和自动内存管理机制/自动内存回收，防止内存泄漏）

# 关键字

## static

“static”关键字表明一个成员变量或者是成员方法**可以在没有所属的类的实例变量的情况下被访问。**
Java中static方法不能被覆盖，因为方法覆盖是基于运行时动态绑定的，而static方法是编译时静态绑定的。

static方法跟类的任何实例都不相关，所以概念上不适用。

## final

# 如何理解Java的一次编译到处运行呢

原因：

一是因为JVM针对各种操作系统、平台都进行了定制

二是因为无论在什么平台，都可以编译生成固定格式的字节码（.class文件）供JVM使用。

---

字节码并不专对一种特定的机器，因此，Java程序无须重新编译便可在多种不同的计算机上运行。

JAVA是编译和解释并行；Java语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率低的问题，同时又保留了解
释型语言可移植的特点。

### --Java和C++区别

- 都支持封装继承多态
- C++支持指针
- C++支持多继承， Java不支持 但Java可以一个类实现多个接口
- java自动内存回收
- java不支持操作符号重载
- java不提供goto语句

### --JRM JDK JVM关系

JVM java虚拟机

JRM，运行java程序 不能创建程序，是JAVA运行环境

JDK 包含jre和编译器 能够创建java程序

![image-20230731182626692](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307311826761.png)

# 面向对象特性

**封装**

大体概念：客观事物封装成抽象类，只暴露小部分信息，对不可暴露信息进行隐藏；

实际操作：指把一个对象的状态信息（也就是属性）==隐藏在对象内部，不允许外部对象直接访问对象的内部信息==。但是可以提供一些可以被外界访问的方法来操作属性。



**多态**

一个对象具有多种的状态，具体表现为父类的引用指向子类的实例。

父类定义的属性 方法被子类继承后，可以表现不同的行为

eg:

对象类型和引用类型之间具有继承（类）/实现（接口）的关系；

引用类型变量发出的方法调用的到底是哪个类中的方法，必须在程序运行期间才能确定；

多态不能调用“只在子类存在但在父类不存在”的方法；

如果子类重写了父类的方法，真正执行的是子类覆盖的方法，如果子类没有覆盖父类的方法，执行的是父类的方法

继承：子类继承父类的功能和属性，进行扩展

> 继承是使用已存在的类的定义作为基础建立**新类**的技术，新类的定义可以增加新的数据或新的功能，也可以用父类的功能，但==不能选择性地继承父类==。通过使用继承，可以快速地创建新的类，可以提高代码的重用，程序的可维护性，节省大量创建新类的时间 ，提高我们的开发效率。

多态指的都是运行时多态，也就是编译时不确定究竟调用哪个具体方法，一直延迟到运行时才能确定。

### --如何实现多态

继承：在多态中必须存在有继承关系的子类和父类。
重写：子类对父类中某些方法进行重新定义，在调用这些方法时就会调用子类的方法。
向上转型：在多态中需要将子类的引用赋给父类对象，只有这样该引用才既能可以调用父类的方法，又能调用子类的方法。

## ---访问修饰符区别

private和protected 不能修饰类

---

private

public

缺省

protected 同一包下和子类

### ---break continue return

break 跳出总上一层循环，不再执行循环(结束当前的循环体)
continue 跳出本次循环，继续执行下次循环(结束正在执行的循环 进入下一个循环条件)
return 程序返回，不再执行下面的代码(结束当前的方法 直接返回)



# 那你告诉我private static final String='a'和private static final int=1，这两个量什么时候初始化，区别是什么？



# Object字段

hashcode toString wait notify  finalize  

### ---Java有哪些数据类型

基本数据类型和引用数据类型

数据类型八大

int,short,long float double char boolean byte

引用数据类型

- 数组
- 接口
- 类

# 基本数据类型和包装数据类型

8种  byte int short long float double char boolean

![image-20230720165111526](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307201651560.png)

区别 包装类型可用于泛型， 包装类型不赋值默认null  ==比较方式比较内存地址

存放  虚拟机栈的局部变量表  对象存在堆

# 自动装箱拆箱

装箱：基本类型->包装类型

拆箱 包装类型->基本类型

装箱包装类的`valueOf()`方法，拆箱其实就是调用了 `xxxValue()`方法。

# 重载和重写区别

重写:发生在子类和父类之间，方法名和参数一样，子类对父类方法重写，

重载，方法名相同，方法参数不同 ；重载的方法不能根据返回类型区分；

# 抽象类接口

抽象类用abstract修饰；含有**抽象方法**的类是抽象类，不能实例化

抽象方法是用public abstact  修饰的方法

不能 用 abstract 修饰变量、代码块、构造器；
不能用 abstract 修饰 私有方法、静态方法、 final 的 方法、 final 的类。

---

接口interface

接口是由**抽象方法**和**常量值**定义的集合

接口中的所有成员变量都 默认 是由 public static final 修饰的 。
接口中 的所有抽象方法 都 默认 是由 public abstract 修饰的

> 定义 Java 类的语法格式： 先写 extends ，后写 implements



**共同点**

- 都不能被实例化。
- 都可以包含抽象方法。
- 都可以有默认实现的方法（Java 8 可以用 `default` 关键字在接口中定义默认方法）。

**不同点**

抽象类可以提供方法实现细节  接口只有public abstract方法

抽象类成员变量各种类型 /接口public static final

接口不能有静态代码块/静态方法   抽象类可以有

接口是对行为抽象，抽象类是对事物抽象

# String、 StringBuffer和StringBuilder的区别是什么?String为什么是不可变的?

1.String不可变， StringBuffer和StringBuilder都可变

2.StringBuffer**线程安全**   String不可变 理解为常量 所以**线程安全**

3.每次对 `String` 类型进行改变的时候，都会生成一个新的 `String` 对象，然后将指针指向新的 `String` 对象。`StringBuffer` 每次都会对 `StringBuffer` 对象本身进行操作，stringbuilder也对对象操作

# String为什么不可变

使用 `final` 关键字修饰**字符数组**来保存字符串

1.字符数组被final修饰且为**私有**，String类没有暴露修改这个字符数组的方法

2.string类被final修饰导致不能被继承 避免子类破坏String不可变特性

![image-20230720194609523](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307201946562.png)

# string类能否继承

不能，被final修饰

# ==String s1 = new String("abc");这段代码创建了几个字符串对象？

1或2个；如果字符串常量池中已存在**字符串对象“abc”**的引用，则只会在堆中创建 1 个字符串对象“abc 否则2个

创建s**tring类对象**和创建 字符串对象 

![img](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307201942702.png)

# final作用

用途:修饰变量、方法、类

>  变量分为`引用不可变`和`对象不可变`

作用：

变量：基本类型不可修改  引用类型不可改变引用对象‘

方法：不能被子类重写

类，不允许被继承

# final finally finalize区别

**finally**

finally是异常处理一部分   try/catch中 一定会被执行

**finalize**

finalize是object的方法 ,这个方法在gc启动，对象被回收时候调用

> 一个对象的 finalize 方法只会被调用一次，finalize 被调用不一定会立即回收该对象，所以有可能调用finalize 后，该对象又不需要被回收了，然后到了真正要被回收的时候，因为前面调用过一次，所以不会再次调用 finalize 了，进而产生问题，因此不推荐使用 finalize 方法。

**final**

用途:修饰变量、方法、类

>  变量分为`引用不可变`和`对象不可变`

作用：

变量：基本类型不可修改  引用类型不可改变引用对象‘

方法：不能被子类重写

类，不允许被继承

# java创建对象方式

- new
- 反射
- clone
- 序列化

**反射**

动态获取类的信息，调用类的方法

获取类的class对象实例

获取构造器对象

newinstance获取反射类对象

获取方法 

1.获取方法对象

2.invoke调用方法

**序列化**

1.什么是序列化



2.

# string底层是什么结构

![](https://duoduo-img.oss-cn-shenzhen.aliyuncs.com/202307201946259.png)

char 字符数组 

# 字符串常量池

为String类设置， 减少内存消耗，提升性能

避免字符串的重复创建

# 异常

excepton 程序能处理

error程序无法处理

# 反射



## 何为反射 

通过反射可以**运行时动态获取任意一个类的所有属性和方法**，你还可以调用这些方法和属性

步骤

1获取类的class对象实例

2获取构造器对象

3newinstance获取反射类对象

4方法 

​	1.获取方法对象

​	2.invoke调用方法

## 几种常见的反射获取Class的方式 

1知道具体类  String.class

2.  传入类的全路径名获取  forName
3.  对象实例.getClass
4. 类加载器传入类路径 `ClassLoader.getSystemClassLoader().loadClass("cn.javaguide.TargetObject");`

## 什么时候可以直接.class获取

知道具体的类

## 反射的底层原理



# 序列化

Java序列化是指把**Java对象转换为字节序列**的过程

Java反序列化是指字节序列恢复为Java对象的过程

序列化可以 把对象 **持久化或网络传输**  堆中对象随着JVM消失而消失

实现serializable接口

# I/O

BIO 同步并阻塞  一个连接一个线程

NIO 同步并且非阻塞    连接到多路复用器上，轮询到有IO请求时才启动一个线程处理

AIO 异步并且非阻塞

## 异步IO和同步IO

# 设计模式

## 聊聊常见的设计模式

**适配器（Adapter Pattern）模式** 主要用于接口互不兼容的类的协调工作，你可以将其联想到我们日常经常使用的电源适配器。

**装饰器模式** 更侧重于动态地增强原始类的功能，装饰器类需要跟原始类继承相同的抽象类或者实现相同的接口。

## spring中的设计模式有哪些

1.简单工厂模式

BeanFactory就是简单工厂模式的体现，根据传入一个唯一标识来获得 Bean 对象

调用者先找到被依赖对象的工厂，然后**主动**通过工厂去获取被依赖对象，最后再调用被依赖对象的方法。（由工厂去创建对象

2.工厂方法模式

FactoryBean就是典型的工厂方法模式。
spring在使用getBean()调用获得该bean时，会自动调用该bean的getObject()方法。
每个 Bean 都会对应一个FactoryBean，如SqlSessionFactory 对应SqlSessionFactoryBean.

3.单例模式（私有化构造方法 私有静态对象  get的时候返回

- 一个类仅有一个实例，提供一个访问它的全局访问点。（避免一个全局使用的类频繁创建和销毁
-  Spring 创建 Bean 实例默认是单例的。

1懒汉 线程不安全

2懒汉 线程安全

3饿汉

4双锁DCL

~~~java
//1
public class Singleton {  
    private static Singleton instance;  
    private Singleton (){}  
  
    public static Singleton getInstance() {  
        if (instance == null) {  
            instance = new Singleton();  
        }  
        return instance;  
    }  
}
//2
public class Singleton {  
    private static Singleton instance;  
    private Singleton (){}  
    public static synchronized Singleton getInstance() {  
        if (instance == null) {  
            instance = new Singleton();  
        }  
        return instance;  
    }  
}
//3
public class Singleton {  
    private static Singleton instance = new Singleton();  
    private Singleton (){}  
    public static Singleton getInstance() {  
    return instance;  
    }  
}
public class Singleton {  
    private static Singleton instance = new Singleton();  
    private Singleton (){}  
    public static Singleton getInstance() {  
    	return instance;  
    }  
}
//4 懒汉 双锁DCL
public class Singleton {  
    private  static Singleton singleton;  
    private Singleton (){}  
    public static Singleton getSingleton() {  
    if (singleton == null) {  
        synchronized (Singleton.class) {  
            if (singleton == null) {  
                singleton = new Singleton();  
            }  
        }  
    }  
    return singleton;  
    }  
}
~~~



4.适配器模式

- SpringMVC中的适配器HandlerAdatper.
- 由于应用会有多个Controller实现，如果需要直接调用Controller方法，那么需要先判断是由哪一个Controller处理请求，然后调用相应的方法。
- 当增加新的 Controller，需要修改原来的逻辑，违反了开闭原则。
  开闭原则:对修改关闭，对扩展开放
- 为此，Spring提供了一个适配器接口，每一种 Controller 对应一种 HandlerAdapter 实现类
- 当请求过来，SpringMVC会调用getHandler()获取相应的Controller
- 然后获取该Controller对应的HandlerAdapter，最后调用HandlerAdapter的handle()方法处理请求，实际上调用的是Controller的handleRequest()。
- 每次添加新的 Controller 时，只需要增加一个适配器类就可以,无需修改原有的逻辑。

5.代理模式（通过代理对象实现对对象的访问

spring 的 aop 使用了动态代理有两种方式
JdkDynamicAopProxy和Cglib2AopProxy。

6.观察者模式
spring 中 observer 模式常用的地方是 listener 的实现，如ApplicationListener
7、模板模式
Spring 中 jdbcTemplate.hibernateTemplate 等，就使用到了模板模式。

## 设计模式了解哪些？代理模式了解吗



## 多线程高并发时候的单例模式怎么办(我的回答是加锁，面试官说我代码里没写，我说我就写了个普通单例)。



## 用过哪几种设计模式 策略模式用过吗



## 你了解哪些设计模式？单例你一般怎么实现的？（`DCL`）



##  动态代理是怎么实现的