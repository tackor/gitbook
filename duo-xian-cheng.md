# 线程生命周期
pthread 

  * 一套通用的用C编写的多线程API
  * 跨平台\可移植
  * 线程生命周期有程序员管理
  
NSThread

  * 使用更加面向对象
  * 简单易用, 可直接操作线程对象
  * OC编写的
  * 程序员只需要赋值创建线程, 不需要自己销毁
  
GCD

  * 旨在替代NSThread等线程技术
  * 从复利用设备的多核
  * C语言编写的, 但它的实现比较底层
  * 生命周期自动管理
  
NSOperation

  * 基于GCD (底层是GCD)
  * 比GCD多了些更坚定使用的功能
  * 使用更加面向对象
  * OC编写的
  * 生命周期自动管理

# NSThread
NSThread 

```
// 获取主线程
NSthread *mainThread = [NSThread mainThread];

// 获取当前线程
NSThread *currentThread = [NSThread currentThread];

// 判断线程是否是组现场
BOOL isMainThread = [current isMainThread];
```

创建线程,方法一:
```
// 1. 创建线程
/*
  参数一: 目标对象 self
  参数二: 要调用的方法的名称 (该方法中的实现将会在子线程中实现)
  参数三: 被调用方法的参数<最多一个, 如果没有参数 nil>
 */
NSThread *thread = [[NSThread alloc] initWithTarget:self selector:@selector(run:) object:nil];

// 2. 启动线程
[thread start];
  
```

注: 与UI相关的操作需要放在主线程中处理





