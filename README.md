### String、StringBuffer和StringBuilder

这个三个类在我们开发过程中经常会遇到，在处理字符串中的位置相当重要，因此我们必须记住他们之间的差异。

### String和StringBuffer、StringBuilder的区别

String：字符创常量，从名字可以看出，String是不可改变的对象

```java
String s = "abc";
s = s + 1;
Log.e("foin--", s);//输出结果为abc1
```

从上面的代码中我们是明明改变了s的值，为什么我们又说他是不可改变的对象？

其实这只是一种表象，JVM是这么解析这段代码的，首先创建一个s对象，赋值abc，然后再创建一个新的s对象用来执行第行代码，在这个过程中，第一行代码中的s对象并没有发生改变，因此我们每次用String来操作字符串的时候，实际上实在不断创建新的对象，而原来的对象将会变成垃圾被GC回收，由此可见用String来操作字符串效率之低不言而喻！

StringBuffer和StringBuilder：字符串变量，是可变的对象，因此我们在用他们操作字符串的时候，实际上是一直在操作我们声明的对象，就不会像String那样产生额外的消耗，效率自然高了。

> 一个特殊的例子

```java
String s = "Fanshuwei is " + "a " + "good boy!"; 
```

和

```java
StringBuffer sb = new StringBuffer("Fanshuwei is ").append("a ").append("good boy!");
```

在这种情况下，很多人会以为StringBuffer的效率会高于String的效率，其实不然，实际上String对象在此处的引用就相当于

```java
String s = "Fanshuwei is a good boy!"; 
```

因此StringBuffer不会比String快，但是在一下这种情况下StringBuffer就会用明显的优势

```java
String s1 = "Fanshuwei is ";
String s2 = "a ";
String s3 = "good boy";
String s1 = s1 + s2 + s3;
```

这时候JVM就会按照原来的方法去做。

### StringBuffer和StringBuilder的区别

StringBuffer：线程安全

StringBuilder：线程不安全

当我们的字符串缓冲区被多个线程使用时，JVM不能保证StringBuilder的线程是安全的，虽然它的速度最快，但是它可以保证StringBuffer是可以正确操作的，我们大部分时候是在单线程中进行操作，所以更建议使用StringBuilder而不是StringBuffer，就因为StringBuilder的在单线程中效率最快。

### 总结

1. 如果操作少量的数据用String；
2. 单线程下操作大量数据用StringBuilder；
3. 多线程下操作大量数据用StringBuffer。

