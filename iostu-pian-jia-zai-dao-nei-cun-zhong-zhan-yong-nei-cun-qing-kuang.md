#iOS图片加载到内存中占用内存情况

(cocos2dx 图片资源占用内存算法是 2的整数倍宽*2的整数倍高*4  例如：960*1704  占用的内存是1024*2048*4， 并不是960*1704*4)

可以用工具Instruments 查看图片占用内存情况

<a href='http://www.cnblogs.com/lishuming/p/5224618.html'>http://www.cnblogs.com/lishuming/p/5224618.html</a>