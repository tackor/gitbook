# UITableViewCell上有个UILabel，显示NSTimer实现的秒表时间，手指滚动cell过程中，label是否刷新，为什么？

这是否刷新取决于timer加入到Run Loop中的Mode是什么。Mode主要是用来指定事件在运行循环中的优先级的，分为：

    * NSDefaultRunLoopMode（kCFRunLoopDefaultMode）：默认，空闲状态
    * UITrackingRunLoopMode：ScrollView滑动时会切换到该Mode
    * UIInitializationRunLoopMode：run loop启动时，会切换到该mode
    * NSRunLoopCommonModes（kCFRunLoopCommonModes）：Mode集合 苹果公开提供的Mode有两个：
        1. NSDefaultRunLoopMode（kCFRunLoopDefaultMode）
        2. NSRunLoopCommonModes（kCFRunLoopCommonModes）

在编程中：如果我们把一`NSTimer`对象以`NSDefaultRunLoopMode（kCFRunLoopDefaultMode）`添加到主运行循环中的时候, `ScrollView`滚动过程中会因为`mode`的切换，而导致`NSTimer`将不再被调度。当我们滚动的时候，也希望不调度，那就应该使用默认模式。但是，如果希望在滚动时，定时器也要回调，那就应该使用`common mode`。
    