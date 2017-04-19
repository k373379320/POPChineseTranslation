#一丶代码:
```


/**
描述动画属性
*/
@interface POPAnimatableProperty : NSObject <NSCopying, NSMutableCopying>

/**
根据 名字 创建 动画属性,名字不存在=nil;
*/
+ (id)propertyWithName:(NSString *)name;

/**
根据 名字 创建 动画属性,名字不存在=nil; 如果名字存在,则初始化block实例;
*/
+ (id)propertyWithName:(NSString *)name initializer:(void (^)(POPMutableAnimatableProperty *prop))block;

/**
属性的名字,标识唯一动画属性
*/
@property (readonly, nonatomic, copy) NSString *name;

/**
返回当前属性值
*/
@property (readonly, nonatomic, copy) void (^readBlock)(id obj, CGFloat values[]);

/**
修改变化的值
*/
@property (readonly, nonatomic, copy) void (^writeBlock)(id obj, const CGFloat values[]);

/**
决定动画变化的间隔的阈(yu第四声)值;值越大,writeBlock的调用次数越少;
*/
@property (readonly, nonatomic, assign) CGFloat threshold;

@end

/**
可变动画可变属性;
*/
@interface POPMutableAnimatableProperty : POPAnimatableProperty

/**
属性的名称
*/
@property (readwrite, nonatomic, copy) NSString *name;

/**
返回当前属性值
*/
@property (readwrite, nonatomic, copy) void (^readBlock)(id obj, CGFloat values[]);

/**
修改变化的值
*/
@property (readwrite, nonatomic, copy) void (^writeBlock)(id obj, const CGFloat values[]);

/**
决定动画变化的间隔的阈(yu第四声)值;值越大,writeBlock的调用次数越少;
*/
@property (readwrite, nonatomic, assign) CGFloat threshold;

@end
```
#二丶使用

iOS_动画_POP_实例(一)_金额格式数字动画
http://www.jianshu.com/p/5d6ed65bdf06

#三丶其他:

翻译有问题,留言告诉我下,谢谢;
以及有使用问题也可以留言,一起探讨探讨;
