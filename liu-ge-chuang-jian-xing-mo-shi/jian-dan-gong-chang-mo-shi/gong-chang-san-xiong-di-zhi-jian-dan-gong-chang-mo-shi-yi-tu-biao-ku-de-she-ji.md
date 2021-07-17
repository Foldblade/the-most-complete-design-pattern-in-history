# 工厂三兄弟之简单工厂模式（一）：图表库的设计

Sunny 软件公司欲基于 Java 语言开发一套图表库，该图表库可以为应用系统提供各种不同外观的图表，例如柱状图、饼状图、折线图等。Sunny 软件公司图表库设计人员希望为应用系统开发人员提供一套灵活易用的图表库，而且可以较为方便地对图表库进行扩展，以便能够在将来增加一些新类型的图表。

Sunny 软件公司图表库设计人员提出了一个初始设计方案，将所有图表的实现代码封装在一个 `Chart` 类中，其框架代码如下所示：

```text
class Chart {
	private String type; //图表类型
	
	public Chart(Object[][] data, String type) {
		this.type = type;
		if (type.equalsIgnoreCase("histogram")) {
			//初始化柱状图
		}
		else if (type.equalsIgnoreCase("pie")) {
			//初始化饼状图
		}
		else if (type.equalsIgnoreCase("line")) {
			//初始化折线图
		}
	}
 
	public void display() {
		if (this.type.equalsIgnoreCase("histogram")) {
			//显示柱状图
		}
		else if (this.type.equalsIgnoreCase("pie")) {
			//显示饼状图
		}
		else if (this.type.equalsIgnoreCase("line")) {
			//显示折线图
		}	
	}
}
```

客户端代码通过调用 `Chart` 类的构造函数来创建图表对象，根据参数 `type` 的不同可以得到不同类型的图表，然后再调用 `display()` 方法来显示相应的图表。

不难看出，`Chart` 类是一个“巨大的”类，在该类的设计中存在如下几个问题：

1. 在 `Chart` 类中包含很多 “if…else…” 代码块，整个类的代码相当冗长，代码越长，阅读难度、维护难度和测试难度也越大；而且大量条件语句的存在还将影响系统的性能，程序在执行过程中需要做大量的条件判断。
2. `Chart` 类的职责过重，它负责初始化和显示所有的图表对象，将各种图表对象的初始化代码和显示代码集中在一个类中实现，违反了“单一职责原则”，不利于类的重用和维护；而且将大量的对象初始化代码都写在构造函数中将导致构造函数非常庞大，对象在创建时需要进行条件判断，降低了对象创建的效率。
3. 当需要增加新类型的图表时，必须修改 `Chart` 类的源代码，违反了“开闭原则”。
4. 客户端只能通过 `new` 关键字来直接创建 `Chart` 对象，`Chart` 类与客户端类耦合度较高，对象的创建和使用无法分离。
5. 客户端在创建 `Chart` 对象之前可能还需要进行大量初始化设置，例如设置柱状图的颜色、高度等，如果在 `Chart` 类的构造函数中没有提供一个默认设置，那就只能由客户端来完成初始设置，这些代码在每次创建 `Chart` 对象时都会出现，导致代码的重复。

面对一个如此巨大、职责如此重，且与客户端代码耦合度非常高的类，我们应该怎么办？本章将要介绍的简单工厂模式**将在一定程度上解决上述问题**。

为什么要引入工厂类，大家可参见：[创建对象与使用对象——谈谈工厂的作用](http://blog.csdn.net/lovelion/article/details/7523392)。

【作者：刘伟 [http://blog.csdn.net/lovelion](http://blog.csdn.net/lovelion)】

