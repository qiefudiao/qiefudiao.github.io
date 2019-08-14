---

layout: post

title: "==和equals区别"

date: Jul 19, 2019 9:21 PM

image: 'http://i2.tiimg.com/693111/649dd4dae3c2974b.jpg'

description: servlet

tags:

- java

- data structure

twitter_text: Lorem ipsum dolor sit amet, consectetur adipisicing elit.

introduction: JSP节课项目遇到的问题

---

# 基本类型变量

| 基本类型 | 字节大小 |	默认值 | 封装类 |
|---------|---------|---------||---------|
|byte|1|0|Byte|
|short|2|0|Short|
|int|4|0|Integer|
|long|8|0L|Long|
|boolean|-|false|Boolean|
|char|2|null|Character|
|float|4|0.0f|Float|
|double|8|0.0d|Double|

# Switch能用的参数类型
在 Java 7之前，switch 只能支持 byte、short、char、int或者其对应的封装类以及 Enum 类型。在 Java 7中，String支持被加上了。

# Object的公用方法
1. clone
	保护方法，实现对象的浅复制，只有实现了Cloneable接口才可以调用该方法，否则抛出CloneNotSupportedException异常
2. euqals
	在Object中与==是一样的，子类一般需要重写该方法
3. hashCode
	该方法用于哈希查找，重写了equals方法一般都要重写hashCode方法。这个方法在一些具有哈希功能的Collection中用到
4. getClass
	final方法，获得运行时类型
5. wait
	使当前线程等待该对象的锁，当前线程必须是该对象的拥有者，也就是具有该对象的锁。wait()方法一直等待，直到获得锁或者被中断。wait(long timeout)设定一个超时间隔，如果在规定时间内没有获得锁就返回。

	调用该方法后当前线程进入睡眠状态，直到以下事件发生：
	1. 其他线程调用了该对象的notify方法
	2. 其他线程调用了该对象的notifyAll方法
	3. 其他线程调用了interrupt中断该线程
	4. 时间间隔到了
	此时该线程就可以被调度了，如果是被中断的话就抛出一个InterruptedException异常
6. notify
	唤醒在该对象上等待的某个线程
7. notifyAll
	唤醒在该对象上等待的所有线程
8. toString
	转换成字符串，一般子类都有重写，否则打印句柄

# hashcode的作用
hashCode用于返回对象的散列值，用于在散列函数中确定放置的桶的位置。

1. hashCode的存在主要是用于查找的快捷性，如Hashtable，HashMap等，hashCode是用来在散列存储结构中确定对象的存储地址的；

2. 如果两个对象相同，就是适用于equals(java.lang.Object) 方法，那么这两个对象的hashCode一定要相同；

3. 如果对象的equals方法被重写，那么对象的hashCode也尽量重写，并且产生hashCode使用的对象，一定要和equals方法中使用的一致，否则就会违反上面提到的第2点；

4. 两个对象的hashCode相同，并不一定表示两个对象就相同，也就是不一定适用于equals(java.lang.Object) 方法，只能够说明这两个对象在散列存储结构中，如Hashtable，他们“存放在同一个篮子里”。

# hashMap和hashTable区别
Hashtable和HashMap类有三个重要的不同之处。

1. 第一个不同主要是历史原因。Hashtable是基于陈旧的Dictionary类的，HashMap是Java 1.2引进的Map接口的一个实现。

2. 也许最重要的不同是Hashtable的方法是同步的，但是这也是HashTable效率低下的原因，任何方法都是同步的，而HashMap的方法不是。这就意味着，虽然你可以不用采取任何特殊的行为就可以在一个多线程的应用程序中用一个Hashtable，但你必须同样地为一个HashMap提供外同步。一个方便的方法就是`利用Collections类的静态的synchronizedMap()方法`，它创建一个线程安全的Map对象，并把它作为一个封装的对象来返回。这个对象的方法可以让你同步访问潜在的HashMap。这么做的结果就是当你不需要同步时，你不能切断Hashtable中的同步（比如在一个单线程的应用程序中），而且同步增加了很多处理费用。

