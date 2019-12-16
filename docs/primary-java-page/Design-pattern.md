## 创建型模式
### 单例（Singleton）模式
某个类只能生成一个实例，该类提供了一个全局访问点供外部获取该实例，其拓展是有限多例模式。
### 原型（Prototype）模式
将一个对象作为原型，通过对其进行复制而克隆出多个和原型类似的新实例。 
### 工厂方法（FactoryMethod）模式
定义一个用于创建产品的接口，由子类决定生产什么产品。
### 抽象工厂（AbstractFactory）模式
提供一个创建产品族的接口，其每个子类可以生产一系列相关的产品。
### 建造者（Builder）模式
将一个复杂对象分解成多个相对简单的部分，然后根据不同需要分别创建它们，最后构建成该复杂对象。

### 建造者（Builder）模式详解
常见到的建造者模式都是xxxBulider，通常都是建造者模式的产物。建造者模式通常有很多变种，但是对于客户端经常使用的是：

`
Food food = new FoodBuilder().a().b().c().build();
Food food = Food.builder().a().b().c().build();
`

#### 特点：
 
优点：
- 各个建造者相互独立，不干扰。有利于系统的构建
- 客户端不需要知道内部具体怎么实现，便于风险控制

缺点：
- 产品的组成部分必须相同，这限制了使用范围
- 如果产品内部非常复杂，该模式会增加很多建造类
> 建造者（Builder）和工厂模式的关注点不同，建造者关注的是零件组装的过程，而工厂模式关注的是零件创建的过程。

#### 构建与实现

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

#### 使用场景
`建造者（Builder）`模式适用于创建复杂对象，其产品各个部分经常面临着巨大变化，但是将他们组合在一起的算法是相对稳定的：
- 创建者对象复杂，由多个部件组成，各个部件面临复杂变化，但是结构之间的构造顺序是相对稳定的。
- 创建复杂对象的算法应该独立于该对象组成部分以及装配方式，就是产品的构建与最终的表示是相对独立的。
>建造者（Builder）模式在应用过程中可以根据需要改变，如果创建的产品种类只有一种，只需要一个具体建造者，这时可以省略掉抽象建造者，甚至可以省略掉指挥者角色。
## 构造模式
### 代理（Proxy）模式
为某对象提供一种代理以控制对该对象的访问。即客户端通过代理间接的访问该对象，从而限制、修改、增强该对象的一些属性。

通俗的来讲就是，在某些情况下客户不能直接访问另一个对象，这时需要中介来进行访问。这个中介就是代理对象。

在软件设计中也经常使用代理模式。eg：要远程访问对象文件比较大(视频/图片)，下载需要使用很多时间，但是还要考虑安全因素，因此因该使用代理模式。

#### 特点
优点：
- 代理模式是客户端与目标端之间的一个中介起到保护目标对象的作用
- 代理模式可以起到增强目标对象的作用
- 代理模式能将客户端与目标对象分离，在一定程度上解决了耦合度

缺点：
- 在客户端与目标端之间增加一个代理对象，会造成请求变慢
- 增加了系统的复杂度
#### 结构与实现
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
#### 使用场景
- 远程代理：隐藏目标对象存在于不同的地址空间中，方便访问。
- 虚拟代理：这种通信方式通常应用于创建的目标对象开销很大。
- 安全代理：对不同的用户进行安全访问控制，权限的管理
- 延迟加载：提高系统性能，延迟对目标加载
>真实主题于代理主题一一对应，只增强真实主题也需要增强代理。
>设计代理模式以前真实主题必须事先存在，但是采用动态代理可以解决。
### 适配（Adapter）模式
适配器模式是将现有类的接口转化为客户向要接口，使原本接口不兼容的类转化为可以协同工作的类。
#### 特点
优点：
- 客户端可以通过适配器透明的调用目标接口。
- 复用了现有的类，不需要重新修改原有的代码而重用现有的适配者类。
- 将目标类与适配者类解耦，解决了目标类和适配者类接口不一致的问题。
缺点：
- 对适配器来说更换适配器的实现过程比较复杂。
#### 结构与实现
结构：
- 目标（Target）类：当前业务所需要的接口，它可以是抽象类或接口
- 适配者（Adaptee）类：它是被访问的和适配的现存的接口
- 适配器(Adapter)类：它是一个转化器，通过继承或引用适配者的对象，把接口转化为目标接口，让客户按照目标接口进行访问。

实现：

（1）类适配器

- 适配器

```java
package com.chen.designPattern.adapter;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class ClassCockAdapter extends WildCock implements Duck {
    @Override
    public void quack() {
        goggble();
    }
    @Override
    public void fly() {
        super.fly();
    }
}

```

- 调用
```java

package com.chen.designPattern.adapter;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class AdapterDemo {
    public static void main(String[] args) {
        Duck duck=new ClassCockAdapter();
        duck.quack();
    }
}


```
（2）对象适配器
- 目标类：

```java
package com.chen.designPattern.adapter;

/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public interface Duck {
    //鸭呱呱
    public void quack();
    //鸭飞
    public void fly();
}
package com.chen.designPattern.adapter;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public interface Cock {
    //鸡叫
    public void goggble();
    //鸡飞
    public void fly();
}

```

- 适配者接口实现

