#1. iOS中成员变量和属性区别

接触iOS的人都知道，@property声明的属性默认会生成一个_类型的成员变量，同时也会生成setter/getter方法。 
但这只是在iOS5之后，苹果推出的一个新机制。看老代码时，经常看到一个大括号里面定义了成员变量，同时用了@property声明，而且还在@implementation中使用@synthesize方法。 

// iOS5之后的代码
```
//
//  Person.h
//  Deom01
//
//  Created by 时空矩人 on 2017/3/22.
//  Copyright © 2017年 时空矩人. All rights reserved.
//

#import <Foundation/Foundation.h>

@interface Person : NSObject

@end


//
//  Person.m
//  Deom01
//
//  Created by 时空矩人 on 2017/3/22.
//  Copyright © 2017年 时空矩人. All rights reserved.
//

#import "Person.h"

@interface Person()

/** 名字 */
@property (nonatomic, strong) NSString *name;

/** 高度 */
@property (nonatomic, assign) int height;

@end

@implementation Person

@end

```

//iOS5之前的代码
```
//
//  Person.h
//  Deom01
//
//  Created by 时空矩人 on 2017/3/22.
//  Copyright © 2017年 时空矩人. All rights reserved.
//

#import <Foundation/Foundation.h>

@interface Person : NSObject

@end


//
//  Person.m
//  Deom01
//
//  Created by 时空矩人 on 2017/3/22.
//  Copyright © 2017年 时空矩人. All rights reserved.
//

#import "Person.h"

@interface Person()
{
    //1. 声明成员变量
    NSString *name;
    int height;
}

//2. 用@property
@property (nonatomic, copy) NSString *name;
@property (nonatomic, assign) int height;

@end

@implementation Person

//3. 最好在@implementation中用@synthesize生成get,set方法
@synthesize name;
@synthesize height;

@end

```
其实, 发生这种状况根本原因是苹果将默认编译器从GCC转换为LLVM(low level virtual machine)，才不再需要为属性声明实例变量了。

在没有更改之前，属性的正常写法需要三个步骤:
    声明成员变量 - 写在 interface的大括号中
    @property  - 写在 interface的大括号外部
    @synthesize 成员变量
    
如果我们只写成员变量+ @property:

```
@interface GBViewController :UIViewController
{
    NSString *myString;
}
@property (nonatomic, strong) NSString *myString;
@end
```
Autosynthesized property 'myString' will use synthesized instance variable '_myString', not existing instance variable 'myString'

```

但更换为LLVM之后，编译器在编译过程中发现没有新的实例变量后，就会生成一个下划线开头的实例变量。因此现在我们不必在声明一个实例变量。（注意：==是不必要，不是不可以==） 

当然我们也熟知，@property声明的属性不仅仅默认给我们生成一个_类型的成员变量，同时也会生成setter/getter方法。

在.m文件中，编译器也会自动的生成一个实例变量_myString。那么在.m文件中可以直接的使用_myString实例变量，也可以通过属性self.myString.都是一样的。

注意这里的self.myString其实是调用的myString属性的setter/getter方法。这与C++中点的使用是有区别的，C++中的点可以直接访问成员变量(也就是实例变量)。

例如在OC中有如下代码:
```
@interface MyViewController :UIViewController
{
    NSString *name;
}
@end
```

在这段代码里面只是声明了一个成员变量，并没有setter/getter方法。所以访问成员变量时，可以直接访问name，也可以像C++一样用self->name来访问，但绝对不能用self.name来访问。

    * 扩展:很多人觉得OC中的点语法比较奇怪，实际是OC设计人员有意为之。
    
    * 点表达式(.)看起来与C语言中的结构体访问以及java语言汇总的对象访问有点类似，如果点表达式出现在等号 ＝ 左边，调用该属性名称的setter方法。如果点表达式出现在＝右边，调用该属性名称的getter方法。

    * OC中点表达式(.)其实就是调用对象的setter和getter方法的一种快捷方式，self.myString = @"张三";实际就是[self setmyString:@"张三"];

那么问题来了： 
我们能否认为新编译器LLVM下的@property == 老编译器GCC的 成员变量+ @property + @synthesize 成员变量呢？

答案是否定的。 
因为成员变量+ @property + @synthesize 成员变量的形式，编译器不会帮我们生成_成员变量，因此不会操作_成员变量了； 
同时@synthesize 还有一个作用，可以指定与属性对应的实例变量， 
例如@synthesize myString = xxx； 
那么self.myString其实是操作的实例变量xxx，而非_String了。


#2. 有了自动合成属性实例变量之后, @synthesize 还有哪些使用场景

什么情况下不会自动合成(autosynthesis)

    * 同时写了getter & setter
    * 重写了只读属性的getter
    * 使用了@dynamic时
    * 在@protocol 中定义的所有属性
    * 在category 中定义的所有属性
    * 重载的属性, 当你在子类中重载了父类中的属性, 必须使用@synthesize来手动合成ivar
    
    
应用场景

    * 当你重写了setter & setter时, 系统不会生成ivar, 这时候你可以:
        1. 手动创建ivar(实例变量)
        2. 使用@synthesize foo = _foo; 关联@property 与 ivar
        
    * 可以用来修改成员变量名, 一般不建议这么做
    
    
  
  
<br />
<br />
<br />
