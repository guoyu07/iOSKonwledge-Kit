# Protocol（二）

* 类是单继承，但是协议可以多遵循。1个类只有1个父类，一个类可以同时遵循多个协议

```
@interface 类名:父类名<协议名称>

@end
```

* 当一个类遵循了多个协议之后，就相当于该类拥有了这些协议中所有方法的声明
* 协议中如果需要让遵循该协议的类都实现方法，那么这些方法就用@optional修饰，如果不是强制该类实现这些方法那么就用@optional修饰，即使不实现编译器也不会报警告
* 协议继承的声明

```
@protocol 本协议名称<父协议名称>
//方法、属性
@end
```

#### 例子

```
//StudyProtocol.h
#import <Foundation/Foundation.h>

@protocol StudyProtocol <NSObject>

@property (nonatomic, assign) NSInteger age;

@property (nonatomic, strong) NSString *name;

-(void)read;

-(void)scan;

@optional
-(void)see;

@end

//DevelopProtocol.h
#import <Foundation/Foundation.h>
#import "StudyProtocol.h"

@protocol DevelopProtocol<StudyProtocol>

@required
-(void)learnObjectiveC;
-(void)learnSwift;

@optional
-(void)developApp;

@end

//Person.h
#import <Foundation/Foundation.h>
#import "DevelopProtocol.h"

@interface Person : NSObject<DevelopProtocol>


@end

//Person.m
#import "Person.h"


@interface Person (){
    NSString *_name;
    NSInteger _age;
}

@property (nonatomic, strong) NSString *sports;
@end

@implementation Person
-(void)setName:(NSString *)name{
    if (_name != name) {
        _name = name;
    }
}

-(NSString *)name{
    return _name;
}

-(void)setAge:(NSInteger)age{
    if (_age != age) {
        _age = age;
    }
}

-(NSInteger)age{
    return _age;
}


-(void)scan{
    NSLog(@"我在阅读");
}

-(void)read{
   NSLog(@"我在读书");
}

-(void)learnObjectiveC{
    NSLog(@"学习OC");
}

-(void)learnSwift{
    NSLog(@"学习Swift");
}

-(void)developApp{
    NSLog(@"练习开发App");
}

@end
```

#### 注意

* 在声明StudyProtocol协议中，再协议的后面&lt;NSObject&gt;,那么这个代表什么？
* 在Foundation框架中，有1个类叫做NSObject，是所有类的基类
* 在Foundation框架中，有1个协议叫做NSObject
* NSObject协议被NSObject类所遵守，所以NSObject协议中的所有方法被全部的OC类所拥有
* 这么说，所有的OC类都遵循了NSObject协议，NSObject协议叫做基协议
* 类的名称可以和协议的名称一致
* 写协议的规范，所有的协议必须直接或者间接地遵循NSObject基协议中继承



