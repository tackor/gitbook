#Assets.xcassets 和 直接用图片 的 区别

###将图片放入Assets.xcassets

* 在mainBundle里面Xcode会生成一个Assets.car文件，将我们放在Images.xcassets的图片打包在里面。

* 无论是通过imageNamed:来加载图片，还是直接在Storyboard的UIImageView里面设置图片，并且无论图片是jpg格式还是png格式，都不需要写后缀名。

* 放在Images.xcassets的图片不能通过imagesWithContentsOfFile:来加载。（因为这个方法相当于是去mainBundle里面找图片，但是这些图片都被打包进了Assets.car文件）

###直接拖入图片

* 直接拖入图片相当于直接将图片放入了mainBundle里面。

* 如果在Storyboard的UIImageView设置图片，那么需要明确地写上后缀名。（无论是.png还是.jpg都要写）

* 在使用imageNamed:加载图片时，如果是.png格式，则不需要使用后缀名；如果是.jpg格式，则必须要写上后缀名。

