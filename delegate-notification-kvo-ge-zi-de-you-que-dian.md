
#Delegate, Notification, KVO 各自的优缺点

在开发ios应用的时候，我们会经常遇到一个常见的问题：在不过分耦合的前提下，controllers间怎么进行通信。

在iOS应用不断的出现三种模式来实现这种通信：

    1.代理,委托 delegation

    2.通知中心 Notification Center

    3.键值观察(key value observing) KVO

