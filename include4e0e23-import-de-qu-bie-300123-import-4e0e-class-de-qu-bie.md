# #include与#import的区别、#import 与 @class 的区别

```
1. #include 和#import其效果相同,都是查询类中定义的行为(方法);
2. #import不会引起交叉编译,确保头文件只会被导入一次；
3. @class 的表明,只定 义了类的名称,而具体类的行为是未知的,一般用于.h 文件；
4. @class 比#import 编译效率更高。
5. 此外@class 和#import 的主要区别在于解决引用死锁的问题。
```

#import 跟#include 又什么区别，@class呢, #import<> 跟 #import””又什么区别?
```
#import是Objective-C导入头文件的关键字，#include是C/C++导入头文件的关键字,使用#import头文件会自动只导入一次，不会重复导入，相当于#include和#pragma once;@class告诉编译器某个类的声明，当执行时，才去查看类的实现文件，可以解决头文件的相互包含;#import<>用来包含系统的头文件，#import””用来包含用户头文件。
```