#一丶源码
```

#import <pop/POPPropertyAnimation.h>

/**
基础动画
*/
@interface POPBasicAnimation : POPPropertyAnimation

/**
类创建实例
*/
+ (instancetype)animation;

/**
指定属性动画;
*/
+ (instancetype)animationWithPropertyNamed:(NSString *)name;

/**
使用kCAMediaTimingFunctionDefault 定时功能的基本动画;
*/
+ (instancetype)defaultAnimation;

/**
@使用kCAMediaTimingFunctionLinear 定时功能的基本动画;
*/
+ (instancetype)linearAnimation;

/**
@使用kCAMediaTimingFunctionEaseIn 定时功能的基本动画;
*/
+ (instancetype)easeInAnimation;

/**
@使用kCAMediaTimingFunctionEaseOut 定时功能的基本动画;
*/
+ (instancetype)easeOutAnimation;

/**
@使用kCAMediaTimingFunctionEaseIn 定时功能的基本动画;
*/
+ (instancetype)easeInEaseOutAnimation;

/**
延迟多少秒执行动画:Defaults to 0.4.
*/
@property (assign, nonatomic) CFTimeInterval duration;

/**
设置动画节奏,默认使用:kCAMediaTimingFunctionDefault

CA_EXTERN NSString * const kCAMediaTimingFunctionLinear
CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
CA_EXTERN NSString * const kCAMediaTimingFunctionEaseIn
CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
CA_EXTERN NSString * const kCAMediaTimingFunctionEaseOut
CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
CA_EXTERN NSString * const kCAMediaTimingFunctionEaseInEaseOut
CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
CA_EXTERN NSString * const kCAMediaTimingFunctionDefault
CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);

*/
@property (strong, nonatomic) CAMediaTimingFunction *timingFunction;

@end

```

#二丶问题及使用:
以下图来之:http://www.cocoachina.com/ios/20150728/12734.html
/** Timing function names. **/

CA_EXTERN NSString * const kCAMediaTimingFunctionLinear

![Linear.png](http://upload-images.jianshu.io/upload_images/1986326-3faea770f32b6ae5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

CA_EXTERN NSString * const kCAMediaTimingFunctionEaseIn


![EaseIn.png](http://upload-images.jianshu.io/upload_images/1986326-162a4a4ed5defa91.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

CA_EXTERN NSString * const kCAMediaTimingFunctionEaseOut



![EasyInEasyOut.png](http://upload-images.jianshu.io/upload_images/1986326-b7b91f28d4ab8a10.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

CA_EXTERN NSString * const kCAMediaTimingFunctionEaseInEaseOut



![EasyInEasyOut.png](http://upload-images.jianshu.io/upload_images/1986326-253c3881990922a7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





简单使用;后期介绍property
```

POPBasicAnimation * butAnimation = [POPBasicAnimation animationWithPropertyNamed:kPOPViewCenter];
butAnimation.duration = 1.0f;
butAnimation.toValue = [NSValue valueWithCGSize:CGSizeMake(_btn.centerX,_btn.centerY + 400)];
[_btn pop_addAnimation:butAnimation forKey:@"btn_Animation"];
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
