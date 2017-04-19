#一丶源码

```

#import <pop/POPPropertyAnimation.h>

/**
弹簧动画类;通过弹簧动力学模型实现动画
*/
@interface POPSpringAnimation : POPPropertyAnimation

/**
初始化一个实例
*/
+ (instancetype)animation;

/**
指定属性动画的实例
*/
+ (instancetype)animationWithPropertyNamed:(NSString *)name;

/**
当前速度;
做动画开始之前应该设置初始速度;
*/
@property (copy, nonatomic) id velocity;

/**
反弹力度
范围 [0, 20]. 默认 4.
*/
@property (assign, nonatomic) CGFloat springBounciness;

/**
速度
范围 [0, 20]. 默认 to 12.
*/
@property (assign, nonatomic) CGFloat springSpeed;

/**
拉力
*/
@property (assign, nonatomic) CGFloat dynamicsTension;

/**
摩擦力
*/
@property (assign, nonatomic) CGFloat dynamicsFriction;

/**
质量
*/
@property (assign, nonatomic) CGFloat dynamicsMass;

@end

```
#二丶问题及使用:

这个...制作弹簧动画,


可以看下胡克定义:
以下来源百度:
```
F=-k·x
表达式为F=-k·x或△F=-k·Δx
，弹簧的弹力F和弹簧的伸长量（或压缩量）x成正比，即F= k·x 。
k是物质的弹性系数，它只由材料的性质所决定，与其他因素无关。
负号表示弹簧所产生的弹力与其伸长（或压缩）的方向相反。
```


###1.@property (copy, nonatomic) id velocity;
初始速度


###2.@property (assign, nonatomic) CGFloat springBounciness;
反弹力度


![反弹力度.gif](http://upload-images.jianshu.io/upload_images/1986326-2bc7b782fd24d369.gif?imageMogr2/auto-orient/strip)
###3.@property (assign, nonatomic) CGFloat springSpeed;
速度


![速度.gif](http://upload-images.jianshu.io/upload_images/1986326-3072e6f2739c15fd.gif?imageMogr2/auto-orient/strip)
/**
拉力:影响回弹力度以及速度
*/
###4.@property (assign, nonatomic) CGFloat dynamicsTension;

![拉力.gif](http://upload-images.jianshu.io/upload_images/1986326-d9d9e70736568a59.gif?imageMogr2/auto-orient/strip)

值越大,动画速度越快

/**
摩擦力:如果开启，动画会不断重复，幅度逐渐削弱，直到停止。
*/
###5.@property (assign, nonatomic) CGFloat dynamicsFriction;

![抹茶李.gif](http://upload-images.jianshu.io/upload_images/1986326-073a5b7cbcf490bd.gif?imageMogr2/auto-orient/strip)



###6.@property (assign, nonatomic) CGFloat dynamicsMass;
//细微的影响动画的回弹力度以及速度

示例:
```
POPSpringAnimation *springAnimaiton = [POPSpringAnimation animationWithPropertyNamed:kPOPLayerPositionY];
springAnimaiton.toValue = @(500);
[_btn pop_addAnimation:springAnimaiton forKey:@"springAnimation"];

springAnimaiton.springBounciness = 20;
springAnimaiton.springSpeed = 20;

以下这3个比较难用;如果不是特别需求,springBounciness和springSpeed就可以解决问题;

//    springAnimaiton.dynamicsTension = _value1;
//    springAnimaiton.dynamicsFriction = _value2;
//    springAnimaiton.dynamicsMass = _value3;

```

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
