# 深拷贝和浅拷贝

* 如果对象有个指针型成员变量指向内存中的某个资源，那么如何复制这个对象呢？你会只是复制指针的值传给副本的新对象吗？指针只是存储内存中资源地址的占位符。在复制操作中，如果只是将指针复制给新对象，那么底层的资源实际上仍然由两个实例在共享。

![](http://upload-images.jianshu.io/upload_images/1713024-3c9b9c263f791aa6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 浅复制：两个实例的指针仍指向内存中的同一资源，只复制指针值而不是实际资源；

* 深复制：不仅复制指针值，还复制指向指针所指向的资源。如下图：

![](http://upload-images.jianshu.io/upload_images/1713024-44f290757378d16f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