```java
package com.chen.designPattern.adapter;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class WildCock implements Cock {
    @Override
    public void goggble() {
        System.out.println("鸡咕咕");
    }
    @Override
    public void fly() {
        System.out.println("鸡飞");
    }
}

```

- 适配器

```java
package com.chen.designPattern.adapter;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class CockAdapter implements Duck{
    //鸡的适配器要实现要适配的对象
    private Cock cock;
    //构造方法要鸡的实例，此类就是要把鸡适配成鸭子
    public CockAdapter(Cock cock) {
        this.cock = cock;
    }
    @Override
    public void quack() {
        cock.goggble();
    }
    @Override
    public void fly() {
        cock.fly();
    }
}

```
>对象适配器就是把鸭子伪装成鸡
#### 使用场景
- 以前开发的功能存在满足新系统功能的类，但是接口与新的系统的接口不一致
- 开发使用第三方使用的组件，但是接口的定义和自己要求的接口定义不同
>适配器可以双向适配

双向适配：

- 适配器文件

```java
package com.chen.designPattern.adapter;
/**
 * @Autre beyond
 * @Data 2019/12/12
 * 双向适配器
 */

public class TwoWayAdapter implements Cock,Duck {
    private Cock cock;
    private Duck duck;
    public TwoWayAdapter(Cock cock) {
        this.cock = cock;
    }
    public TwoWayAdapter(Duck duck) {
        this.duck = duck;
    }
    @Override
    public void goggble() {
        duck.quack();
    }
    @Override
    public void fly() {
        cock.fly();
        duck.fly();
    }
    @Override
    public void quack() {
        cock.goggble();
    }
}

```

- 调用demo

```java
package com.chen.designPattern.adapter;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class AdapterDemo {
    public static void main(String[] args) {
       /* Cock wildCock=new WildCock();
        Duck duck=new CockAdapter(wildCock);
        duck.fly();
        duck.quack();
        //类适配器模式测试
        Duck duck=new ClassCockAdapter();
        duck.quack();
*/
        //双向适配器
        System.out.println("把鸭子变为鸡");
        Cock cock=new WildCock();
        Duck duck=new TwoWayAdapter(cock);
        duck.quack();
        System.out.println("把Duck的鸡变为鸡");
        Cock cock1=new TwoWayAdapter(duck);
        cock1.goggble();
    }
}
```
### 桥接/桥梁（Bridge）模式
在现实生活中，某些具有两个或多个维度的变化。eg按照图像颜色、大小分类。如何设计类似于photoShop这样的软件
能画不同颜色/类型的图像。如果使用继承的方式有mxn种，不但子类多，而且不容易扩展。为了解决这样的问题使用桥接模式
#### 特点
优点：
- 抽象与实现分离，便于扩展
- 其实现对客户透明

缺点：
- 由于聚合关系存在抽象层，要求开发者针对抽象层进行设计编写，者增加了系统理解与设计的难度

#### 结构与实现
结构：取消二者继承关系，改用组合关系
- 抽象化（Abstraction）角色：定义抽象类，并且包含一个对实现化对象的引用。
- 扩展抽象化（Refined Abstraction）角色：是抽象化角色的子类，实现父类中的业务方法，并且通过组合关系调用实现化角色中的业务方法。
- 实现化（Implementor）角色：定义实现化接口，提供扩展抽象化角色的调用。
- 具体实现化（Concre Implementor）角色：具体实现-实现化角色

实现：
- 抽象化（Abstraction）角色

```java

package com.chen.designPattern.Bridge;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public abstract class FileAbstract {
    public FileService fileService;
    public FileAbstract(FileService fileService) {
        this.fileService = fileService;
    }
    public abstract void Operation();
}


```

- 扩展抽象化（Refined Abstraction）角色

```java
package com.chen.designPattern.Bridge;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public  class RefinedFileAbstract extends FileAbstract {
    protected RefinedFileAbstract(FileService fileService) {
        super(fileService);
    }
    @Override
    public void Operation() {
        System.out.println("扩展抽象化(Refined Abstraction)角色被访问" );
        fileService.add();
    }
}



```

- 实现化（Implementor）角色

```java
package com.chen.designPattern.Bridge;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public interface FileService {
    public void add();
}

```

- 具体实现化（Concre Implementor）角色

 ```java
 
package com.chen.designPattern.Bridge;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class FileServiceImpl  implements  FileService{
    @Override
    public void add() {
        System.out.println("文件添加");
    }
}

```  

- 调用

```java

package com.chen.designPattern.Bridge;
/**
 * @Autre beyond
 * @Data 2019/12/12
 */
public class BridgeDemo {
    public static void main(String[] args) {
        FileService fileService=new FileServiceImpl();
        FileAbstract fileAbstract=new RefinedFileAbstract(fileService);
        fileAbstract.Operation();
    }
}

```  

桥接模式通常适用于以下场景:

- 当一个类存在两个独立变化的维度，且这两个维度都需要进行扩展时。
- 当一个系统不希望使用继承或因为多层次继承导致系统类的个数急剧增加时。
- 当一个系统需要在构件的抽象化角色和具体化角色之间增加更多的灵活性时。
    
### 装饰者（Decorator）模式
### 外观（Facade）模式
### 享元（Flyweight）模式
### 组合（Composite）模式