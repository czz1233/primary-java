# 为什么要使用 spring？
- 依赖注入（DI）
- 降低耦合
看到DI也许你会不理解,使用注入会使代码变得更加简洁
测试用例：学生踢球？

    - Ball.java
    ```java
    
    public class Ball {
        public void play(){
        }
    }
    
    ```
    - Foodball.java
    
    ```java
      public class Foodball extends Ball {
      
          @Override
          public void play() {
              System.out.println("玩足球");
          }
      
      }
    
    ```
    - Student.java
    
    ```java
      public class Student {
          private Foodball foodball;
          public Student() {
              foodball=new Foodball();  //高度耦合与Student
          }
      
          public void play(){
              foodball.play();
          }
          @Test
          public void test(){
              Student student=new Student();
              student.play();
          }
          @Test
          public void testCons(){
              Foodball ball=new Foodball();
              StudentConstruct studentConstruct=new StudentConstruct(ball);
              studentConstruct.play();
          }
      }
  ```
上面测试用例可以看出，高度耦合与Student,当学生打篮球时就需要重写代码。所以需要降低耦合。

修改代码为：

 ```java

public class StudentConstruct {
    private Ball ball;
    public StudentConstruct(Ball ball) {
        this.ball = ball;
    }
    public void play(){
        ball.play();
    }
}

```
测试用例在`testCons`方法中。这个使用的是构造方法注入。它解决的无论是什么球student都可以玩
而且不用改代码-降低了耦合。可以使用new的方式，可以用xml方法配置：

xml:

```xml

 <bean id="Foodball" class="com.chen.springDetail.Foodball"/>
    <bean id="StudentConstruct" class="com.chen.springDetail.StudentConstruct">
        <constructor-arg ref="Foodball"/>
    </bean>
    
```

```java
    @Test
    public void assembly(){
        ApplicationContext applicationContext=new ClassPathXmlApplicationContext("application.xml");
        StudentConstruct student= (StudentConstruct) applicationContext.getBean("StudentConstruct");
        student.play();
    }
    
```

- 面向切面（AOP）编程
xml配置：

```xml

<bean id ="record" class="com.chen.springDetail.Record"/>
    <aop:config>
        <aop:aspect ref="record">
            <!--织入点-->
            <aop:pointcut id="play" expression="execution(* com.chen.springDetail.StudentConstruct.play(..))"/>
            <aop:before method="startTime" pointcut-ref="play"/>
            <aop:after method="stopTime" pointcut-ref="play"/>
        </aop:aspect>
    </aop:config>

```

demo:

```java

 @Test
    public void assembly(){
        ApplicationContext applicationContext=new ClassPathXmlApplicationContext("application.xml");
        StudentConstruct student= (StudentConstruct) applicationContext.getBean("StudentConstruct");
        student.play();
    }

```
运行结果：

```java

开始：Fri Dec 20 13:20:31 CST 2019
玩足球
结束：Fri Dec 20 13:20:31 CST 2019

```


![](https://images2017.cnblogs.com/blog/1289075/201711/1289075-20171130164027448-137580909.png)

可以使事务/安全组件/日志模块单独成模块随时调用。

使用AOP用会节省出更多的时间去处理业务问题。

# IoC 属于哪种设计模式？
IOC（Inversion of Control）是一种全新的设计模式：Interface Driven Design接口驱动，接口驱动有很多优点，可以提供不同灵活的子类实现。
增加代码的健壮性，但是接口一定要实现aInterface=new aInterfaceImpl()，但是这样耦合就会出现。

IoC模式，系统中通过引入实现了IoC模式的IoC容器，即可由IoC容器来管理对象的生命周期、依赖关系等，从而使得应用程序的配置和依赖性规范与实际的应用程序代码分离。其中一个特点就是通过文本的配置文件进行应用程序组件间相互关系的配置，而不用重新修改并编译具体的代码。

可以把IoC模式看作工厂模式的升华，把IoC容器看作是一个大工厂，只不过这个大工厂里要生成的对象都是在XML文件中给出定义的。利用Java 的“反射”编程，根据XML中给出的类定义生成相应的对象。从实现来看，以前在工厂模式里写死了的对象，IoC模式改为配置XML文件，这就把工厂和要生成的对象两者隔离，极大提高了灵活性和可维护性。

# 谈谈你对 Spring IoC 和 DI 的理解，它们有什么区别？
IOC:将类的创建的对象交给Spring管理
DI：依赖注入，将类里面的属性在创建的时候赋值。
DI和IOC之间的关系：DI不能单独存在，需要在IOC的基础之上来完成。

# 简单谈谈 IoC 容器的原理。
IOC的原理：
- 开始加载：

```java

    ApplicationContext context = new ClassPathXmlApplicationContext("classpath:applicationfile.xml");

```
![](https://www.javadoop.com/blogimages/spring-context/1.png)

从这个类图中可以看出ClassPathXmlApplicationContext只是其中一个启动方式。

FileSystemXmlApplicationContext 是使用xml的绝对路径。

AnnotationConfigApplicationContext ：使用注解来配置。
![](/images/ClassPathXmlApplicationContext.png)
- 测试

# bean 的 scope 有几种类型？请详细列举。

# 说说 IoC 中的继承和 Java 继承的区别。

# IoC 中 car 对象的配置如下，现在要添加 user 对象，并且将 car 注入到 user 中，正确的配置是？

```java
<bean id="car" class="com.southwind.entity.Car"></bean>
```

# 请分别写出 IoC 静态工厂方法和实例工厂方法的配置。

# IoC 自动装载有几种方式？

# 介绍一下 Spring 框架中 bean 的生命周期。

# IoC 容器自动完成装载，默认的方式是？
