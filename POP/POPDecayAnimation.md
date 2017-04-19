一丶源码
```

#import <pop/POPPropertyAnimation.h>

/**
衰减动画,也有称阻尼动画
*/
@interface POPDecayAnimation : POPPropertyAnimation

/**
实例对象
*/
+ (instancetype)animation;

/**
指定属性动画的实例
*/
+ (instancetype)animationWithPropertyNamed:(NSString *)name;

/**
初始速度;
支持:
kPOPValuePoint, 
kPOPValueInteger,
kPOPValueFloat,
kPOPValueRect,
kPOPValueSize.
*/
@property (copy, nonatomic) id velocity;

/**
原始速度
用于设置 autoreverse 和 repeatCount
*/
@property (copy, nonatomic, readonly) id originalVelocity;

/**
减速:较低的值会更快的减速
范围[0, 1]. 默认 0.998.
*/
@property (assign, nonatomic) CGFloat deceleration;

/**
预计持续时间;
根据 velocity 和 deceleration 得出
*/
@property (readonly, assign, nonatomic) CFTimeInterval duration;

/**
基于Velocity 和 deceleration;
*/
- (void)setToValue:(id)toValue NS_UNAVAILABLE;

/**
反转速度
*/
- (id)reversedVelocity;

@end


```

#二丶问题及示例:

```
POPDecayAnimation *anim = [POPDecayAnimation animationWithPropertyNamed:kPOPLayerPositionY];
anim.velocity = @(300);
[_btn pop_addAnimation:anim forKey:@"slide"];
```


![1.gif](http://upload-images.jianshu.io/upload_images/1986326-ad3c6a834c151816.gif?imageMogr2/auto-orient/strip)
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
