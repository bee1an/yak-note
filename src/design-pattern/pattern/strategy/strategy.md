# 策略模式

[参考文章](https://refactoringguru.cn/design-patterns/strategy)

> 亦称: Strategy

策略模式是一种[行为型设计模式](../pattern.md#行为型模式)

封装一系列算法或者行为, 将每种**算法封装**到独立类中, 以使算法的对象能够相互替换

## 场景

小宇开发了一款地图, 刚开始只是提供驾车路线, 随着功能的增加, 现在需要**新增骑行路线**, 后面又会**新增步行路线**

我们发现每一次新增路线会非常头痛, 代码会越来越**臃肿**, 而且任何修改都会**影响整个**类, 违背了开闭原则

此外, 在协同开发时也会因为同时修改这一个类, 导致**代码冲突**

那就**重构!!!**

## 解决方法

策略模式建议将逻辑封装到独立类中, 这些独立的类被成为策略(Strategy: /ˈstrætədʒi/), 策略之间可以**相互替换**

我们需要一个上下文类(Context)来将**工作委派**给策略类

上下文中因保存策略的引用(类型为策略的接口), **上下文并不关心策略**, 它只关心策略的通用接口, 上下文并不指定策略, 而是允许客户端在运行时指定(提供设置策略的方法)

上下文类和策略类是**松耦合**的, 上下文完全独立与策略类, 所以, 在新增策略时, 不需要修改上下文类

上面的例子中, 使用策略模式时每次新增路线都只需要新增一个子类, 满足开闭原则

## 结构

> 引用自: https://refactoringguru.cn/design-patterns/strategy

![structure](./structure-indexed.png)

1. 上下文 （Context） 维护指向具体策略的引用， 且仅通过策略接口与该对象进行交流。

2. 策略 （Strategy） 接口是所有具体策略的通用接口， 它声明了一个上下文用于执行策略的方法。

3. 具体策略 （Concrete Strategies） 实现了上下文所用算法的各种不同变体。

4. 当上下文需要运行算法时， 它会在其已连接的策略对象上调用执行方法。 上下文不清楚其所涉及的策略类型与算法的执行方式。

5. 客户端 （Client） 会创建一个特定策略对象并将其传递给上下文。 上下文则会提供一个设置器以便客户端在运行时替换相关联的策略。

## 跟状态模式的区别

策略模式跟[状态模式](../state/state.md)很像, 都是将工作委派给其他对象

具体区别就在于状态模式子实现类清楚的知道其他状态并且可以相互转换

策略模式并不关心其他策略, 所有策略都是相对独立的

## 贴个代码

<<< @/src/design-pattern/pattern/strategy/strategy.ts
