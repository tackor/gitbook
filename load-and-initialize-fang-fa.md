# load & initialize 方法

```
+ (void)load & +(void)initialize 方法有什么用

```

* load:

    * 当类对象被引入项目时, runtime会向每一个类对象发送load消息
    * load方法会在每个类甚至分类被引入时仅调用移除, 调用顺序: 父类优先子类, 子类优先分类
    * 由于load方法会在类被 import时调用一次, 而这时旺旺是改变类的行为的最佳时间, 在这里可以使用例如 method swizlling 来修改稿原来的方法
    * load方法不会被类自动继承
    
* initialize"

    * 也是在第一次使用该类的时候调用, 也就是说initialize也是懒加载
    
总结:

    * 在Objective-C 中, runtime会自动调用每个类的这两个方法
    * load会在类被初始化加载时调用
    * initialize 会在第一次调用类的类方法或者实例方法之前被调用
    * 这两个方法是可选的, 且只有在实现他们是才会被调用
    * 两这的共同的: 两个方法都只会被调用一次
    
    
<br />
<br />
<br />