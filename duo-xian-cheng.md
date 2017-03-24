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
  
# 线程的状态

//1. 新建状态 (new)
NSThread *thread = [[NSThread alloc] initWithTarget:self selector:@selector(run) object:nil];
// 新建状态, 此时 线程被放入`内存`, 但是不是在`可调度线程池`中

//2. 就绪状态 (Runnable)
[thread start];
线程被放入到了`可调度线程池里`, 此时CPU调用当前线程以及其他线程, 每个线程都调用一片时间

//3. 阻塞状态 (blocked)
当我们调用了sleep方法, 或者等待同步锁时, 线程处于阻塞状态时, 线程会被移出可调度线程池, 当等待时间结束之后, 有会被放入可调度线程池继续被CPU调度

//4. 死亡状态
如果线程任务执行完毕, 或者异常, 强制退出,那么线程会进入死亡状态, 死亡了的线程无法继续使用

![](/assets/Snip20170324_1.png)

### 手动设置 线程状态

//1. 新建状态 (new)
NSThread *thread = [[NSThread alloc] initWithTarget:self selector:@selector(run) object:nil];

//2. 线程在 就绪状态 与 运行状态之间切换
[thread start];

- (void)run {

  //3. 阻塞线程
  [NSThread sleepForTimeInterval:2.0] //阻塞线程, 时间 2s
  
  // 也可以用一下方法 阻塞线程
  [NSThread sleepUntilDate:[NSDate dateWithTimeIntervalSinceNow:3.0];
  
  for (int i = 0; i < 100; i++) {
    if (i == 50) {
      [NSThread exit];   // 强制退出线程, 一旦线程退出,就不能在使用.
      
      // 也可以使用一下的, 退出任务
      // break;
    }
  }
  
}

# 线程安全 (使用互斥锁)
当多个线程使用同一块资源时 需要使用线程锁, 但是给线程是很耗性能的, 加锁的时候, 需要注意加锁的位置

```
- (void)run {
  @synchronized(self) {
    // 需要在子线程中执行的代码
  }
}
```

线程同步, 多线程是并发执行, 通过加锁可以实现多个线程按一定顺序执行. 线程默认是异步执行的

# 原子 & 非原子属性 (atomic & nonatomic)

* 一个属性默认是atomic,

* atomic 原子属性, 会为setter方法加锁(互斥锁), 线程安全, 但是需要消耗大量资源

* nonatomic 非原子属性, 不会为setter方法加锁

iOS开发中
1. 所有的声明为nonatomic
2. 尽量避免多线程抢夺同一块资源
3. 零件将加锁, 资源抢夺d额业务逻辑交给服务器处理.

#线程间通信
在一个进程中, 往往有多个线程, 多个线程自己需要通信
比如图片的下载& 显示这个需求, 我们会把图片下载放在子线程中处理, 图片的展示放在UI线程中处理.

```
[NSThread detachNewThreadSelector:@selector(downImg) toTarget:self withObject: nil];

- (void)downImg {

  // 1. 在子线程中下载图片
  NSURL *url = [NSURL URLWithString:@"www.badf.sss.jpg"];
  NSData *imgData = [NSData dataWithContentsOfURL:url];
  UIImage *img = [UIImage imageWithData:imgData];
  
  // 2. 回到主线程中刷新UI
  [self performSelectorOnMainThread:@selector(showImg:) withObject:img];
    
// 也可以用performSelector: onThread: withObject: waitUntilDown:
  
}

- (void)showImg:(UIImage *)img {
{
  self.imgView.image = img;
}
```


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
// 1. 创建线程(用alloc ,init 创建的线程, 默认是处于未启动状态的, 需要手动启动)
/*
  参数一: 目标对象 self
  参数二: 要调用的方法的名称 (该方法中的实现将会在子线程中实现)
  参数三: 被调用方法的参数<最多一个, 如果没有参数 nil>
 */
NSThread *thread = [[NSThread alloc] initWithTarget:self selector:@selector(run) object:nil];

// 设置线程的名称
thread.name = @"线程A"

// 设置线程的优先级(0 ~ 1) 默认0.5
thread.threadPriority = 1.0;

// 2. 启动线程
[thread start];

// 3. 获取当前线程
NSThread *curThread = [NSThread currentThread];

// 4. 获取当前线程名称
NSString *curThreadName = curThread.name;
  
```

分离出一条新的线程, 方法二:
```
[NSThread detachNewThreadSelector:@selector(run:) toTarget:self withObject: @"这是一条子线程"];
```
这种方法可以不需要手动开启子线程, 子线程一创建出来就处于启动状态,
但是无法获取当前线程


开启一条后台线程, 方法三:
```
[self performSelectorInBackground:@selector(run) withObject:nil waitUntillDown:YES];
```
自动启动, 但是不能获取线程

注: 与UI相关的操作需要放在主线程中处理

#GCD
* 什么是GCD

*任务: 需要执行的操作

*队列: 用来存放任务的, 赋值安排线程来执行任务

###GCD的使用 (2个步骤)
1. 定制任务: 
    * 确定要做什么事情

2. 将任务添加到队列中
    * GCD会自动将队列中的任务取出, 放到对应的线程中执行
    * 任务的取出遵循队列的FIFO原则, 先进先出



<br />
<br />
<br />


