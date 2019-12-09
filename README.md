# 互联网 Java 工程师基础知识完全扫盲<sup>[©](https://github.com/czz1233)</sup>

 
   |
| [![license](https://badgen.net/github/license/czz1233/primary-java?color=green)](https://github.com/czz1233/primary-java/blob/master/LICENSE) | [![original](https://badgen.net/badge/original/%E4%B8%AD%E5%8D%8E%E7%9F%B3%E6%9D%89/orange)](https://github.com/czz1233/primary-java)|[![notice](https://badgen.net/badge/notice/%E7%BB%B4%E6%9D%83%E8%A1%8C%E5%8A%A8/red)](/docs/from-readers/rights-defending-movement.md)
| [![wechat-group](https://badgen.net/badge/chat/%E5%BE%AE%E4%BF%A1%E4%BA%A4%E6%B5%81/138c7b)](#公众号)
 | [![reading](https://badgen.net/badge/books/read%20together/cyan)](https://github.com/doocs/technical-books)
 | [![coding](https://badgen.net/badge/leetcode/coding%20together/cyan)](https://github.com/doocs/leetcode)
 | [![doocs](https://badgen.net/badge/organization/join%20us/cyan)](https://doocs.github.io/#/?id=how-to-join)
 | [![stars](https://badgen.net/github/stars/czz1233/primary-java)](https://github.com/czz1233/primary-java/stargazers)
| [![contributors](https://badgen.net/github/contributors/czz1233/primary-java)](https://github.com/czz1233/primary-java/tree/master/docs/from-readers#contributors)
| [![help-wanted](https://badgen.net/github/label-issues/czz1233/primary-java/help%20wanted/open)](https://github.com/czz1233/primary-java/labels/help%20wanted)
| [![issues](https://badgen.net/github/open-issues/czz1233/primary-java)](https://github.com/czz1233/primary-java/issues)
| [![PRs Welcome](https://badgen.net/badge/PRs/welcome/green)](http://makeapullrequest.com)

总结内容大部分来自于网络和实际笔试和面试经验，内容涵盖[java基础](#java基础)、[容器](#容器)、[多线程](#多线程)、[常用设计模式](#常用设计模式)、[Spring/SpringMVC](#Spring/SpringMVC)、[SpringBoot/SpringCloud](#SpringBoot/SpringCloud)、[Mybatis](#Mybatis)、[Kafka](#Kafka)、[Zookeeper](#Zookeeper)、[MySql](#MySql)、[Redis](#Redis)、[JVM](#JVM)

此项目为知乎 `12个模块 150 道 java 必考面试题`的升级版，更新目录和内容。配合项目食用，效果更佳！！
***
### java基础
### [java基础](/docs/primary-java-page/primary.md)
[1. JDK 和 JRE 有什么区别？](/docs/primary-java-page/primary.md?id=_1jdk-和-jre-有什么区别？)

[2. == 和 equals 的区别是什么？](/docs/primary-java-page/primary.md?id=_2-和-equals-的区别是什么？)

[3. 两个对象的 hashCode()相同，则 equals()也一定为 true，对吗？](/docs/primary-java-page/primary.md?id=_3-两个对象的-hashcode相同，则-equals也一定为-true，对吗？)

[4. final在 java 中有什么作用？](/docs/primary-java-page/primary.md?id=_4-final在-java-中有什么作用？)

[5.  java 中的 Math.round(-1.5) 等于多少？](/docs/primary-java-page/primary.md?id=_5-java-中的-mathround-15-等于多少？)

[6. String 属于基础的数据类型吗？](/docs/primary-java-page/primary.md?id=_6-string-属于基础的数据类型吗？)

[7. java 中操作字符串都有哪些类？它们之间有什么区别？](/docs/primary-java-page/primary.md?id=_7-java-中操作字符串都有哪些类？它们之间有什么区别？)

[8. String str="i"与 String str=new String(“i”)一样吗？](/docs/primary-java-page/primary.md?id=_8-string-strquotiquot与-string-strnew-stringi一样吗？)

[9. 如何将字符串反转？](/docs/primary-java-page/primary.md?id=_9-如何将字符串反转？)

[10. String 类的常用方法都有那些？](/docs/primary-java-page/primary.md?id=_10-string-类的常用方法都有那些？)

[11. 抽象类必须要有抽象方法吗？](/docs/primary-java-page/primary.md?id=_11-抽象类必须要有抽象方法吗？)

[12. 普通类和抽象类有哪些区别？](/docs/primary-java-page/primary.md?id=12-普通类和抽象类有哪些区别？)

[14. 接口和抽象类有什么区别？](/docs/primary-java-page/primary.md?id=_14-接口和抽象类有什么区别？)

[15. java 中 IO 流分为几种？](/docs/primary-java-page/primary.md?id=_15-java-中-io-流分为几种？)

[16. BIO、NIO、AIO 有什么区别？](/docs/primary-java-page/primary.md?id=_16-bio、nio、aio-有什么区别？)

[17. Files的常用方法都有哪些？](/docs/primary-java-page/primary.md?id=_17-files的常用方法都有哪些？)
## 容器
### [容器](/docs/primary-java-page/container.md)

[18. java 容器都有哪些？](/docs/primary-java-page/container.md?id=_18-java-容器都有哪些？)

[19. Collection 和 Collections 有什么区别？](/docs/primary-java-page/container.md?id=_19-collection-和-collections-有什么区别？)

[20. List、Set、Map 之间的区别是什么？](/docs/primary-java-page/container.md?id=_20-list、set、map-之间的区别是什么？)

[21. 如何决定使用 HashMap 还是 TreeMap？](/docs/primary-java-page/container.md?id=_21-如何决定使用-hashmap-还是-treemap？)

[22. 如何实现数组和 List 之间的转换？](/docs/primary-java-page/container.md?id=_22-如何实现数组和-list-之间的转换？)

[23. 哪些集合类是线程安全的？](/docs/primary-java-page/container.md?id=_23-哪些集合类是线程安全的？)

[24. 迭代器 Iterator 是什么？](/docs/primary-java-page/container.md?id=_24-迭代器-iterator-是什么？)

[25. Iterator 和 ListIterator 有什么区别？](/docs/primary-java-page/container.md?id=_25-iterator-和-listiterator-有什么区别？)

[26. 怎么确保一个集合不能被修改？](/docs/primary-java-page/container.md?id=_26-怎么确保一个集合不能被修改？)
## 多线程
### [多线程](/docs/primary-java-page/Multi-threaded.md)

[27. 并行和并发有什么区别？](/docs/primary-java-page/Multi-threaded.md?id=_27-并行和并发有什么区别？)

[28. 线程和进程的区别？](/docs/primary-java-page/Multi-threaded.md?id=_28-线程和进程的区别？)

[29. 守护线程是什么？](/docs/primary-java-page/Multi-threaded.md?id=_29-守护线程是什么？)

[30. 创建线程有哪几种方式？](/docs/primary-java-page/Multi-threaded.md?id=_30-创建线程有哪几种方式？)

[31. 说一下 runnable 和 callable 有什么区别？](/docs/primary-java-page/Multi-threaded.md?id=_31-说一下-runnable-和-callable-有什么区别？)

[32. 线程有哪些状态？](/docs/primary-java-page/Multi-threaded.md?id=_32-线程有哪些状态？)

[33. 序列化和反序列化](/docs/primary-java-page/Multi-threaded.md?id=_33-序列化和反序列化)

[34. 线程池中 submit()和 execute()方法有什么区别？](/docs/primary-java-page/Multi-threaded.md?id=_34-线程池中-submit和-execute方法有什么区别？)

[35. 在 java 程序中怎么保证多线程的运行安全？](/docs/primary-java-page/Multi-threaded.md?id=_35-在-java-程序中怎么保证多线程的运行安全？)

[36. 多线程锁的升级原理是什么？](/docs/primary-java-page/Multi-threaded.md?id=_36-多线程锁的升级原理是什么？)

[37. 什么是死锁？](/docs/primary-java-page/Multi-threaded.md?id=_37-什么是死锁？)

[38. 怎么防止死锁？](/docs/primary-java-page/Multi-threaded.md?id=_38-怎么防止死锁？)

[39. ThreadLocal 是什么？有哪些使用场景？](/docs/primary-java-page/Multi-threaded.md?id=_39-threadlocal-是什么？有哪些使用场景？)

[40. 说一下 synchronized 底层实现原理？](/docs/primary-java-page/Multi-threaded.md?id=_40-说一下-synchronized-底层实现原理？)

[41. synchronized 和 volatile 的区别是什么？](/docs/primary-java-page/Multi-threaded.md?id=_41-synchronized-和-volatile-的区)

[42. synchronized 和 Lock 有什么区别？](/docs/primary-java-page/Multi-threaded.md?id=_42-synchronized-和-lock-有什么区别？)

[43. synchronized 和 ReentrantLock 区别是什么？](/docs/primary-java-page/Multi-threaded.md?id=_43-synchronized-和-reentrantlock-区别是什么？)

[44. 说一下 atomic 的原理](/docs/primary-java-page/Multi-threaded.md?id=_44-说一下-atomic-的原理)
## 常用设计模式
## Spring/SpringMVC
## SpringBoot/SpringCloud
## Mybatis
## Kafka
## Zookeeper
## MySql
## Redis
## JVM



