#一丶原文
```


#import <pop/POPAnimatableProperty.h>
#import <pop/POPAnimation.h>

/**
@abstract Flags for clamping animation values.
@discussion Animation values can optionally be clamped to avoid overshoot. kPOPAnimationClampStart ensures values are more than fromValue and kPOPAnimationClampEnd ensures values are less than toValue.
*/
typedef NS_OPTIONS(NSUInteger, POPAnimationClampFlags)
{
kPOPAnimationClampNone        = 0,
kPOPAnimationClampStart       = 1UL << 0,
kPOPAnimationClampEnd         = 1UL << 1,
kPOPAnimationClampBoth = kPOPAnimationClampStart | kPOPAnimationClampEnd,
};

/**
semi-concrete 属性动画子类
*/
@interface POPPropertyAnimation : POPAnimation

/**
做动画的属性
*/
@property (strong, nonatomic) POPAnimatableProperty *property;

/**
做动画的初始值;
如果未设置,则在动画启动的时候,按照对象当前的值作为初始值;
*/
@property (copy, nonatomic) id fromValue;

/**
做动画的值
如果未设置,则在动画启动的时候,按照对象当前的值作为初始值;
*/
@property (copy, nonatomic) id toValue;

/**
四舍五入系数;
作用让动画变得更圆滑; 默认0; 取1.0和取整值之间;
*/
@property (assign, nonatomic) CGFloat roundingFactor;

/**
就是让动画保证在fromValue和tovalue之间,不会越界;
*/
@property (assign, nonatomic) NSUInteger clampMode;

/**
动画的值是叠加,而不是设置;
默认NO;
*/
@property (assign, nonatomic, getter = isAdditive) BOOL additive;

@end

```

#二问题

###1.@property (assign, nonatomic) CGFloat roundingFactor; 使用;

先看看源码;
```
默认为0
roundingFactor(0),
```

继续翻
![Paste_Image.png](http://upload-images.jianshu.io/upload_images/1986326-60518113c33097b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/1986326-c998ef36cbd350f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![Paste_Image.png](http://upload-images.jianshu.io/upload_images/1986326-386c7075b345c071.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![Paste_Image.png](http://upload-images.jianshu.io/upload_images/1986326-19c7cc2b251004d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

四舍五入;

就是让每一帧动画变得更滑一点;


### @property (assign, nonatomic) NSUInteger clampMode;
庆幸是开源的,不然压根不懂它干嘛的;

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/1986326-926ddab4bdfff2c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

让动画保证在fromValue和tovalue之间,不会越界
看枚举
```
kPOPAnimationClampNone        = 0,
kPOPAnimationClampStart       = 1UL << 0, //保证fromValue开始
kPOPAnimationClampEnd         = 1UL << 1,//保证toValue开始
kPOPAnimationClampBoth = kPOPAnimationClampStart | kPOPAnimationClampEnd,
```

###@property (assign, nonatomic, getter = isAdditive) BOOL additive;

叠加,不是设置;

图片来源:http://www.tuicool.com/articles/v22QVfq

![1.gif](http://upload-images.jianshu.io/upload_images/1986326-1d30c4c332a0d6db.gif?imageMogr2/auto-orient/strip)

#三丶其他:
翻译有问题,留言告诉我下,谢谢;
以及有使用问题也可以留言,一起探讨探讨;


###POP
http://www.jianshu.com/p/2f6304ebc982

###1.POPAnamiton:
iOS_动画_POP_POPAnimation.h 中文翻译及使用经验
http://www.jianshu.com/p/5a396a7b91b2

###2.POPPropertyAnimation:
iOS_动画_POP_POPPropertyAnimation.h 翻译及使用
http://www.jianshu.com/p/74de16ffe197

###3.POPBasicAnimation
iOS_动画_POP_POPBasicAnimation.h 翻译及使用
http://www.jianshu.com/p/f51565e123a0

###4.POPSpringAnimation
iOS_动画_POP_POPSpringAnimation.h 翻译及使用
http://www.jianshu.com/p/a86595d4adca

###5.POPDecayAnimation
iOS_动画_POP_POPSpringAnimation.h 翻译及使用
http://www.jianshu.com/p/0ce7b805f56c

###6.POPCustomAnimation
iOS_动画_POP_POPCustomAnimation.h 翻译及使用
http://www.jianshu.com/p/ee07b9e8ec98
