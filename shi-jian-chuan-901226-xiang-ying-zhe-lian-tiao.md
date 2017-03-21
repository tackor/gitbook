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

UIView的触摸事件主要有: 一根或者多根手指开始触摸view，系统会 动调 view的下  法. - (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event 根或者多根 指在view上移动时，系统会 动调 view的下  法 (随着 指的移动，会持续调 该 法,也就是说这个 法会调 很多次)- (void)touchesMoved:(NSSet *)touches withEvent:(UIEvent *)event 根或者多根 指离开view，系统会 动调 view的下  法- (void)touchesEnded:(NSSet *)touches withEvent:(UIEvent *)event