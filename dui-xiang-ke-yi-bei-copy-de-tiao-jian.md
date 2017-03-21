# 对象可以被copy的条件

* 只有实现了`NSCopying`和`NSMutableCopying`协议的类的对象才能被拷贝,分为不可变拷贝和可变拷贝,具体区别戳这；

* `NSCopying`协议方法为：
```
- (id)copyWithZone:(NSZone *)zone {
 MyObject *copy = [[[self class] allocWithZone: zone] init];
 copy.username = [self.username copyWithZone:zone];
 return copy;
}
```

<a href='http://www.jianshu.com/p/f84803356cbb'>NSCopying和NSMutableCopying协议</a>