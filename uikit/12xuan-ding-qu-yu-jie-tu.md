# 选定区域截图

#### 关键思路

* 滑动手势开始的位置记录x、y

* 手势滑动过程中计算现在雨刚开始的位置的差，就是需要裁剪的宽、高

* 设置一个半透明的view，手势移动改变view的frame

* 开始图片上下文。上下文大小就是手势滑动所形成的区域

* 设置上下文裁剪区域

* 将图片的layer绘制到上下文中

* 关闭图片上下文

* 将半透明的view移除掉。

Demo

```
/*
 * 滑动手势开始的位置记录x、y
 * 手势滑动过程中计算现在雨刚开始的位置的差，就是需要裁剪的宽、高
 * 设置一个半透明的view，手势移动改变view的frame
 * 开始图片上下文
 * 上下文大小就是手势滑动所形成的区域
 * 设置上下文裁剪区域
 * 将图片的layer绘制到上下文中
 */
-(IBAction)panGestureMoved:(UIPanGestureRecognizer *)pan{
    CGPoint currentLoaction = [pan locationInView:self.view];
    CGFloat offsetWidth = currentLoaction.x - self.startPoint.x;
    CGFloat offsetHeight = currentLoaction.y - self.startPoint.y;
    CGRect rect = CGRectMake(self.startPoint.x, self.startPoint.y, offsetWidth, offsetHeight);

    if (pan.state == UIGestureRecognizerStateBegan) {
        self.startPoint = [pan locationInView:self.view];
    }else if(pan.state == UIGestureRecognizerStateChanged){
        self.coverView.frame = rect;
    }else if(pan.state == UIGestureRecognizerStateEnded){
       /*
        * UIKIT_EXTERN void     UIGraphicsBeginImageContextWithOptions(CGSize size, BOOL opaque, CGFloat scale) NS_AVAILABLE_IOS(4_0);
        * opaque : 如果图片不需要透明效果，设置为YES。
        * scale : 缩放因子 iPhone 4是2.0，其他是1.0。如果设置为0，系统则根据[UIScreen mainScreen].scale 获取
        */
        UIGraphicsBeginImageContextWithOptions(CGSizeMake(self.imageView.bounds.size.width, self.imageView.bounds.size.height), NO, 0);
        CGContextRef ctx = UIGraphicsGetCurrentContext();
        UIBezierPath *path = [UIBezierPath bezierPathWithRect:rect];
        [path addClip];

        CGContextAddPath(ctx, path.CGPath);
        [self.imageView.layer renderInContext:ctx];


        UIImage *imageGot = UIGraphicsGetImageFromCurrentImageContext();

        self.imageView.image = imageGot;
        UIGraphicsEndImageContext();

         [self.coverView removeFromSuperview];
    }
}

#pragma mark -- lazy load

-(UIView *)coverView{
    if (!_coverView) {
       UIView *cover = [[UIView alloc] init];
        cover.backgroundColor = [UIColor blackColor];
        cover.alpha = 0.6;
        [self.view addSubview:cover];
        _coverView = cover;
    }
    return _coverView;
}
```