3. 第三点不同是，只有HashMap可以让你将空值作为一个表的条目的key或value。HashMap中只有一条记录可以是一个空的key，但任意数量的条目可以是空的value。这就是说，如果在表中没有发现搜索键，或者如果发现了搜索键，但它是一个空的值，那么get()将返回null。如果有必要，用containKey()方法来区别这两种情况。

一些资料建议，当需要同步时，用Hashtable，反之用HashMap。但是，因为在需要时，HashMap可以被同步，HashMap的功能比Hashtable的功能更多，而且它不是基于一个陈旧的类的，所以有人认为，在各种情况下，HashMap都优先于Hashtable。

# Collection包结构，与Collections的区别
(1) Collection 是单列集合

**List** 元素是有序的、可重复

有序的 collection，可以对列表中每个元素的插入位置进行精确地控制。

可以根据元素的整数索引（在列表中的位置）访问元素，并搜索列表中的元素。

可存放重复元素，元素存取是有序的。

List接口中常用类

- Vector：线程安全，但速度慢，已被ArrayList替代。

底层数据结构是数组结构

- ArrayList：线程不安全，查询速度快。

底层数据结构是数组结构

- LinkedList：线程不安全。增删速度快。

底层数据结构是列表结构

**Set**(集) 元素无序的、不可重复。

取出元素的方法只有迭代器。不可以存放重复元素，元素存取是无序的。

Set接口中常用的类

- HashSet：线程不安全，存取速度快。

它是如何保证元素唯一性的呢？依赖的是元素的hashCode方法和euqals方法。

- TreeSet：线程不安全，可以对Set集合中的元素进行排序。

它的排序是如何进行的呢？通过compareTo或者compare方法中的来保证元素的唯一性。元素是以二叉树的形式存放的。

（2）**Map** 是一个双列集合

- Hashtable:线程安全，速度快。底层是哈希表数据结构。是同步的。

不允许null作为键，null作为值。

- Properties:用于配置文件的定义和操作，使用频率非常高，同时键和值都是字符串。

是集合中可以和IO技术相结合的对象。(到了IO在学习它的特有和io相关的功能。)

- HashMap:线程不安全，速度慢。底层也是哈希表数据结构。是不同步的。

允许null作为键，null作为值。替代了Hashtable.

- LinkedHashMap: 可以保证HashMap集合有序。存入的顺序和取出的顺序一致。

- TreeMap：可以用来对Map集合中的键进行排序.

（3）Collection 和 Collections的区别

Collection是集合类的上级接口，子接口主要有Set 和List。

Collections是针对集合类的一个帮助类，提供了操作集合的工具方法：一系列静态方法实现对各种集合的搜索、排序、线程安全化等操作。

# try catch finally，try里有return，finally还执行么？

执行，并且finally的执行早于try里面的return

结论：

1. 不管有木有出现异常，finally块中代码都会执行；

2. 当try和catch中有return时，finally仍然会执行；

3. finally是在return后面的表达式运算后执行的（此时并没有返回运算后的值，而是先把要返回的值保存起来，管finally中的代码怎么样，返回的值都不会改变，任然是之前保存的值），所以函数返回值是在finally执行前确定的；

4. finally中最好不要包含return，否则程序会提前退出，返回值不是try或catch中保存的返回值。

举例：

情况1：try{} catch(){}finally{} return;

显然程序按顺序执行。

情况2:try{ return; }catch(){} finally{} return;

程序执行try块中return之前（包括return语句中的表达式运算）代码；

再执行finally块，最后执行try中return;

finally块之后的语句return，因为程序在try中已经return所以不再执行。

情况3:try{ } catch(){return;} finally{} return;

程序先执行try，如果遇到异常执行catch块，

有异常：则执行catch中return之前（包括return语句中的表达式运算）代码，再执行finally语句中全部代码，

最后执行catch块中return. finally之后也就是4处的代码不再执行。

无异常：执行完try再finally再return.

情况4:try{ return; }catch(){} finally{return;}

程序执行try块中return之前（包括return语句中的表达式运算）代码；

