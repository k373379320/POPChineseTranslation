#一丶源码

```

#import <pop/POPAnimation.h>

@class POPCustomAnimation;

/**
是自定义动画的回调块
每个帧动画回调此block,最新的属性;
target:动画对象,避免循环;
animation:动画实例,确定上次回调来的当前时间,和已经使用的时间;避免循环使用;
return no = 动画完成;
*/
typedef BOOL (^POPCustomAnimationBlock)(id target, POPCustomAnimation *animation);

/**
自定义动画
*/
@interface POPCustomAnimation : POPAnimation

/**
初始化,并返回一个动画实例
*/
+ (instancetype)animationWithBlock:(POPCustomAnimationBlock)block;

/**
当前动画的时间
*/
@property (readonly, nonatomic) CFTimeInterval currentTime;

/**
上次回调的时间
*/
@property (readonly, nonatomic) CFTimeInterval elapsedTime;

@end

```
#二丶问题及实例




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
