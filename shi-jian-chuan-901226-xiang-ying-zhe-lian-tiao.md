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