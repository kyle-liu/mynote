# Java ClassLoader
###什么是ClassLoader
&emsp;&emsp;我们都知道，当我们写好一个JAVA程序后，不管是我们自己手动通过javac编译，还是通过IDE开发自动编译，我们写的.java文件会最终生成一堆.class文件。当JVM要执行我们所写的程序时，其实就是要解析并执行这些.class文件。  
&emsp;&emsp;首先JVM会找到程序的入口类，一般即拥有public static void main(String[] args)这个类，因为要执行main方法，所以要先要加载这个方法所在的.class文件，然后在后续过程中“按需加载”———加载main方法所在类的class文件时以及执行main方法过程所需要用到其他的class文件。这些class文件会通过JVM的ClassLoader加载到JVM内存并且在JVM的方法区中每一个加载的class文件会对应一个Class对象，这个Class对象实际上是某个class文件在JVM中一种runtime表现，它包含着某个class所有的元数据。  
&emsp;&emsp;综上所述，class文件从外部硬盘(或者字节流、网络)进入到JVM的内存并创建对应的Class对象的过程称之为“类加载”，那么负责完成这个过程的工具就叫做“ClassLoader”。

###JVM默认提供的ClassLoader


###ClassLoader加载机制

###自定义ClassLoader