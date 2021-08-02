---
description: Prototype Pattern【学习难度：★★★☆☆，使用频率：★★★☆☆】
---

# 对象的克隆——原型模式

张纪中版《西游记》以出乎意料的造型和雷人的台词遭到广大观众朋友的热议，我们在此对该话题不作过多讨论。但无论是哪个版本的《西游记》，孙悟空都是其中的一号雄性主角，关于他（或它）拔毛变小猴的故事几乎人人皆知，孙悟空可以用猴毛根据自己的形象，复制（又称“克隆”或“拷贝”）出很多跟自己长得一模一样的“身外身”来。在设计模式中也存在一个类似的模式，可以通过一个原型对象克隆出多个一模一样的对象，该模式称之为原型模式。

## 1. 大同小异的工作周报

Sunny 软件公司一直使用自行开发的一套 OA \(Office Automatic，办公自动化\)系统进行日常工作办理，但在使用过程中，越来越多的人对工作周报的创建和编写模块产生了抱怨。追其原因，Sunny 软件公司的 OA 管理员发现，由于某些岗位每周工作存在重复性，工作周报内容都大同小异，如图 1 工作周报示意图。这些周报只有一些小地方存在差异，但是现行系统每周默认创建的周报都是空白报表，用户只能通过重新输入或不断复制粘贴来填写重复的周报内容，极大降低了工作效率，浪费宝贵的时间。如何快速创建相同或者相似的工作周报，成为 Sunny 公司 OA 开发人员面临的一个新问题。