再执行finally块，因为finally块中有return所以提前退出。

情况5:try{} catch(){return;}finally{return;}

程序执行catch块中return之前（包括return语句中的表达式运算）代码；

再执行finally块，因为finally块中有return所以提前退出。

情况6:try{ return;}catch(){return;} finally{return;}

程序执行try块中return之前（包括return语句中的表达式运算）代码；

有异常：执行catch块中return之前（包括return语句中的表达式运算）代码；

则再执行finally块，因为finally块中有return所以提前退出。

无异常：则再执行finally块，因为finally块中有return所以提前退出。

最终结论：任何执行try 或者catch中的return语句之前，都会先执行finally语句，如果finally存在的话。

如果finally中有return语句，那么程序就return了，所以finally中的return是一定会被return的，编译器把finally中的return实现为一个warning。

# Exception与Error包结构
（1）Java异常

Java中有Error和Exception，它们都是继承自Throwable类。





二者的不同之处

Exception：

可以是可被控制(checked) 或不可控制的(unchecked)。表示一个由程序员导致的错误。应该在应用程序级被处理。

Error：

总是不可控制的(unchecked)。经常用来用于表示系统错误或低层资源的错误。如何可能的话，应该在系统级被捕捉。

异常的分类

Checked exception: 这类异常都是Exception的子类。异常的向上抛出机制进行处理，假如子类可能产生A异常，那么在父类中也必须throws A异常。可能导致的问题：代码效率低，耦合度过高。Unchecked exception: 这类异常都是RuntimeException的子类，虽然RuntimeException同样也是Exception的子类，但是它们是非凡的，它们不能通过client code来试图解决，所以称为Unchecked exception 。

# Interface与abstract类的区别

1. abstract class 在Java中表示的是一种继承关系，一个类只能使用一次继承关系。但是，一个类却可以实现多个interface。
2. 在abstract class 中可以有自己的数据成员，也可以有非abstarct的方法，而在interface中，只能够有静态的不能被修改的数据成员（也就是必须是static final的，不过在 interface中一般不定义数据成员），所有的方法都是public abstract的。
3. 抽象类中的变量默认是 friendly 型，其值可以在子类中重新定义，也可以重新赋值。接口中定义的变量默认是public static final 型，且必须给其赋初值，所以实现类中不能重新定义，也不能改变其值。
4. abstract class和interface所反映出的设计理念不同。其实abstract class表示的是"is-a"关系，interface表示的是"like-a"关系，门和报警的关系。
5. 实现抽象类和接口的类必须实现其中的所有方法。抽象类中可以有非抽象方法。接口中则不能有实现方法。

abstract class 和 interface 是 Java语言中的两种定义抽象类的方式，它们之间有很大的相似性。但是对于它们的选择却又往往反映出对于问题领域中的概念本质的理解、对于设计意图的反映是否正确、合理，因为它们表现了概念间的不同的关系。
抽象类的使用原则如下：
（1）抽象方法必须为public或者protected（因为如果为private，则不能被子类继承，子类便无法实现该方法），缺省情况下默认为public；
（2）抽象类不能直接实例化，需要依靠子类采用向上转型的方式处理；
（3）抽象类必须有子类，使用extends继承，一个子类只能继承一个抽象类；
（4）子类（如果不是抽象类）则必须覆写抽象类之中的全部抽象方法（如果子类没有实现父类的抽象方法，则必须将子类也定义为为abstract类。）；

# foreach与正常for循环对比

循环ArrayList时，普通for循环比foreach循环花费的时间要少一点；循环LinkList时，普通for循环比foreach循环花费的时间要多很多。

当我将循环次数提升到一百万次的时候，循环ArrayList，普通for循环还是比foreach要快一点；但是普通for循环在循环LinkList时，程序直接卡死。


结论：需要循环数组结构的数据时，建议使用普通for循环，因为for循环采用下标访问，对于数组结构的数据来说，采用下标访问比较好。

需要循环链表结构的数据时，一定不要使用普通for循环，这种做法很糟糕，数据量大的时候有可能会导致系统崩溃。


原因：foreach使用的是迭代器