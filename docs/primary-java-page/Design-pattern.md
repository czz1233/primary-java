### 建造者模式（Builder模式）详解
常见到的建造者模式都是xxxBulider，通常都是建造者模式的产物。建造者模式通常有很多变种，但是对于客户端经常使用的是：

`
Food food = new FoodBuilder().a().b().c().build();
Food food = Food.builder().a().b().c().build();
`

####特点：
 
优点：
- 各个建造者相互独立，不干扰。有利于系统的构建
- 客户端不需要知道内部具体怎么实现，便于风险控制

缺点：
- 产品的组成部分必须相同，这限制了使用范围
- 如果产品内部非常复杂，该模式会增加很多建造类
> 建造者（Builder）和工厂模式的关注点不同，建造者关注的是零件组装的过程，而工厂模式关注的是零件创建的过程。

####构建与实现

建造者主要是四个元素组成：
- 产品角色（product）：包含组成部件的复杂对象，由创建者创建具体各个零部件
- 抽象建造者（Builder）：是一个包含创建产品各个子部件的抽象方法的接口，通常还包含返回复杂产品的方法getResult（）。
- 具体建造者（Concrete Builder）:实现Builder的接口，具体实现创建各个部件
- 指挥者（Direct）：它调用建造者中的零部件与装配方法完成复杂对象的创建，指挥者中不涉及具体的产品信息
实现：

1. 创建一个product
```java
package com.chen.designPattern.bulider;

/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class NoodleProduct {
    private String boilFiveMin;
    private String boilTenMin;
    private String boilTwentyMin;

    public String getBoilFiveMin() {
        return boilFiveMin;
    }

    public void setBoilFiveMin(String boilFiveMin) {
        this.boilFiveMin = boilFiveMin;
    }

    public String getBoilTenMin() {
        return boilTenMin;
    }

    public void setBoilTenMin(String boilTenMin) {
        this.boilTenMin = boilTenMin;
    }

    public String getBoilTwentyMin() {
        return boilTwentyMin;
    }

    public void setBoilTwentyMin(String boilTwentyMin) {
        this.boilTwentyMin = boilTwentyMin;
    }

    //显示各个组成信息
    public void show(){

    }
}
```

2.创建一个抽象Builder

```java
package com.chen.designPattern.bulider;

/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public abstract class Builder {
    protected NoodleProduct product =new NoodleProduct();

    //大火煮5分钟
    public abstract void boilFiveMin();
    //大火煮10分钟
    public abstract void boilTenMin() ;
    //大火煮20分钟
    public abstract void boilTwentyMin();
    //返回对象
    public NoodleProduct getResult(){
        return product;
    }
}
```

3.创建Builder的实现

```java
package com.chen.designPattern.bulider;

/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class LanZhouNoodleBuilder extends Builder {
    @Override
    public void boilFiveMin() {
        System.out.println("煮5分钟");

    }

    @Override
    public void boilTenMin() {
        System.out.println("煮10分钟");

    }

    @Override
    public void boilTwentyMin() {
        System.out.println("煮20分钟");
    }

}
```

4.创建Drect

```java
package com.chen.designPattern.bulider;

/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class Direct {

    private Builder builder;

    public Direct(Builder builder) {
        this.builder = builder;
    }

    //组装与配置方法
    public NoodleProduct construct(){
        //让他煮15分钟
        builder.boilFiveMin();
        builder.boilTenMin();
        return builder.getResult();
    }
}

```

5.创建消费者

```java
package com.chen.designPattern.bulider;

/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class Customer {
    public static void main(String[] args) {
        Builder builder=new LanZhouNoodleBuilder();
        Direct direct=new Direct(builder);
        //顾客要煮15分钟的面
        NoodleProduct product=direct.construct();
        product.show();
    }
}

```

