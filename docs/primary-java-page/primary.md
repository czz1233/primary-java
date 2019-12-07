## Java基础知识
### 1. JDK 和 JRE 有什么区别？
![es-index-type-mapping-document-field](./images/java1.jpg)
### 2. == 和 equals 的区别是什么？
“==”比较的是两个引用在内存中的地址是否相同，也就是说在内存中的地址是否一样。
equals方法是由Object类提供的，可以由子类来进行重写。默认的实现只有当对象和自身进行比较时才会返回true， 这个时候和 “==”是等价的。
Java中很多类（String类 Date类 File类）等都对equals方法进行了重写，这里拿常见的String类举例。