# ViewController 的 loadView,、viewDidLoad,、viewDidUnload 分别是在什么时候调用的？

* viewDidLoad在view从nib文件初始化时调用，loadView在controller的view为nil时调用。

* 此方法在编程实现view时调用,view控制器默认会注册memory warning notification,当view controller的任何view没有用的时候，viewDidUnload会被调用，在这里实现将retain的view release,如果是retain的IBOutlet view 属性则不要在这里release,IBOutlet会负责release 。