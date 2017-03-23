# ARC下会存在内存泄漏吗?

* 循环引用会导致内存泄漏

* Objective-C 对象与CoreFoundation对象进行桥接的时候如果管理不当会造成内存泄漏

* CoreFoundation中的对象不受ARC 管理, 需要开发者手动释放

