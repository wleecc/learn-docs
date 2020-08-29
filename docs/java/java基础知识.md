# 1.Java基础

## 1.1. Java入门

### 1.1.1. Java语言的特点

1. 简单易学
2. 面向对象（封装、继承、多态）
3. 平台无关性（Java虚拟机对不同系统又特定的实现）
4. 可靠性
5. 安全性
6. 原生支持多线程
7. 支持网络编程（Java语言本身就是为简化网络编程设计的）
8. 编译与解释并存



### 1.1.2 关于JVM、JDK和JRE

#### 1.1.2.1 JVM

Java虚拟机（JVM）是运行Java字节码的虚拟机。JVM有针对不同系统的特定实现（Windows、Linux、macOS），目的是使用相同的字节码，它们都能执行出相同的结果。

**什么是字节码？采用字节码的好处是什么？**
>  在 Java 中，JVM 可以理解的代码就叫做`字节码`（即扩展名为 `.class` 的文件），它不面向任何特定的处理器，只面向虚拟机。Java 语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率低的问题，同时又保留了解释型语言可移植的特点。所以 Java 程序运行时比较高效，而且，由于字节码并不针对一种特定的机器，因此，Java 程序无须重新编译便可在多种不同操作系统的计算机上运行。 

**Java程序从源代码到运行一般有下面3步**
![](../../images/java/Java程序运行过程.png)

我们需要格外注意的是 .class->机器码 这一步。在这一部JVM类加载器首先加载字节码文件，然后通过解释器逐行解释执行，这种方式的执行速度会相对比较慢。而且，有些方法和代码块是经常需要被调用的（也就是所谓的热点代码），所以后面引进了JIT编译器，而JIT属于运行时编译。当JIT编译器完成第一次编译后，其会将字节码对应的机器码保存下来，下次可以直接使用。而我们知道，机器码的运行效率肯定是高于Java解释器的。这也解释了我们为什么经常会说Java是编译与解释共存的语言。

**总结：**
Java虚拟机（JVM）是运行Java字节码的虚拟机。JVM有针对不同系统的特定实现（Windows、Linux、macOS），目的是使用相同的字节码，它们都会给出相同的结果。字节码和不同系统的JVM实现是Java语言“一次编译，随处可运行”的关键所在。

#### 1.1.2.2. JDK和JRE
JDK是Java Development Kit，它是功能齐全的Java SDK。它拥有JRE所拥有的一切，还有编译器（javac）的工具（如javadoc和jdb）。它能够创建和编译程序。

JRE是Java运行时环境。它是运行已编译Java程序所需的所有内容的集合，包括Java虚拟机（JVM）、Java类库、Java命令和其他的一些基础构件。但是，它不能用于创建新程序。

如果只是为了运行一下Java程序的话，那么你之需要安装JRE就可以了。如果需要进行一些Java编程方面的工作，那么你就需要安装JDK了。但是，这不是绝对的。有时，即使您不打算再计算机上进行任何Java开发，仍然需要安装JDK。例如，如果要使用JSP部署Web应用程序，那么从技术上讲，您只是在应用程序服务器中运行Java程序。那你为什么需要JDK呢？因为应用程序服务器会将JSP转换为Java servlet，并且需要使用JDK来编译servlet。

### 1.1.3. 为什么说Java语言“编译与解释并存”
高级编程语言按照程序的执行方式分为编译型和解释型两种。简单开说，编译型语言是指编译器针对特定的操作系统将源代码一次性编译成可被该平台执行的机器码；解释型语言是指解释器对源程序逐行解释成特定平台的机器码并立即执行。

Java语言既具有编译型语言的特征，也具有解释型语言的特征，因为Java程序要经过先编译、后解释两个步骤，由Java编写的程序需要先经过编译步骤，生成字节码（*.class文件），这种字节码必须由Java解释器来解释执行。因此，我们可以认为Java语言编译与解释并存。

## Java语法

### 1.2.1. 字符型常量和字符串常量的区别
1. 形式上：字符常量是单引号引起的一个字符；字符串常量是双引号引起的若干个字符
2. 含义上：字符常量相当于一个整形值（ASCII值），可以参加表达式运算；字符串常量代表一个地址值（该字符串在内存中存放位置）
3. 占内存大小：字符常量只占2个字节；字符串常量占若干个字节（**注意：char在Java中占两个字节**）

