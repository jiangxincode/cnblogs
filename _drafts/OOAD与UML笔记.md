UML基础介绍

## 1.UML的定义

统一建模语言（UML）是一种图形化的语言，它可以帮助我们在OOAD过程中标识元素、构建模块、分析过程并可通过文档说明系统中的重要细节

## 2.OOAD

OOAD是根据OO的方法学，对软件系统进行分析和设计的过程

* OOA 分析阶段
* OOD 设计阶段

## 3.面向对象

面向对象（ Object-Orientation ，简称OO）是一种系统建模技术

面向对象编程（ Object-Orientation Programming，简称OOP）是按照OO的方法学来开发程序的过程通过分析系统内对象的交互来描述或建模一个系统交互的对象最终以类的形式组织

OO的方法由三部分组成

* 过程
* 标识
* 规则

## 4.OOP的主要特征

* 抽象(abstract)
* 封装(encapsulation)
* 继承(inheritance)
* 多态(polymorphism)
* 关联(association)
* 聚合(aggregation)
* 组合(composition)
* 内聚与耦合(cohesion & coupling)

## 域对象之间的关系

### 1.关联(Association)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_13038961871GI6.gif)

### 2.依赖(Dependency)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896187m9u8.gif)

### 3.聚集(Aggregation)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896188OeHE.gif)

### 4.一般化(Generalization)——泛化

一般化指的是类之间的继承关系。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_13038961884Q39.gif)

### 5.内聚与藕合

内聚：度量一个类独立完成某项工作的能力
耦合：度量系统内或系统之间依赖关系的复杂度
设计原则：增加内聚，减少耦合

## UML图的分类

### 1.用例图（Use Case Diagram）

用例图

展示系统的核心功能及与其交互的用户

用户被称之为"活动者"（Actor）

用例使用椭圆表示

为简化建模过程，用例图可标注优先级

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896189WIbu.gif)

### 2.类图（Class Diagram）

表现类的特征

类图描述了多个类、接口的特征，以及对象之间的协作与交互

由一个或多个矩形区域构成，内容包括：

—— 类型（类名）

—— 属性（可选）

—— 操作（可选）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896189Nw8g.gif)

### 3.对象图（object Diagram）

表现对象的特征

对象图展现了多个对象的特征及对象之间的交互

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_13038961897aaN.gif)

### 4.组件图（Component Diagram）

表现软件组件之间的关系

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_13038961893YnM.gif)

### 5.部署图（Deloyment Diagram）

表现用于部署软件应用的物理设备信息

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896190cK9Y.gif)

### 6.时序图（Sequence Diagram）

捕捉一段时间范围内多个对象之间的交互信息

强调消息交互的时间顺序

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896190c7c5.gif)

图1

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_130389619107Px.gif)

图2

### 7.协作图 （Collaboration Diagram）

表现一定范围内对象之间协作的信息

强调参与信息交流的对象之间的组织结构

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896191IKjP.gif)

### 8.状态转换图（Statechart Diagram）

强调一个对象在不同事件触发时，其内部状态的转变过程

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896194Uoyg.gif)

### 9.活动图（Activity Diagram）

描述活动的流程

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_13038961950a8n.gif)

### 10.包（package）

引用一组相关实体

通常可用于划分类的命名空间

包可用于

* 命名(Naming)
* 成员可见度(Member visibility)
* 导入(Importing)
* 继承(Extending)
* 泛化(Generalization)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896195l3Je.gif)

## 几种常见模式

### 1.观察者模式（Observer）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_13038961957Uff.gif)

### 2.组合模式（Composite）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896196T7vc.gif)

### 3.装饰模式（Decorator）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896197N65O.gif)

### 4.适配器模式（adapter）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896197CXZN.gif)

### 5.代理模式（peoxy）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/0_1303896198eITI.gif)