![&#x56FE; 1  &#x5DE5;&#x4F5C;&#x5468;&#x62A5;&#x793A;&#x610F;&#x56FE;](../.gitbook/assets/1333464343_7157.gif)

Sunny 公司的开发人员通过对问题进行仔细分析，决定按照如下思路对工作周报模块进行重新设计和实现：

1. 除了允许用户创建新周报外，还允许用户将创建好的周报保存为模板；
2. 用户在再次创建周报时，可以创建全新的周报，还可以选择合适的模板复制生成一份相同的周报，然后对新生成的周报根据实际情况进行修改，产生新的周报。

只要按照如上两个步骤进行处理，工作周报的创建效率将得以大大提高。这个过程让我们想到平时经常进行的两个电脑基本操作：复制和粘贴，快捷键通常为 Ctrl + C 和 Ctrl + V，通过对已有对象的复制和粘贴，我们可以创建大量的相同对象。如何在一个面向对象系统中实现对象的复制和粘贴呢？不用着急，本章我们介绍的原型模式正为解决此类问题而诞生。

## 2. 原型模式概述

在使用原型模式时，我们需要首先创建一个原型对象，再通过复制这个原型对象来创建更多同类型的对象。试想，如果连孙悟空的模样都不知道，怎么拔毛变小猴子呢？原型模式的定义如下：

> 原型模式 \(Prototype Pattern\)：使用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。原型模式是一种对象创建型模式。

原型模式的工作原理很简单：将一个原型对象传给那个要发动创建的对象，这个要发动创建的对象通过请求原型对象拷贝自己来实现创建过程。由于在软件系统中我们经常会遇到需要创建多个相同或者相似对象的情况，因此原型模式在真实开发中的使用频率还是非常高的。原型模式是一种“另类”的创建型模式，创建克隆对象的工厂就是原型类自身，工厂方法由克隆方法来实现。

需要注意的是通过克隆方法所创建的对象是全新的对象，它们在内存中拥有新的地址，通常对克隆所产生的对象进行修改对原型对象不会造成任何影响，每一个克隆对象都是相互独立的。通过不同的方式修改可以得到一系列相似但不完全相同的对象。

原型模式的结构如图 2 所示：

![&#x56FE; 2  &#x539F;&#x578B;&#x6A21;&#x5F0F;&#x7ED3;&#x6784;&#x56FE;](../.gitbook/assets/1333464346_2107.gif)

在原型模式结构图中包含如下几个角色：

* `Prototype`（抽象原型类）：它是声明克隆方法的接口，是所有具体原型类的公共父类，可以是抽象类也可以是接口，甚至还可以是具体实现类。
* `ConcretePrototype`（具体原型类）：它实现在抽象原型类中声明的克隆方法，在克隆方法中返回自己的一个克隆对象。
* `Client`（客户类）：让一个原型对象克隆自身从而创建一个新的对象，在客户类中只需要直接实例化或通过工厂方法等方式创建一个原型对象，再通过调用该对象的克隆方法即可得到多个相同的对象。由于客户类针对抽象原型类 `Prototype` 编程，因此用户可以根据需要选择具体原型类，系统具有较好的可扩展性，增加或更换具体原型类都很方便。

原型模式的核心在于如何实现克隆方法，下面将介绍两种在 Java 语言中常用的克隆实现方法：

### **1. 通用实现方法**

通用的克隆实现方法是在具体原型类的克隆方法中实例化一个与自身类型相同的对象并将其返回，并将相关的参数传入新创建的对象中，保证它们的成员属性相同。示意代码如下所示：

```text
class ConcretePrototype implements Prototype
{
    private String attr; // 成员属性
    public void setAttr(String attr)
    {
        this.attr = attr;
    }
    
    public String getAttr()
    {
        return this.attr;
    }
    
    public Prototype clone() // 克隆方法
    {
        Prototype  prototype = new ConcretePrototype(); // 创建新对象
        prototype.setAttr(this.attr);
        return prototype;
    }
}
```

**🤔**思考**：**能否将上述代码中的clone\(\)方法写成：`public Prototype clone() { return this; }`？给出你的理由。

在客户类中我们只需要创建一个 `ConcretePrototype` 对象作为原型对象，然后调用其clone\(\)方法即可得到对应的克隆对象，如下代码所示：

```text
Prototype obj1  = new ConcretePrototype();
obj1.setAttr("Sunny");
Prototype obj2  = obj1.clone();
```

这种方法可作为原型模式的通用实现，它与编程语言特性无关，任何面向对象语言都可以使用这种形式来实现对原型的克隆。

###  2. Java语言提供的 `clone()` 方法

学过Java语言的人都知道，所有的 Java 类都继承自 `java.lang.Object`。事实上，`Object` 类提供一个 `clone()` 方法，可以将一个 Java 对象复制一份。因此在 Java 中可以直接使用 `Object` 提供的 `clone()` 方法来实现对象的克隆，Java 语言中的原型模式实现很简单。

需要注意的是能够实现克隆的 Java 类必须实现一个标识接口 `Cloneable`，表示这个 Java 类支持被复制。如果一个类没有实现这个接口但是调用了 `clone()` 方法，Java 编译器将抛出一个 CloneNotSupportedException 异常。如下代码所示：

```text
class ConcretePrototype implements Cloneable
{
    ……
    public Prototype clone()
    {
        Object object = null;
        try {
            object = super.clone();
        } catch (CloneNotSupportedException exception) {
            System.err.println("Not support cloneable");
        }
        return (Prototype )object;
    }
    ……
}
```

在客户端创建原型对象和克隆对象也很简单，如下代码所示：

```text
Prototype obj1  = new ConcretePrototype();
Prototype obj2  = obj1.clone();
```

一般而言，Java 语言中的 `clone()` 方法满足：

1. 对任何对象 `x`，都有 `x.clone() != x`，即克隆对象与原型对象不是同一个对象；
2. 对任何对象 `x`，都有 `x.clone().getClass() == x.getClass()`，即克隆对象与原型对象的类型一样；
3. 如果对象 `x` 的 `equals()` 方法定义恰当，那么 `x.clone().equals(x)` 应该成立。

为了获取对象的一份拷贝，我们可以直接利用 `Object` 类的 `clone()` 方法，具体步骤如下：

1. 在派生类中覆盖基类的 `clone()` 方法，并声明为 public；
2. 在派生类的 `clone()` 方法中，调用 `super.clone()`；
3. 派生类需实现 `Cloneable` 接口。

此时，`Object` 类相当于抽象原型类，所有实现了 `Cloneable` 接口的类相当于具体原型类。

## 3. 完整解决方案

Sunny 公司开发人员决定使用原型模式来实现工作周报的快速创建，快速创建工作周报结构图如图 3 所示：

![&#x56FE; 3  &#x5FEB;&#x901F;&#x521B;&#x5EFA;&#x5DE5;&#x4F5C;&#x5468;&#x62A5;&#x7ED3;&#x6784;&#x56FE;](../.gitbook/assets/1333464523_7039.gif)

在图 3 中，`WeeklyLog` 充当具体原型类，`Object` 类充当抽象原型类，`clone()` 方法为原型方法。`WeeklyLog` 类的代码如下所示：

```text
// 工作周报WeeklyLog：具体原型类，考虑到代码的可读性和易理解性，只列出部分与模式相关的核心代码
class WeeklyLog implements Cloneable
{
    private String name;
    private String date;
    private String content;
    public void setName(String name) {
        this.name  = name;
    }
    public void setDate(String date) {
        this.date  = date;
    }
    public void setContent(String content) {
        this.content  = content;
    }
    public String getName() {
        return  (this.name);
    }
    public String getDate() {
        return  (this.date);
    }
    public String getContent() {
        return  (this.content);
    }
    
    // 克隆方法clone()，此处使用Java语言提供的克隆机制
    public WeeklyLog clone()
    {
        Object obj = null;
        try
        {
            obj = super.clone();
            return (WeeklyLog)obj;     
        }
        catch(CloneNotSupportedException e)
        {
            System.out.println("不支持复制！");
            return null;
        }
    }
}
```

编写如下客户端测试代码：

```text
class Client
{
    public static void main(String args[])
    {
        WeeklyLog log_previous = new WeeklyLog();  // 创建原型对象
        log_previous.setName("张无忌");
        log_previous.setDate("第12周");
        log_previous.setContent("这周工作很忙，每天加班！");
        System.out.println("****周报****");
        System.out.println("周次：" + log_previous.getDate());
        System.out.println("姓名：" + log_previous.getName());
        System.out.println("内容：" + log_previous.getContent());
        System.out.println("--------------------------------");
        WeeklyLog log_new;
        log_new = log_previous.clone(); // 调用克隆方法创建克隆对象
        log_new.setDate("第13周");
        System.out.println("****周报****");
        System.out.println("周次：" + log_new.getDate());
        System.out.println("姓名：" + log_new.getName());
        System.out.println("内容：" + log_new.getContent());
    }
}
```

编译并运行程序，输出结果如下：

```text
****周报****
周次：第12周
姓名：张无忌
内容：这周工作很忙，每天加班！
--------------------------------
****周报****
周次：第13周
姓名：张无忌
内容：这周工作很忙，每天加班！
```

通过已创建的工作周报可以快速创建新的周报，然后再根据需要修改周报，无须再从头开始创建。原型模式为工作流系统中任务单的快速生成提供了一种解决方案。

🤔思考：如果在 `Client` 类的 main\(\) 函数中增加如下几条语句：

```text
System.out.println(log_previous == log_new);
System.out.println(log_previous.getDate() == log_new.getDate());
System.out.println(log_previous.getName() == log_new.getName());
System.out.println(log_previous.getContent() == log_new.getContent());
```

预测这些语句的输出结果。

## 4. 带附件的周报

通过引入原型模式，Sunny 软件公司 OA 系统支持工作周报的快速克隆，极大提高了工作周报的编写效率，受到员工的一致好评。但有员工又发现一个问题，有些工作周报带有附件，例如经理助理“小龙女”的周报通常附有本周项目进展报告汇总表、本周客户反馈信息汇总表等，如果使用上述原型模式来复制周报，周报虽然可以复制，但是周报的附件并不能复制，这是由于什么原因导致的呢？如何才能实现周报和附件的同时复制呢？我们在本节将讨论如何解决这些问题。

在回答这些问题之前，先介绍一下两种不同的克隆方法，浅克隆（ShallowClone）和深克隆（DeepClone）。在 Java 语言中，数据类型分为值类型（基本数据类型）和引用类型，值类型包括 int、double、byte、boolean、char 等简单数据类型，引用类型包括类、接口、数组等复杂类型。浅克隆和深克隆的主要区别在于是否支持引用类型的成员变量的复制，下面将对两者进行详细介绍。

### 1. 浅克隆

在浅克隆中，如果原型对象的成员变量是值类型，将复制一份给克隆对象；如果原型对象的成员变量是引用类型，则将引用对象的地址复制一份给克隆对象，也就是说原型对象和克隆对象的成员变量指向相同的内存地址。简单来说，在浅克隆中，当对象被复制时只复制它本身和其中包含的值类型的成员变量，而引用类型的成员对象并没有复制，如图 4 所示：

![&#x56FE; 4  &#x6D45;&#x514B;&#x9686;&#x793A;&#x610F;&#x56FE;](../.gitbook/assets/1333464896_9252.gif)

在 Java 语言中，通过覆盖 Object 类的 clone\(\) 方法可以实现浅克隆。为了让大家更好地理解浅克隆和深克隆的区别，我们首先使用浅克隆来实现工作周报和附件类的复制，其结构如图 5 所示：

![&#x56FE; 5  &#x5E26;&#x9644;&#x4EF6;&#x7684;&#x5468;&#x62A5;&#x7ED3;&#x6784;&#x56FE;&#xFF08;&#x6D45;&#x514B;&#x9686;&#xFF09;](../.gitbook/assets/1333464920_5154.gif)

附件类 `Attachment` 代码如下：

```text
// 附件类
class Attachment
{
    private String name; // 附件名
    public void setName(String name)
    {
        this.name  = name;
    }
    public String getName()
    {
        return  this.name;
    }
     public void download()
     {
         System.out.println("下载附件，文件名为" + name);
     }
}
```

修改工作周报类 `WeeklyLog`，修改后的代码如下：

```text
// 工作周报 WeeklyLog
class WeeklyLog implements Cloneable
{
    // 为了简化设计和实现，假设一份工作周报中只有一个附件对象，实际情况中可以包含多个附件，可以通过List等集合对象来实现
    private Attachment attachment;
    private String name;
    private String date;
    private String content;
    public void setAttachment(Attachment  attachment) {
        this.attachment = attachment;
    }
    public void setName(String name) {
        this.name  = name;
    }
    public void setDate(String date) {
        this.date  = date;
    }
    public void setContent(String content) {
        this.content  = content;
    }
    public Attachment  getAttachment(){
        return (this.attachment);
    }
    public String getName() {
        return (this.name);
    }
    public String getDate() {
        return (this.date);
    }
    public String getContent() {
        return  (this.content);
    }
    // 使用 clone() 方法实现浅克隆
    public WeeklyLog clone()
    {
        Object obj = null;
        try
        {
            obj = super.clone();
            return (WeeklyLog)obj;
        }
        catch(CloneNotSupportedException e)
        {
            System.out.println("不支持复制！");
            return null;
        }
    }
}
```

客户端代码如下所示：

```text
class Client
{
    public  static void main(String args[])
    {
        WeeklyLog  log_previous, log_new;
        log_previous  = new WeeklyLog(); // 创建原型对象
        Attachment  attachment = new Attachment(); // 创建附件对象
        log_previous.setAttachment(attachment);  // 将附件添加到周报中
        log_new  = log_previous.clone(); // 调用克隆方法创建克隆对象
        //比较周报
        System.out.println("周报是否相同？ " + (log_previous ==  log_new));
        //比较附件
        System.out.println("附件是否相同？ " +  (log_previous.getAttachment() == log_new.getAttachment()));
    }
}
```

编译并运行程序，输出结果如下：

```text
周报是否相同？ false
附件是否相同？ true
```

由于使用的是浅克隆技术，因此工作周报对象复制成功，通过“==”比较原型对象和克隆对象的内存地址时输出 false；但是比较附件对象的内存地址时输出 true，说明它们在内存中是同一个对象。

### 2. 深克隆

在深克隆中，无论原型对象的成员变量是值类型还是引用类型，都将复制一份给克隆对象，深克隆将原型对象的所有引用对象也复制一份给克隆对象。简单来说，在深克隆中，除了对象本身被复制外，对象所包含的所有成员变量也将复制，如图 6 所示：

![&#x56FE; 6  &#x6DF1;&#x514B;&#x9686;&#x793A;&#x610F;&#x56FE;](../.gitbook/assets/1333464924_1911.gif)

在 Java 语言中，如果需要实现深克隆，可以通过序列化（Serialization）等方式来实现。序列化就是将对象写到流的过程，写到流中的对象是原有对象的一个拷贝，而原对象仍然存在于内存中。通过序列化实现的拷贝不仅可以复制对象本身，而且可以复制其引用的成员对象，因此通过序列化将对象写到一个流中，再从流里将其读出来，可以实现深克隆。需要注意的是能够实现序列化的对象其类必须实现 `Serializable` 接口，否则无法实现序列化操作。下面我们使用深克隆技术来实现工作周报和附件对象的复制，由于要将附件对象和工作周报对象都写入流中，因此两个类均需要实现 `Serializable` 接口，其结构如图 7 所示：

![&#x56FE; 7  &#x5E26;&#x9644;&#x4EF6;&#x7684;&#x5468;&#x62A5;&#x7ED3;&#x6784;&#x56FE;&#xFF08;&#x6DF1;&#x514B;&#x9686;&#xFF09;](../.gitbook/assets/1333464931_1578.gif)

修改后的附件类 `Attachment` 代码如下：

```text
import java.io.*;
// 附件类
class Attachment implements Serializable
{
    private String name; //附件名
    public void setName(String name)
    {
        this.name  = name;
    }
    public String getName()
    {
        return  this.name;
    }
    public void download()
    {
        System.out.println("下载附件，文件名为" + name);
    }
}
```

工作周报类 `WeeklyLog` 不再使用 Java 自带的克隆机制，而是通过序列化来从头实现对象的深克隆，我们需要重新编写 `clone()` 方法，修改后的代码如下：

```text
import java.io.*;
// 工作周报类
class WeeklyLog implements Serializable
{
    private Attachment attachment;
    private String name;
    private String date;
    private String content;
    public void setAttachment(Attachment attachment) {
        this.attachment  = attachment;
    }
    public void setName(String name) {
        this.name  = name;
    }
    public void setDate(String date) {
        this.date  = date;
    }
    public void setContent(String content) {
        this.content  = content;
    }
    public Attachment getAttachment(){
        return  (this.attachment);
    }
    public String getName() {
        return  (this.name);
    }
    public  String getDate() {
        return  (this.date);
    }
    public  String getContent() {
        return  (this.content);
    }
    // 使用序列化技术实现深克隆
    public WeeklyLog deepClone() throws IOException, ClassNotFoundException, OptionalDataException
    {
        // 将对象写入流中
        ByteArrayOutputStream bao=new ByteArrayOutputStream();
        ObjectOutputStream oos=new ObjectOutputStream(bao);
        oos.writeObject(this);
        // 将对象从流中取出
        ByteArrayInputStream bis=new ByteArrayInputStream(bao.toByteArray());
        ObjectInputStream ois=new ObjectInputStream(bis);
        return (WeeklyLog)ois.readObject();
    }
}
```

客户端代码如下所示：

```text
class Client
{
    public  static void main(String args[])
    {
        WeeklyLog log_previous, log_new = null;
        log_previous = new WeeklyLog(); // 创建原型对象
        Attachment attachment = new Attachment(); // 创建附件对象
        log_previous.setAttachment(attachment);  // 将附件添加到周报中
        try
        {
            log_new =  log_previous.deepClone(); // 调用深克隆方法创建克隆对象                  
        }
        catch(Exception e)
        {
            System.err.println("克隆失败！");
        }
        // 比较周报
        System.out.println("周报是否相同？ " + (log_previous == log_new));
        // 比较附件
        System.out.println("附件是否相同？ " + (log_previous.getAttachment() == log_new.getAttachment()));
    }
}
```

编译并运行程序，输出结果如下：

```text
周报是否相同？  false
附件是否相同？  false
```

从输出结果可以看出，由于使用了深克隆技术，附件对象也得以复制，因此用“==”比较原型对象的附件和克隆对象的附件时输出结果均为 false。深克隆技术实现了原型对象和克隆对象的完全独立，对任意克隆对象的修改都不会给其他对象产生影响，是一种更为理想的克隆实现方式。

🤔扩展：Java语言提供的 `Cloneable` 接口和 `Serializable` 接口的代码非常简单，它们都是空接口，这种空接口也称为标识接口，标识接口中没有任何方法的定义，其作用是告诉JRE这些接口的实现类是否具有某个功能，如是否支持克隆、是否支持序列化等。

## 5. 原型管理器的引入和实现

原型管理器（Prototype Manager）是将多个原型对象存储在一个集合中供客户端使用，它是一个专门负责克隆对象的工厂，其中定义了一个集合用于存储原型对象，如果需要某个原型对象的一个克隆，可以通过复制集合中对应的原型对象来获得。在原型管理器中针对抽象原型类进行编程，以便扩展。其结构如图 8 所示：

![&#x56FE; 8  &#x5E26;&#x539F;&#x578B;&#x7BA1;&#x7406;&#x5668;&#x7684;&#x539F;&#x578B;&#x6A21;&#x5F0F;](../.gitbook/assets/1333465608_5871.gif)

下面通过模拟一个简单的公文管理器来介绍原型管理器的设计与实现：

Sunny 软件公司在日常办公中有许多公文需要创建、递交和审批，例如《可行性分析报告》、《立项建议书》、《软件需求规格说明书》、《项目进展报告》等，为了提高工作效率，在 OA 系统中为各类公文均创建了模板，用户可以通过这些模板快速创建新的公文，这些公文模板需要统一进行管理，系统根据用户请求的不同生成不同的新公文。

我们使用带原型管理器的原型模式实现公文管理器的设计，其结构如图 9 所示：

![&#x56FE; 9  &#x516C;&#x6587;&#x7BA1;&#x7406;&#x5668;&#x7ED3;&#x6784;&#x56FE;](../.gitbook/assets/1333465614_7325.gif)

以下是实现该功能的一些核心代码，考虑到代码的可读性，我们对所有的类都进行了简化：

```text
import java.util.*;
// 抽象公文接口，也可定义为抽象类，提供 clone() 方法的实现，将业务方法声明为抽象方法
interface OfficialDocument extends  Cloneable
{
    public OfficialDocument clone();
    public void display();
}
// 可行性分析报告（Feasibility Analysis Report）类
class FAR implements OfficialDocument
{
    public OfficialDocument clone()
      {
        OfficialDocument far = null;
        try
        {
            far  = (OfficialDocument)super.clone();
        }
        catch(CloneNotSupportedException  e)
        {
            System.out.println("不支持复制！");
        }
        return  far;
    }
    public  void display()
    {
        System.out.println("《可行性分析报告》");
    }
}
// 软件需求规格说明书(Software Requirements Specification)类
class SRS implements OfficialDocument
{
    public OfficialDocument clone()
    {
        OfficialDocument  srs = null;
        try
        {
            srs  = (OfficialDocument)super.clone();
        }
        catch(CloneNotSupportedException  e)
        { 
            System.out.println("不支持复制！");
        }
        return  srs;
    }
    public  void display()
    {
        System.out.println("《软件需求规格说明书》");
    }
}
// 原型管理器（使用饿汉式单例实现）
class PrototypeManager
{
    // 定义一个 Hashtable，用于存储原型对象
    private Hashtable ht=new Hashtable();
    private static PrototypeManager pm =  new PrototypeManager();
    // 为 Hashtable 增加公文对象   
    private PrototypeManager()
    {
        ht.put("far",new  FAR());
        ht.put("srs",new  SRS());         
    }
     // 增加新的公文对象
    public void addOfficialDocument(String  key,OfficialDocument doc)
    {
        ht.put(key,doc);
    }
    // 通过浅克隆获取新的公文对象
    public OfficialDocument  getOfficialDocument(String key)
    {
        return ((OfficialDocument)ht.get(key)).clone();
    }
    public static PrototypeManager  getPrototypeManager()
    {
        return pm;
    }
}
```

客户端代码如下所示：

```text
class Client
{
    public static void main(String args[])
    {
        // 获取原型管理器对象
        PrototypeManager pm = PrototypeManager.getPrototypeManager();  
        OfficialDocument doc1,doc2,doc3,doc4;
        doc1 = pm.getOfficialDocument("far");
        doc1.display();
        doc2 = pm.getOfficialDocument("far");
        doc2.display();
        System.out.println(doc1 == doc2);
        doc3 = pm.getOfficialDocument("srs");
        doc3.display();
        doc4 = pm.getOfficialDocument("srs");
        doc4.display();
        System.out.println(doc3 == doc4);
    }
}
```

编译并运行程序，输出结果如下：

```text
《可行性分析报告》
《可行性分析报告》
false
《软件需求规格说明书》
《软件需求规格说明书》
false
```

在 `PrototypeManager` 中定义了一个 `Hashtable` 类型的集合对象，使用“键值对”来存储原型对象，客户端可以通过 Key（如“far”或“srs”）来获取对应原型对象的克隆对象。 `PrototypeManager` 类提供了类似工厂方法的 `getOfficialDocument()` 方法用于返回一个克隆对象。在本实例代码中，我们将 `PrototypeManager` 设计为单例类，使用饿汉式单例实现，确保系统中有且仅有一个 `PrototypeManager` 对象，有利于节省系统资源，并可以更好地对原型管理器对象进行控制。

🤔思考：如果需要增加一种新类型的公文，如《项目进展报告》（Project Progress Report, PPR），公文管理器系统源代码如何修改，动手实践你的修改方案。

## 6. 原型模式总结

原型模式作为一种快速创建大量相同或相似对象的方式，在软件开发中应用较为广泛，很多软件提供的复制（Ctrl + C）和粘贴（Ctrl + V）操作就是原型模式的典型应用，下面对该模式的使用效果和适用情况进行简单的总结。

###  **1. 主要优点**

原型模式的主要优点如下：

1. 当创建新的对象实例较为复杂时，使用原型模式可以简化对象的创建过程，通过复制一个已有实例可以提高新实例的创建效率。
2. 扩展性较好，由于在原型模式中提供了抽象原型类，在客户端可以针对抽象原型类进行编程，而将具体原型类写在配置文件中，增加或减少产品类对原有系统都没有任何影响。
3. 原型模式提供了简化的创建结构，工厂方法模式常常需要有一个与产品类等级结构相同的工厂等级结构，而原型模式就不需要这样，原型模式中产品的复制是通过封装在原型类中的克隆方法实现的，无须专门的工厂类来创建产品。
4. 可以使用深克隆的方式保存对象的状态，使用原型模式将对象复制一份并将其状态保存起来，以便在需要的时候使用（如恢复到某一历史状态），可辅助实现撤销操作。

### **2. 主要缺点**

原型模式的主要缺点如下：

1. 需要为每一个类配备一个克隆方法，而且该克隆方法位于一个类的内部，当对已有的类进行改造时，需要修改源代码，违背了“开闭原则”。
2. 在实现深克隆时需要编写较为复杂的代码，而且当对象之间存在多重的嵌套引用时，为了实现深克隆，每一层对象对应的类都必须支持深克隆，实现起来可能会比较麻烦。

### **3. 适用场景**

在以下情况下可以考虑使用原型模式：

1. 创建新对象成本较大（如初始化需要占用较长的时间，占用太多的CPU资源或网络资源），新的对象可以通过原型模式对已有对象进行复制来获得，如果是相似对象，则可以对其成员变量稍作修改。
2. 如果系统要保存对象的状态，而对象的状态变化很小，或者对象本身占用内存较少时，可以使用原型模式配合备忘录模式来实现。
3. 需要避免使用分层次的工厂类来创建分层次的对象，并且类的实例对象只有一个或很少的几个组合状态，通过复制原型对象得到新实例可能比使用构造函数创建一个新实例更加方便。

🤔练习：设计并实现一个客户类 `Customer`，其中包含一个名为客户地址的成员变量，客户地址的类型为 Address，用浅克隆和深克隆分别实现 `Customer` 对象的复制并比较这两种克隆方式的异同。

【作者：刘伟 [http://blog.csdn.net/lovelion](http://blog.csdn.net/lovelion)】



