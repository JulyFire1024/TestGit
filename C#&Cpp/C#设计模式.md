博文： [https://www.cnblogs.com/wyy1234/category/1341803.html](https://www.cnblogs.com/wyy1234/category/1341803.html)


-----
1、总述

- 设计模式（Design pattern）是帮助解决实际开发过程中的方法，
- 这些方法是为了降低对象之间的耦合度。将其总结为若干种设计模式。
- 使用设计模式是为了可重用代码、代码更容易被他人理解和维护、保证代码可靠性。
- 设计模式使得代码编制真正工程化，是软件工程的基石脉络。
- 分类为：
  - 创建型模式
    - 工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式
  - 结构型模式
    - 适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式
  - 行为型模式
    - 策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式。

- 遵循的设计原则
  - 单一职责原则，一个类只负责一些特定的关联度极高的职责
  - 接口隔离原则，使用多个专门的接口
  - 开闭原则，对添加（拓展）开放，对修改关闭，方便拓展的同时避免修改带来的已有功能的颠覆
  - 里氏替代原则，父类存在的地方，子类都可以替换，且行为不发生改变
  - 合成复用原则，对象A中包含了另一个对象B,A就可以委托B来实现B的功能
  - 依赖倒置原则，方便实现类的切换，降低业务要求和具体实现间的耦合
  - 迪米特法则，最小知道原则，类与类之间应当尽可能地不了解，最好是相互独立的，彼此通信最好通过第三方进行



-----


-----
2、单例模式

一个类只能有一个实例，类只在类内部创建自己的唯一实例，然后对外提供这一实例，

外部无法对此类实例化

- 意图：保证一个类仅有一个实例，并提供一个访问它的全局访问点。
- 主要解决：一个全局使用的类频繁地创建与销毁。
- 何时使用：当想控制实例数目，节省系统资源的时候。
- 如何解决：判断系统是否已经有这个单例，如果有则返回，如果没有则创建。
- 关键代码：
  - 将构造函数私有private，使得其在外部无法用new来实例化
  - 全局唯一，用static关键字来在类内创建实例使其属于全局
  - 提供一个供外部访问的变量，访问该变量时，若唯一实例为空，则创建唯一实例，若唯一实例已存在，则返回唯一实例

  public class MySingLeton

  {

  private static MySingleton \_instance;

  public static MySingleton Instance

  {

  get

    {

  - [ ] if(\_instance == null) \_instance == new MySingleton();

  return \_instance;

  }

  }



-----
3、观察者模式

定义一种一对多的依赖关系，让多个观察者对象同时监听某一个主题对象，对象在状态发生变化时，会通知所有的观察者对象，使他们能够自动更新自己，常用于实现事件处理系统。也称为发布/订阅模式。

- 意图：定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新。
- 主要解决：多个对象状态改变依赖于某一个对象，考虑易用和低耦合，保证高度的协作。
- 何时使用：一个对象（目标对象）的状态发生改变，所有的依赖对象（观察者对象）都将得到通知，进行广播通知。
- 如何解决：使用面向对象技术，可以固定实现依赖关系，无须时刻考虑。
- 关键代码：
  - 在抽象类里有一个 ArrayList 存放观察者们。
  - 使用多播委托来实现一对多的模式，将各个观察者需要更新的状态+=到发布者的通知里
  - 在发布者类 中遍历观察者列表进行通知


-----
4、简单工厂模式

简单工厂就是一个生产对象的类，它的主要作用就是创建具体的产品类实例。

- 意图：降低客户端和具体对象的耦合，将new具体实例的任务交给一个简单工厂类
- 违反了开闭原则，在新增产品时需要修改简单工厂类
  


-----
5、工厂模式

为解决简单工厂的缺陷，将创建具体实例的任务放在了工厂的子类中，工厂只提供创建实例的接口，这样添加新产品只需要增加新的子类即可，无需修改工厂类的代码。

- 但子类都是生产的同一种类型的产品，为了解决生产系列产品的问题，引入了抽象工厂模式

-----
6、抽象工厂模式

- 抽象工厂类可以拥有多个抽象方法来生产不同类型的产品，子工厂继承抽象工厂，来进行创建具体的实例
- 但增加新产品时，违反了开闭原则，不仅需要创建新产品的抽象类和具体类，还需要在工厂中增加新的方法


-----
7、适配器模式

适配器模式（Adapter Pattern）是作为两个不兼容的接口之间的桥梁，结构型模式。

- 意图：将一个原有类的接口转换成客户希望的另外一个接口。适配器模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。
- 如何解决：继承或依赖（推荐）。
- 关键代码：
  - Adaptee:初始角色，实现了我们想要使用的功能，但是接口不匹配
  - Target:目标角色，定义了客户端期望的接口
  - Adapter:适配器角色，继承自目标角色，但内部包含一个Adaptee的对象，通过这个对象调用Adaptee的原有方法实现目标接口。
  - 可以统一调用接口




- [ ] C#notifiers
- [ ] INotify类
