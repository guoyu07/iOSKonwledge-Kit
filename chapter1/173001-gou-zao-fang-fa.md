# 构造方法

* new方法的内部就是先调用alloc方法，再调用init方法

  * alloc方法：那个类接受alloc消息，那么该方法返回该接受类的对象，并把对象返回

  * init方法：是1个对象方法，作用：初始化对象

* 创建对象的步骤：先使用alloc创建1个对象，再使用init初始化这个对象，才可以使用这个对象

  * 使用1个未被初始化的对象是很危险的

* init方法：作用：初始化对象，为对象赋初始值，叫做构造方法

# 重写init构造方法

* 如果想创建出来的对象的属性值不是默认的初始化值，则需要重写init方法

* 重写init方法的规范：

  * 必须要先调用父类的init方法（因为当前类初始化就是通过\`\[父类init\]\`去初始化），然后将返回值赋值给self

  * 调用init方法有可能会失败，如果失败直接返回nil

  * 判断父类是否初始化成功。如果self != nil，则代表初始化成功

  * 如果初始化成功就去初始化当前对象的属性

  * 最后返回self

#### 解惑：

1. 为什么要调用父类的init方法？
   1. 当前类有isa指针，当前类的isa指针赋值是通过父类的init方法赋值的。
   2. 需要保证当前对象的父类属性同时被初始化
2. 重写init方法的规范：

```
-(instancetype)init{
    if (self = [super init]) {
        //todo：自定义属性的初始化
    }
    return self;
}
```

```
//Person

#import <Foundation/Foundation.h>

@interface Person : NSObject
@property NSString* name;
@property int age;

-(void)sayHi;

@end

#import "Person.h"
@implementation Person

-(void)sayHi{
    NSLog(@"Hi");
}

-(instancetype)init{
    self = [super init];
    if (self) {
        self.name = @"杭城小刘";
        self.age = 22;
    }
    return self;
}
@end


//测试

 Person *p1 = [[Person alloc] init];    //p1.name = "杭城小刘"，p1.age =22;
 Person *p2 = [Person new];             //p2.name = "杭城小刘"，p2.age =22;
```

如果2个类的关系为
