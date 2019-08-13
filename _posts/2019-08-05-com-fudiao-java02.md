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

# 简单了解JVM的内存分配
	在jvm中，内存分为堆内存跟栈内存。二者区别是：当我们创建一个对象（new Object）时，就会调用对象的构造函数来开辟空间，将对象数据存储到堆内存中，与此同时在栈内存生成对应的引用，当我们在后续代码中调用的时候用的都是栈内存中的引用。还需注意一点，基本数据类型是存储在栈内存中
    
# 简单认识equals与==的区别
   1. ==是判断两个变量或实例是不是只想同一个内存空间，equals是判断两个变量或实力所指向的内存空间值是不是相同
   2. ==是指对内存地址进行比较，equals（）是对字符串的内容比较
   3. ==指引用是否相同，equals（）是指值是否相同
   
# 用一张图表现
![](https://img-blog.csdn.net/20180602183200272?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2NTIyMzA2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
#==与equals区别详解

等号比较的是变量(栈)内存中存放的对象的(堆)内存地址，用来判断两个对象的地址是否相同，即是否是指相同一个对象。比较的是真正意义上的指针操作。equals用来比较的是两个对象的内容是否相等，由于所有的类都是继承自java.lang.Object类的，所以适用于所有对象，如果没有对该方法进行覆盖的话，调用的仍然是Object类中的方法，而Object中的equals方法返回的却是==的判断。String s="abcd"是一种非常特殊的形式,和new 有本质的区别。它是java中唯一不需要new 就可以产生对象的途径。以String s="abcd";形式赋值在java中叫直接量,它是在常量池中而不是象new一样放在压缩堆中。 这种形式的字符串，在JVM内部发生字符串拘留，即当声明这样的一个字符串后，JVM会在常量池中先查找有有没有一个值为"abcd"的对象,如果有,就会把它赋给当前引用.即原来那个引用和现在这个引用指点向了同一对象, 如果没有,则在常量池中新创建一个"abcd",下一次如果有String s1 = "abcd";又会将s1指向"abcd"这个对象,即以这形式声明的字符串,只要值相等,任何多个引用都指向同一对象.
而String s = new String("abcd");和其它任何对象一样.每调用一次就产生一个对象，只要它们调用。
也可以这么理解: String str = "hello"; 先在内存中找是不是有"hello"这个对象,如果有，就让str指向那个"hello".
如果内存里没有"hello"，就创建一个新的对象保存"hello". String str=new String ("hello") 就是不管内存里是不是已经有"hello"这个对象，都新建一个对象保存"hello"
