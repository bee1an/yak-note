# 迭代器模式

[参考文章](https://refactoringguru.cn/design-patterns/iterator)

> 亦称: Iterator

迭代器模式是一种**行为设计模式**

在不暴露集合的底层表现形式的情况下**遍历集合**

## 场景

新年到了, 小宇想给微信好友发送祝福消息, 想根据不同的人群发送不同的祝福语, 比如朋友和同事的祝福语会不一样, 小宇想通过脚本的方式来实现发送消息

可是在获取人群的方式上出现了问题, 如果只是在 `send` 方法内部通过 `type` 判断当前成员归属从而发送不同的祝福语, 这样方法与发送信息的方法耦合了, 而且如果后续需要新增给亲人发送祝福语的话会修改`send` 方法, 不满足[开闭原则](../../principle/open-close/open-close.md)

## 解决方法

分析上面的问题, 对于一个集合的**遍历行为不确定**, 我们需要使用迭代器模式

迭代器模式的主要思想将集合的**遍历行为抽取**为一个独立的迭代器对象

迭代器通常提供返回集合元素的方法与是否迭代完成的方法, 如 `next` 和 `hasNext`, `next` 方法表示当前元素, `hasNext` 表示迭代器是否遍历完了所有元素

所有迭代器必须实现相同的接口, 这样客户端就不用依赖具体的迭代器, 客户端的遍历行为可以根据具体迭代器而改变, 满足[里氏代换原则](../../principle/liskov-substitution/liskov-substitution.md)

## 结构

> 引用自: https://refactoringguru.cn/design-patterns/iterator

![structure](./structure-indexed.png)

1. 迭代器 （Iterator） 接口声明了遍历集合所需的操作： 获取下一个元素、 获取当前位置和重新开始迭代等。

2. 具体迭代器 （Concrete Iterators） 实现遍历集合的一种特定算法。 迭代器对象必须跟踪自身遍历的进度。 这使得多个迭代器可以相互独立地遍历同一集合。

3. 集合 （Collection） 接口声明一个或多个方法来获取与集合兼容的迭代器。 请注意， 返回方法的类型必须被声明为迭代器接口， 因此具体集合可以返回各种不同种类的迭代器。

4. 具体集合 （Concrete Collections） 会在客户端请求迭代器时返回一个特定的具体迭代器类实体。 你可能会琢磨， 剩下的集合代码在什么地方呢？ 不用担心， 它也会在同一个类中。 只是这些细节对于实际模式来说并不重要， 所以我们将其省略了而已。

5. 客户端 （Client） 通过集合和迭代器的接口与两者进行交互。 这样一来客户端无需与具体类进行耦合， 允许同一客户端代码使用各种不同的集合和迭代器。客户端通常不会自行创建迭代器， 而是会从集合中获取。 但在特定情况下， 客户端可以直接创建一个迭代器 （例如当客户端需要自定义特殊迭代器时）。

## 贴个代码

<<< @/src/design-pattern/pattern/iterator/iterator.ts
