---

layout: post

title: "JDK与JRE的区别"

date: Jul 19, 2019 9:21 PM

image: 'http://i2.tiimg.com/693111/649dd4dae3c2974b.jpg'

description: servlet

tags:

- java

- data structure

twitter_text: Lorem ipsum dolor sit amet, consectetur adipisicing elit.

introduction: JSP节课项目遇到的问题

---

# 1.直观区别
从面相对象，主要作用，组成部分三方面对比。如图
![01](https://img-blog.csdn.net/20180804194412881?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM5OTc1NTQy/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
# 2.JDK就是JAVA Development Kit 的英文缩写
1. 主要面相开发人员。开发人员在软件开发时使用的SDK(Software Development Kit 一般指软件开发包)，它提供了Java的开发环境和运行环境。
2. 如果电脑安装了JDK，name不仅可以开发Java程序，也同时具有了运行Java程序的平台。
3. 是整个Java开发的核心，包括了Java运行环境，Java工具和Java基础类库。
# 3.JRE就是Java Runtime Enviroment的英文缩写
1. 主要面相程序使用者
2. 如果年脑安装了JRE，那么只能运行Java程序，不能开发
3. 包括JVM标准实现及Java核心类库。它包括Java虚拟机，Java平台核心类和支持文件。不包括开发工具（编译器，调试器）。同时还包含了编译Java源码的编译器javac，还包含了很多java程序调试和分析的工具：console，jvisualvm等工具软件，还包括了java程序编写所需的文档和demo例子程序
# 4.补充
1. JRE是个运行环境，JDK是个开发环境。因此开发程序时，写的Java程序就是在JDK上，而运行Java程序时候就需要JRE
2. JDK包含了JRE，但是，JRE可以独立安装的
3. JDK，JRE，JVM关系
4. ![](https://img-blog.csdn.net/20180804204658455?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM5OTc1NTQy/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
# 5.题目
1. java程序在执行过程中用到一套JDK工具，其中java.exe是指（B）
	A.Java文档生成器
	B.Java解释器
	C.Java编译器
	D.Java类分解器 
2. JDK安装目录下具有多个文件夹和一些网页文件，其中为java使用者提供的一些已经编好的范例程序的文件夹是（demo）
    JDK安装目录下主要文件夹及文件功能：
    （1）bin文件夹：提供JDK工具程序，包括javac、java、javadoc、appletviewer等可执行程序。
    （2）demo文件夹：Sun公司为Java使用者提供给的一些已经编写好的范例程序。
    （3）jre文件夹：存放Jaca运行环境文件。
    （4）lib文件夹：存放Java的类库文件，即工具程序使用的Java类库。JDK中的工具程序大多也是由Java编写而成。
    （5）include文件夹：存放用于本地方法的文件。

3. （A）称为JAVA开发包或JAVA开发工具，是一个写JAVA的Applet小程序和应用程序的程序开发环境。
	A.JDK
	B.JRE
	C.JVM
4. (C )可以实现Java程序的跨平台运行。
	A.JDK
	B.JRE
	C.JVM
