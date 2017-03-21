# isMemberOfClass 和 isKindOfClass 联系与区别

* 联系：两者都能检测一个对象是否是某个类的成员

* 区别：`isKindOfClass` 不仅用来确定一个对象是否是一个类的成员,也可以用来确定一个对象是否派生自该类的类的成员 ,而`isMemberOfClass` 只能做到第一点。

举例：

如 ClassA 派生自 NSObject类 ,
```
ClassA *a = [ClassA alloc] init];

// 可以检查出 a 是否是 NSObject派生类 的成员,但 isMemberOfClass 做不到。
[a isKindOfClass:[NSObject class]]
```