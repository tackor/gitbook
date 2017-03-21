#事件传递&响应者链条

###1. iOS中常用的事件

    * 触摸事件
    * 加速计事件 
    * 远程控制事件
    
###2. 响应者对象
继承了`UIResponds`的对象我们称它为响应者对象

UIApplication、UIViewController、UIView都继承 UIResponder 因此它们都是响应者对象，都能够接收并处理事件

###3. 为什么继承了UIResponder就能够处理事件?
因为UIResponder内部提供了以下方法来处理事件  

如
```
//触摸事件会调用以下方法:
- (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event;

- (void)touchesMoved:(NSSet *)touches withEvent:(UIEvent *)event;

- (void)touchesEnded:(NSSet *)touches withEvent:(UIEvent *)event;

- (void)touchesCancelled:(NSSet *)touches withEvent:(UIEvent *)event; 

//加速计事件会调用以下方法:
- (void)motionBegan:(UIEventSubtype)motion withEvent:(UIEvent *)event;

- (void)motionEnded:(UIEventSubtype)motion withEvent:(UIEvent *)event;

- (void)motionCancelled:(UIEventSubtype)motion withEvent:(UIEvent *)event; 

//远程控制事件会调用:
- (void)remoteControlReceivedWithEvent:(UIEvent *)event;
```

###4.如何监听UIView的触摸事件? 
想要监听UIViiew的触摸事件, 先第 步要 定义UIView, 因为只有实现了UIResponder的事件放法才能够监听事件.

```
UIView的触摸事件主要有: 一根或者多根手指开始触摸view，系统会自动调 view的下面方法. 
- (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event 

一根或者多根手指在view上移动时，系统会自动调 view的下面方法 (随着手指的移动，会持续调用该方法,也就是说这个方法会调用很多次)
- (void)touchesMoved:(NSSet *)touches withEvent:(UIEvent *)event 

一根或者多根手指离开view，系统会自动调 view的下面方法
- (void)touchesEnded:(NSSet *)touches withEvent:(UIEvent *)event
```

##事件的产生&传递
1. 当用户点击设备屏幕时，iOS捕捉到一系列的触摸，将其打包到UIEvent对象并放置到应用程序活动事件队列中

2. UIApplication对象从事件队列中取出最前面的事件并将其分发，通常，其将事件发送给应用程序的主窗口(UIWindow实例)，主窗口会在视图层次结构中找到一个最合适的视图来处理触摸事件(也就是主窗口会发送事件给第一响应者来处理)，一般通过touchesBegan方法获取该事件

注意:

触摸事件的传递是从父控件传递给子控件的
如果一个父控件不能接收事件,那么它里面的子控件也不能够接收事件.

UIView不能接受触摸事件的三种情况
    
```
1. userInteractionEnabled = NO  //不接受用户交互
2. hidden = YES                 // 隐藏
3. alpha = 0.0 ~ 0.01           //透明
```

###1. 寻找最适合的View的过程

    1.先判断自己是否能够接收触摸事件,
    2.如果能, 再判断触摸的当前点在不在自己的身上.
    3.如果在自己身上,它会从后往前遍历子控件,遍历出每个子控件后,重复前 的两个步骤.
    4.如果没有符合条件的子控件,那么它自己就是最适合的View.