####使用场景
`建造者（Builder）`模式适用于创建复杂对象，其产品各个部分经常面临着巨大变化，但是将他们组合在一起的算法是相对稳定的：
- 创建者对象复杂，由多个部件组成，各个部件面临复杂变化，但是结构之间的构造顺序是相对稳定的。
- 创建复杂对象的算法应该独立于该对象组成部分以及装配方式，就是产品的构建与最终的表示是相对独立的。
>建造者（Builder）模式在应用过程中可以根据需要改变，如果创建的产品种类只有一种，只需要一个具体建造者，这时可以省略掉抽象建造者，甚至可以省略掉指挥者角色。
##构造模式
###代理（Proxy）模式
为某对象提供一种代理以控制对该对象的访问。即客户端通过代理间接的访问该对象，从而限制、修改、增强该对象的一些属性。

通俗的来讲就是，在某些情况下客户不能直接访问另一个对象，这时需要中介来进行访问。这个中介就是代理对象。

在软件设计中也经常使用代理模式。eg：要远程访问对象文件比较大(视频/图片)，下载需要使用很多时间，但是还要考虑安全因素，因此因该使用代理模式。

####特点
优点：
- 代理模式是客户端与目标端之间的一个中介起到保护目标对象的作用
- 代理模式可以起到增强目标对象的作用
- 代理模式能将客户端与目标对象分离，在一定程度上解决了耦合度

缺点：
- 在客户端与目标端之间增加一个代理对象，会造成请求变慢
- 增加了系统的复杂度
####结构与实现
模式的结构：
- 抽象主题（Subject）类：通过接口或抽象类声明真实主题和代理对象的实现方法。
- 真实主题（real Subject）类：实现抽象主题中具体的业务，是代理对象所要代理的对象，是要最终引用的对象。
- 代理（proxy）类:实现与抽象主题，对真实主题进行扩展/增强

实现：

1.抽象主题类

```java
package com.chen.designPattern.proxy;

/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public interface FoodService {
    public Food LanzhouNoodle();
    public Food beefSoup();
}

```

2.真实主题类

```java
package com.chen.designPattern.proxy;

/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class FoodServiceImpl implements FoodService {
    @Override
    public Food LanzhouNoodle() {
        Food food=new Food();
        food.setNoodle("面");
        food.setWater("水");
        return food;
    }

    @Override
    public Food beefSoup() {
        Food food=new Food();
        food.setBeef("牛肉");
        food.setWater("水");
        return food;
    }
}

```

3.代理类

```java
package com.chen.designPattern.proxy;

/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class FoodServiceProxy implements FoodService{
    //在增强前先实现
    private FoodServiceImpl foodServiceImpl=new FoodServiceImpl();
    @Override
    public Food LanzhouNoodle() {
        System.out.println("开始做面");
        Food food= foodServiceImpl.LanzhouNoodle();
        //增强
        food.setHujiao("胡椒");
        System.out.println("结束");
        return food;
    }

    @Override
    public Food beefSoup() {
        System.out.println("开始");
        Food food=foodServiceImpl.beefSoup();
        System.out.println("结束");
        return food;

    }
}

```

- 调用

```java
public class Customer {
    public static void main(String[] args) {
        FoodServiceProxy foodServiceProxy=new FoodServiceProxy();
        foodServiceProxy.beefSoup();
        foodServiceProxy.LanzhouNoodle();
    }
}
```
####使用场景
- 远程代理：隐藏目标对象存在于不同的地址空间中，方便访问。
- 虚拟代理：这种通信方式通常应用于创建的目标对象开销很大。
- 安全代理：对不同的用户进行安全访问控制，权限的管理
- 延迟加载：提高系统性能，延迟对目标加载
>真实主题于代理主题一一对应，只增强真实主题也需要增强代理。
>设计代理模式以前真实主题必须事先存在，但是采用动态代理可以解决。
###适配（Adapter）模式
###桥接（Bridge）模式
###装饰者（Decorator）模式
###外观（Facade）模式
###享元（Flyweight）模式
###组合（Composite）模式