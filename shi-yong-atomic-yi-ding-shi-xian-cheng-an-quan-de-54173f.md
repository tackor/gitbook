# 使用atomic 一定是线程安全的吗?

不是, atomic的本意是指属性的存取方法是线程安全的, 并不保证整个对象是线程安全的, 比如: 声明一个可变数组(NSMutableArray)的原子属性 stuff, 此时self.stuff & self.stuff = otherStuff 都是线程安全的, 但是 使用[self.stuff objectAtIndex:index] 就不是线程安全的, 需要用互斥锁来保证线程安全.

```
@property (atomic, strong) NSMutableArray *stuff;

那么:
self.stuff   //获取 是安全的
self.stuff = othersuff  //保存 是安全的

[self.stuff objectAtIndex:index]  // 不是线程安全的

```