> Java编程思想第四版：2.2.2节
> 
> ![](../../images/java/java基本类型.jpg)

### 1.2.2. 关于注释
Java中的注释有三种：
1. 单行注释
2. 多行注释
3. 文档注释

在我们编写代码的时候，如果代码量比较少，我们自己或者团队其他成员还可以很轻易地看懂代码，但是当项目结构一旦复杂起来，我们就需要用到注释了。注释并不会执行，是我们程序员学给自己看的，注释是你的代码说明书，能够帮助看代码的人快速地理清代码之间的逻辑关系。因此，在写程序的时候随手加上注释是一个非常好的习惯。

《Clean Code》这本书明确指出：
> **代码的注释不是越详细越好。实际上好的代码本身就是注释，我们要尽量规范和美化自己的代码来减少不必要的注释。**
> 
> **若编程语言足够有表达力，就不需要注释，尽量通过代码来阐述。**
> 
> 举个例子:
> 
> 去掉下面复杂的注释，只需要创建一个与注释所言同一事物的函数即可
> ```java
> // check to see if the employee is eligible for full benefits
> if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
> ```
> 应替换为
> ```java
> if (employee.isEligibleForFullBenefits())
> ```

### 1.2.3. 标识符和关键字的区别是什么
在我们编写程序的时候，需要大量地为程序、类、变量、方法等取名字，于是就有了标识符，简单来说，标识符就是一个名字。但是有一些标识符，Java语言已经赋予了其特殊的含义，只能用于特定的地方，这种特殊的标识符就是关键字。

### 1.2.4. Java中有哪些常见的关键字？
| 访问控制             | private  | protected  | public   |              |            |           |        |
| -------------------- | -------- | ---------- | -------- | ------------ | ---------- | --------- | ------ |
| 类，方法和变量修饰符 | abstract | class      | extends  | final        | implements | interface | native |
|                      | new      | static     | strictfp | synchronized | transient  | volatile  |        |
| 程序控制             | break    | continue   | return   | do           | while      | if        | else   |
|                      | for      | instanceof | switch   | case         | default    |           |        |
| 错误处理             | try      | catch      | throw    | throws       | finally    |           |        |
| 包相关               | import   | package    |          |              |            |           |        |
| 基本类型             | boolean  | byte       | char     | double       | float      | int       | long   |
|                      | short    | null       | true     | false        |            |           |        |
| 变量引用             | super    | this       | void     |              |            |           |        |
| 保留字               | goto     | const      |          |              |            |           |        |

### 1.2.5. continue、break和return的区别是什么？
在循环结构中，当循环条件不满足或者循环次数达到要求时，循环会正常结束。但是，有时候可能需要在循环的过程中，当满足了某种条件之后，提前终止循环，这就需要用到下面几个关键词：
1. continue：指跳出当前的这一次循环，继续下一次循环。
2. break：指跳出整个循环体，继续执行循环下面的语句。

return用于跳出所在的方法，结束该方法的运行。return一般有两种用法：
1. `return;`:直接使用return结束方法的执行，用于没有返回值函数的方法
2. `return value;`:return一个特定值,用于有返回值函数的方法

### 1.2.7. Java泛型了解么？什么是类型擦除？介绍一下常用的通配符？
Java泛型（generics）是JDK5中引入的一个新特性，泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

**Java的泛型是伪泛型，这是因为Java在编译期间，所有的泛型信息都会被擦掉，这也就是通常所说类型擦除。更多关于类型擦除的问题，可以i查看这篇文章：[《Java泛型类型擦除以及类型擦除带来的问题》](https://www.cnblogs.com/wuqinglong/p/9456193.html)**

```java
List<Integer> list = new ArrayList<>();

list.add(12);
//这里直接添加会报错
list.add("a");
Class<? extends List> clazz = list.getClass();
Method add = clazz.getDeclaredMethod("add", Object.class);
//但是通过反射添加，是可以的
add.invoke(list, "kl");

System.out.println(list);

```

1. 泛型类：
```java
//此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型
//在实例化泛型类时，必须指定T的具体类型
public class Generic<T>{ 

    private T key;

    public Generic(T key) { 
        this.key = key;
    }

    public T getKey(){ 
        return key;
    }
}

```

如何实例化泛型类：
```java
Generic<Integer> genericInteger = new Generic<Integer>(123456);

```

2. 泛型接口：
```java
public interface Generator<T> {
    public T method();
}

```

