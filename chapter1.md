# 三种传值

所谓的三种传值问题 指的是iOS类与类制剂的三种传值方式, 这三种方式分别是: `通过代理方式传值`,  `通过Block传值`, `通过通知进行传值`

###1. 代理方式 (代理模式)

传入的对象,代替当前类完成了某一个功能,称为代理模式.

代理的实现逻辑:
```
//在要传值的类中

1> 声明代理方法

2> 定义代理属性

3> 在适当的时候调用代理方法
```

```
//在要接受值的类中

1> 设置代理对象

2> 遵守代理协议

3> 实现代理方法
```

逻辑图:

![](http://upload-images.jianshu.io/upload_images/1899934-20edac2be8773c3f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

实现代码:

```
B.H类  类名  name
///声明代理方法
@protocol  nameDelegate <NSObject>

- (void)name:(B *)VC ;

@end

///定义代理属性
@property (nonatomic, weak) id<nameDelegate> delegate;

B.M
///在合适的时候调用代理方法
 if ([self.delegate respondsToSelector:@selector(a:)]) {
        [self.delegate a:self];
    }

A.M
///设置代理对象,获取B
B *b = [[B alloc]init];

b.delegate = self;

///遵守代理协议
@interface contactController ()<nameDelegate>

///实现代理方法
- (void)name:(B *)VC { }
```








