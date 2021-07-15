# 设计模式是什么

俗话说：站在别人的肩膀上，我们会看得更远。设计模式的出现可以让我们站在前人的肩膀上，通过一些成熟的设计方案来指导新项目的开发和设计，以便于我们开发出具有更好的灵活性和可扩展性，也更易于复用的软件系统。

设计模式的一般定义如下：

> 设计模式 \(Design Pattern\) 是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结，使用设计模式是为了可重用代码、让代码更容易被他人理解并且保证代码可靠性。

狭义的设计模式是指 GoF 在《设计模式：可复用面向对象软件的基础》一书中所介绍的 23 种经典设计模式，不过设计模式并不仅仅只有这 23 种，随着软件开发技术的发展，越来越多的新模式不断诞生并得以应用。

设计模式一般包含模式名称、问题、目的、解决方案、效果等组成要素，其中关键要素是模式名称、问题、解决方案和效果。

* 模式名称 \(Pattern Name\) 通过一两个词来描述模式的问题、解决方案和效果，以便更好地理解模式并方便开发人员之间的交流，绝大多数模式都是根据其功能或模式结构来命名的（GoF 设计模式中没有一个模式用人名命名，🙂）
* 问题 \(Problem\) 描述了应该在何时使用模式，它包含了设计中存在的问题以及问题存在的原因
* 解决方案 \(Solution\) 描述了一个设计模式的组成成分，以及这些组成成分之间的相互关系，各自的职责和协作方式，通常解决方案通过 UML 类图和核心代码来进行描述
* 效果 \(Consequences\) 描述了模式的优缺点以及在使用模式时应权衡的问题。

虽然GoF设计模式只有23个，但是它们各具特色，每个模式都为某一个可重复的设计问题提供了一套解决方案。根据它们的用途，设计模式可分为创建型 \(Creational\)，结构型 \(Structural\) 和行为型 \(Behavioral\) 三种，其中**创建型模式主要用于描述如何创建对象，结构型模式主要用于描述如何实现类或对象的组合，行为型模式主要用于描述类或对象怎样交互以及怎样分配职责**，在 GoF 23 种设计模式中包含 5 种创建型设计模式、 7 种结构型设计模式和 11 种行为型设计模式。此外，根据某个模式主要是用于处理类之间的关系还是对象之间的关系，设计模式还可以分为类模式和对象模式。我们经常将两种分类方式结合使用，如单例模式是对象创建型模式，模板方法模式是类行为型模式。

值得一提的是，有一个设计模式虽然不属于 GoF 23 种设计模式，但一般在介绍设计模式时都会对它进行说明，它就是简单工厂模式，也许是太“简单”了， GoF 并没有把它写到那本经典著作中，不过现在大部分的设计模式书籍都会对它进行专门的介绍。

表 1 列出将要介绍的 24 种设计模式，其中**模式的学习难度**是我个人在多年模式使用和推广过程中的经验总结，仅作参考，**模式的使用频率**来自著名的模式推广和教育网站——http://www.dofactory.net。

表1  常用设计模式一览表



| 类型 | 模式名称 | 学习难度 | 使用频率 |
| :--- | :--- | :--- | :--- |
| 创建型模式Creational Pattern | 单例模式Singleton Pattern | ★☆☆☆☆ | ★★★★☆ |
|  | 简单工厂模式Simple Factory Pattern | ★★☆☆☆ | ★★★☆☆ |
|  | 工厂方法模式Factory Method Pattern | ★★☆☆☆ | ★★★★★ |
|  | 抽象工厂模式Abstract Factory Pattern | ★★★★☆ | ★★★★★ |
|  | 原型模式Prototype Pattern | ★★★☆☆ | ★★★☆☆ |
|  | 建造者模式Builder Pattern | ★★★★☆ | ★★☆☆☆ |
| 结构型模式Structural Pattern | 适配器模式Adapter Pattern | ★★☆☆☆ | ★★★★☆ |
|  | 桥接模式Bridge Pattern | ★★★☆☆ | ★★★☆☆ |
|  | 组合模式Composite Pattern | ★★★☆☆ | ★★★★☆ |
|  | 装饰模式Decorator Pattern | ★★★☆☆ | ★★★☆☆ |
|  | 外观模式Façade Pattern | ★☆☆☆☆ | ★★★★★ |
|  | 享元模式Flyweight Pattern | ★★★★☆ | ★☆☆☆☆ |
|  | 代理模式Proxy Pattern | ★★★☆☆ | ★★★★☆ |
| 行为型模式Behavioral Pattern | 职责链模式Chain of Responsibility Pattern | ★★★☆☆ | ★★☆☆☆ |
|  | 命令模式Command Pattern | ★★★☆☆ | ★★★★☆ |
|  | 解释器模式Interpreter Pattern | ★★★★★ | ★☆☆☆☆ |
|  | 迭代器模式Iterator Pattern | ★★★☆☆ | ★★★★★ |
|  | 中介者模式Mediator Pattern | ★★★☆☆ | ★★☆☆☆ |
|  | 备忘录模式Memento Pattern | ★★☆☆☆ | ★★☆☆☆ |
|  | 观察者模式Observer Pattern | ★★★☆☆ | ★★★★★ |
|  | 状态模式State Pattern | ★★★☆☆ | ★★★☆☆ |
|  | 策略模式Strategy Pattern | ★☆☆☆☆ | ★★★★☆ |
|  | 模板方法模式Template Method Pattern | ★★☆☆☆ | ★★★☆☆ |
|  | 访问者模式Visitor Pattern | ★★★★☆ | ★☆☆☆☆ |

【作者：刘伟 [http://blog.csdn.net/lovelion](http://blog.csdn.net/lovelion)】
