### 建造者模式（Builder模式）详解
常见到的建造者模式都是xxxBulider，通常都是建造者模式的产物。建造者模式通常有很多变种，但是对于客户端经常使用的是：

`
Food food = new FoodBuilder().a().b().c().build();
Food food = Food.builder().a().b().c().build();
`

###特点：
 
优点：
- 各个建造者相互独立，不干扰。有利于系统的构建
- 客户端不需要知道内部具体怎么实现，便于风险控制

缺点：
- 产品的组成部分必须相同，这限制了使用范围
- 如果产品内部非常复杂，该模式会增加很多建造类
> 建造者（Builder）和工厂模式的关注点不同，建造者关注的是零件组装的过程，而工厂模式关注的是零件创建的过程。

###构建与实现

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

###使用场景
`建造者（Builder）`模式适用于创建复杂对象，其产品各个部分经常面临着巨大变化，但是将他们组合在一起的算法是相对稳定的：
- 创建者对象复杂，由多个部件组成，各个部件面临复杂变化，但是结构之间的构造顺序是相对稳定的。
- 创建复杂对象的算法应该独立于该对象组成部分以及装配方式，就是产品的构建与最终的表示是相对独立的。
>建造者（Builder）模式在应用过程中可以根据需要改变，如果创建的产品种类只有一种，只需要一个具体建造者，这时可以省略掉抽象建造者，甚至可以省略掉指挥者角色。