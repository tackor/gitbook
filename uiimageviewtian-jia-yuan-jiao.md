# UIImageView添加圆角

* 最直接的方法就是使用如下属性设置：

```
imgView.layer.cornerRadius = 10;
// 这一行代码是很消耗性能的
imgView.clipsToBounds = YES;
```

* 给UIImage添加生成圆角图片的扩展API：这是on-screen-rendering

```
- (UIImage *)imageWithCornerRadius:(CGFloat)radius {
    CGRect rect = (CGRect){0.f, 0.f, self.size};
    
    UIGraphicsBeginImageContextWithOptions(self.size, NO, UIScreen.mainScreen.scale);
    CGContextAddPath(UIGraphicsGetCurrentContext(),
     [UIBezierPath bezierPathWithRoundedRect:rect cornerRadius:radius].CGPath);
    CGContextClip(UIGraphicsGetCurrentContext());
    
    [self drawInRect:rect];
    UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
    
    UIGraphicsEndImageContext();
    
    return image;
}
```