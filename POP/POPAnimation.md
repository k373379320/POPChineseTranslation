#一丶原文翻译
```
#import <Foundation/NSObject.h>

#import <pop/POPAnimationTracer.h>
#import <pop/POPGeometry.h>

@class CAMediaTimingFunction;

/**
动画的抽象基类.
*/
@interface POPAnimation : NSObject

/**
* 动画的名称
* 根据这个属性用来区别动画;识别动画
*/
@property (copy, nonatomic) NSString *name;

/**
动画的开始时间;
默认是从0开始启动
*/
@property (assign, nonatomic) CFTimeInterval beginTime;

/**
动画的delegete
详情查看查看[POPAnimationDelegate]
*/
@property (weak, nonatomic) id delegate;

/**
动画的追踪器
记录所有动画相关事件,还允许完成后对其进行查询和分析;更多可以查看[POPAnimationTracer.h]
*/
@property (readonly, nonatomic) POPAnimationTracer *tracer;

/**
动画开始的时候回调的block
*/
@property (copy, nonatomic) void (^animationDidStartBlock)(POPAnimation *anim);

/**
动画达到toValue或者超过值的时候调用的block
*/
@property (copy, nonatomic) void (^animationDidReachToValueBlock)(POPAnimation *anim);

/**
动画完成的时候调用的block
*/
@property (copy, nonatomic) void (^completionBlock)(POPAnimation *anim, BOOL finished);

/**
正在做动画的时候调用;调用次数比较多
*/
@property (copy, nonatomic) void (^animationDidApplyBlock)(POPAnimation *anim);

/**
完成动画的时候是否删除动画;
默认为YES;
设置NO的话
*/
@property (assign, nonatomic) BOOL removedOnCompletion;

/**
动画是否已暂停;
在初始化的时候,默认YES;在动画添加的时候,隐式暂停???在动画完成的时候和     removedOnCompletion = NO的时候,动画是暂停的,
*/
@property (assign, nonatomic, getter = isPaused) BOOL paused;

/**
动画是否逆转;比如向前的动画,做完之后,会再后退回来;
注意:时间是原来的2倍,动画到toValue后,又回到原始的值;
delegete跟再做一次动画一样;

*/
@property (assign, nonatomic) BOOL autoreverses;

/**
重复动画次数;
= 0或者1不会重复;
注意:
delegete中
animationDidStart:每次动画重复开头调用;
animationDidReachToValue:每次到toValue的时候调用;
animationDidStop：finished：每次到toValue的时候调用,如果设置了autoreverses,动画还未完成,返回NO;
设置了autoreverses,动画时间是原来2倍;

*/
@property (assign, nonatomic) NSInteger repeatCount;

/**
一直重复做动画;
delegete中animationDidStop将恒等于NO;
*/
@property (assign, nonatomic) BOOL repeatForever;

@end


@protocol POPAnimationDelegate <NSObject>
@optional

/**
动画开始的时候调用
*/
- (void)pop_animationDidStart:(POPAnimation *)anim;

/**
动画达到toValue或者超过的时候调用;
*/
- (void)pop_animationDidReachToValue:(POPAnimation *)anim;

/**
动画停止
*/
- (void)pop_animationDidStop:(POPAnimation *)anim finished:(BOOL)finished;

/**
正在做动画的时候调用;
*/
- (void)pop_animationDidApply:(POPAnimation *)anim;

@end


@interface NSObject (POP)

/**
添加动画到接收器;
anim :要添加的动画
key:动画标识符,可以是任何字符串,但每个动画必须唯一;
*/
- (void)pop_addAnimation:(POPAnimation *)anim forKey:(NSString *)key;

/**
删除所有附件在接收器上的动画;
*/
- (void)pop_removeAllAnimations;

/**
删除附加在接收器上的所有关键
*/
- (void)pop_removeAnimationForKey:(NSString *)key;

/**
返回接收器所有动画的key的数组;key的顺序=动画顺序;
*/
- (NSArray *)pop_animationKeys;

/**
返回某个key的动画,=nil表示不存在
*/
- (id)pop_animationForKey:(NSString *)key;

@end

/**
实现NSCopying协议;
*/
@interface POPAnimation (NSCopying) <NSCopying>

@end
```

#二丶问题

###1.@property (assign, nonatomic) CFTimeInterval beginTime; 的使用;

我想要动画2秒后执行
```
POPBasicAnimation * butAnimation = [POPBasicAnimation animationWithPropertyNamed:kPOPViewCenter];
butAnimation.duration = 1.0f;
butAnimation.toValue = [NSValue valueWithCGSize:CGSizeMake(_btn.centerX,_btn.centerY + 400)];
butAnimation.beginTime = CACurrentMediaTime() + 2.0f;
[_btn pop_addAnimation:butAnimation forKey:@"btn_Animation"];
```

CACurrentMediaTime()  :
官方:

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/1986326-d0a29263664cd30c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
返回当前的绝对时间
```
其他阅读:
```
CACurrentMediaTime() 是基于内建时钟的，能够更精确更原子化地测量，
并且不会因为外部时间变化而变化（例如时区变化、夏时制、秒突变等）,
但它和系统的uptime有关,系统重启后CACurrentMediaTime()会被重置。
```
借鉴:https://cnbin.github.io/blog/2016/03/21/nsdate-,-cfabsolutetimegetcurrent,-cacurrentmediatime-de-chai-yi/


###2.@property (readonly, nonatomic) POPAnimationTracer *tracer; 的使用;
作用:辅助单元测试和debug;
可以看下[ POPAnimationTracer ] 这个类的api;挺简单;
比如- (void)start
```
- (void)start
{
POPAnimationState *s = POPAnimationGetState(_animation);
s->tracing = true;
}
```
去看tracing;会定位到

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/1986326-b08f33fc4809cab8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
跟踪的开始;
默认是tracing(false);
再全局搜索下tracing;

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/1986326-4420240280278752.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

跟动画delegete,和startblock的回调位置一样,功能一样;

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
