# runtime

1. runtime机制 是什么

    RunTime机制 简称 运行时机制, 是一套底层的C语言API，它是iOS内部的核心之一，我们平时编写的OC代码，底层都是基于它来实现的. 所以在程序运行过程中, OC代码最终转成runtime的C语言代码.
    
    Objective-C是基于C, 并且在C语言的基础上加入了面向对象特性和消息转发机制的动态语言，除编译器之外，还需用Runtime机制来动态创建类和对象，消息发送和转发。
    
    所以可以说 oc是一个全动态语言，它一切都是基于runtime机制实现的！
    
2. runtime 有什么用

    从我刚才所说的你应该知道Runtime是属于OC的底层, 所以可以进行一些非常底层的操作(这些操作是我们无法通过OC实现的, 或者说不好实现的)
    
    举个例子:
        
        1. 在程序运行过程中, 动态创建一个类 (这就是KVO的底层实现)
        
        2. 遍历一个类的所有成员变量(属性)\所有的方法(字典转模型中会用到, 如mjExtension 中 就用到了)
        
        3. 在程序运行过程中, 动态地为某个类添加属性\方法, 或者动态修改属性值\方法 (这个一般在我们调用一个系统方法时, 需要在这个系统方法中添加一些操作时用到)





















<br />
<br />
<br />