# NSThread
NSThread 

```
// 获取主线程
NSthread *mainThread = [NSThread mainThread];

// 获取当前线程
NSThread *currentThread = [NSThread currentThread];

// 判断线程是否是组现场
BOOL isMainThread = [current isMainThread];

// 创建线程
NSThread *thread = [[NSThread alloc] initWithTarget:self selector:@selector(run:) object:nil];

// 启动
[thread start];
  
```



