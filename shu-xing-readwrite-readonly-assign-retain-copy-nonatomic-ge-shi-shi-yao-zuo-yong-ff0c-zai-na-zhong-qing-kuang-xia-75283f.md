# 属性readwrite，readonly，assign，retain，copy，nonatomic 各是什么作用，在那种情况下用?


1 readwrite 是可读可写特性;需要生成getter方法和setter方法时

2 readonly 是只读特性 只会生成getter方法 不会生成setter方法 ;不希望属性在类外改变

3 assign 是赋值特性，setter方法将传入参数赋值给实例变量;仅设置变量时;

4 retain 表示持有特性，setter方法将传入参数先保留，再赋值，传入参数的retaincount会+1;

5 copy 表示赋值特性，setter方法将传入对象复制一份;需要完全一份新的变量时。

6 nonatomic 非原子操作，决定编译器生成的setter getter是否是原子操作，atomic表示多线程安全，一般使用nonatomic
