# 迪米特法则

> demeter principle

最少知道原则是指：**一个实体应当尽量少地与其他实体之间发生相互作用，使得系统功能模块相对独立**

例如, 粉丝只需要明星的签名照, 但是如果粉丝知道明星的所有的东西, 粉丝可能会不小心使用了不该使用的东西, 所以这个时候我们需要经纪人来解除粉丝和明星的耦合关系, 或者让粉丝只知道明星签名照这个功能, 不让粉丝访问明星其他功能

## 贴个代码

<<< @/src/design-pattern/principle/demeter/demeter.ts
