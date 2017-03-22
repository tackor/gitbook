# KVO 内部实现原理
同类问题:
1. apple 用什么方式实现对一个对象的kvo?


解答:
* KVO 是基于runtime机制实现的

* 当某个类的属性对象第一次被观察时, 系统就会在运行期动态创建该类的一个派生类, 在这个派生类中重写基类中任何被观察属性的setter方法, 派生类在被重写setter方法内实现真正的通知机制

* 如果原类为Person, 那么生成的派生类名为NSKVONotifying_Person

* 每个类对象中都有一个isa指针指向当前类, 当一个类对象的第一次被观察, 那么系统会偷偷将isa指针指向动态生成的派生类, 从而在给被监控属性赋值时指向的是派生类的setter方法

* 键值观察通知依赖于NSObject的两个方法: willChangeValueForKey: 和didChangeValueForKey; 在一个被观察的属性发生改变之前, willChangeValueForKey: 一定会被调用, 这就记录了旧值, 而当改变发生之后, didChangeValueForKey: 会被调用, 继而 observeValueForKey: ofObject: change: context: 也会被调用

*补充: KVO的这套实现集中中苹果偷偷重写了class方法, 让我们误以为还是使用的当前类, 从而达到隐藏生成的派生类

#KVC & KVO 的 keyPath 一定是属性吗?

    * 可以是成员变量
    




<br />
<br />
<br />