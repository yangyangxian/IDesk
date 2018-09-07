String经常在一个语言中或多或少都有些特殊地位。在Java亦不例外。今天先来讨论，String是不可变的。

String是引用类型，String变量储存一个地址，地址指向内存堆中的String对象。当我们说变量不可变，有两种不可变性：
1. 变量储存的地址不可变；
2. 地址指向的对象内容不可变。

String的不可变指的是哪一种？下面用例子来看。

通常有人在疑问String不可变时，会举这样的例子：我们平时不都像下面这样在“修改”String字符串吗：
```java
String s = "hello,world";
s = "Hello,coder";
System.out.println(s);    //Hello,coder
```
我认为这只是一个语义上的误导。赋值操作符`=`通常作用于基本数据类型时，确是修改变量的值。所以在这里让人误以为也是修改了变量的内容。但是对于引用类型String，`s="Hello,coder"`的实际作用是将变量`s`指向另一个内容为`Hello,coder`的新的对象。

所以，对于String不可变性的结论显而易见了：String变量指向的地址是可变的，他的不可变性当然说的是第二种——地址指向的对象内容不可变。

纵览String的方法，String类确实没有提供能从String外部修改对象的方法。我们熟悉的`replace`,`substring`等等方法都要返回一个String，其实都是在返回一个新的对象，而没有修改原有的对象。

为什么要设计成对象内容不可变？

#### String常量池
一个说法是便于实现**String常量池**。String存在于常量池中，当新创建一个字符串变量，如果字符串在内存中已经存在，那么就会把这个已经存在于常量池对象的地址赋给变量。这样可节省内存开销。

但这不完全对。

只有两种情况下创建的String变量，他们才会指向常量池中的同一对象：
* String是字面直接量赋值创建。字面直接量是编译期常量，变量会指向常量池中的对象。所有字面量赋值创建的String变量都会指向常量池中的对象。
* 通过String类的intern()方法得到String变量也是指向常量池中的对象。

但是通过构造函数`new String()`的并不是。通过构造函数创建的String变量在机制上与其他对象一致，都是在heap上创建新的对象，然后把引用赋给变量。

简单例子验证。
```java
String a = "hello,world";
String b = "hello,world";
boolean c = (a == b);                  //true

String d = new String("hello,world");
String e = new String("hello,world");;
boolean f = (d == e);                  //false

String g = d.intern();
boolean h = (a == g);                 //true
```
此外，String的方法`substring`,`relpace`和`split`等方法实现均是调用了构造函数创建了新的对象，所以他们返回的String也都是存在于heap上的新对象。

综上来看似乎节省不了多少内存，毕竟程序中编译常量是少数，大多数String都是在运行时产生。

#### 线程安全
这一点显而易见，对象内容都不可变了，自然不会有线程安全问题。

#### 代码安全
String经常被用来存储server connection, database connection或者file path等等。如果String可变，一旦代码某处改动了字符串，会对系统有安全和稳定性威胁。发生在其他普通字符串，则是不可预料的bug。尤其是代码复杂度很高的时候，一个字符串对象被多个变量引用，直接修改对象内容，引起所有引用该对象的变量都发生变化，容易引起bug。

当然这一点主要是降低程序员的错误和bug的可能。

其实，话说回来，在JAVA里，String不可变也并非特殊，所有包装类Interger，Boolean等都是不可变类。