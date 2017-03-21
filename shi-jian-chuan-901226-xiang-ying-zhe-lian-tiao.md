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

##1. 事件的产生&传递
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

寻找最适合的View的过程中涉及到两个方法`hitTest` & `PointInside`

######hitTest方法
```
-(UIView *)hitTest:(CGPoint)point withEvent:(UIEvent *)event
```
作用:         寻找最适合的View
参数:         当前手指所在的点, 产生的事件
返回值:       返回最适合的View
什么时候调用:  只要一个控件接收到一个事件时, 就会调用这个控件的hitTest

######PointInside方法
```
-(BOOL)pointInside:(CGPoint)point withEvent:(UIEvent *)event
```
作用:          判断point在不在方法的调用者身上
参数:          point必须是 方法调用者的坐标系 上在方法调用者范围内
什么时候调用:    hitTest方法底层会调用该方法, 判断点是否在控件上

##2. 事件响应
用户点击屏幕后产生的一个触摸事件，经过一系列的传递过程后，会找到最合适的视图控件来处理这个事件, 找到最合适的视图控件后,就会调用控件的touches 法来作具体的事件处理 那这些touche方法的默认做法是将事件顺着响应者链条向上传递，将事件交给上一个响应者进行处理

#####响应者链条
由多个响应者对象连接起来的链条 就叫响应者链条.


<br />
<br />
<br />




