### 闭包捕获列表

```
weak和unowned用于修饰类。使用引用类型是对指针的拷贝，因此容易造成野指针或者内存泄漏；值类型是对值的拷贝，在使用完后是销毁掉了。不会造成内存泄漏。
闭包也是引用类型，因此在闭包里面使用self的话要加闭包捕获列表。[]。方括号里面加容易捕获到的对象。
```

    import UIKit
    class SmartAirConditioner{
        var temperature:Int = 26
        //weak和unowned用于类
        var temperatureChange:((Int)->Void)!
        init() {
            print("The airconditioner is initialized")
            temperatureChange = { [weak self] newRemperature in
                if let `self` = self {
                    if abs(newRemperature - self.temperature) >= 10 {
                        print("It is not healthy to do it!")
                    }else{
                        self.temperature = newRemperature
                        print("New temperature \(self.temperature) is set!")
                    }
                }
            }
        }

        deinit {
            print("The airconditioner is deinitialized")
        }
    }

    var airConditioner:SmartAirConditioner? = SmartAirConditioner()
    airConditioner?.temperatureChange(10)
    airConditioner = nil

    import UIKit
    class SmartAirConditioner{
        var temperature:Int = 26
        //weak和unowned用于类
        var temperatureChange:((Int)->Void)!
        init() {
            print("The airconditioner is initialized")
            temperatureChange = { [weak self] newRemperature in
                //解包
    //            if let `self` = self {
                if let weakSelf = self {
                if abs(newRemperature - weakSelf.temperature) >= 10 {
                        print("It is not healthy to do it!")
                    }else{
                        weakSelf.temperature = newRemperature
                        print("New temperature \(weakSelf.temperature) is set!")
                    }
                }
            }
        }

        deinit {
            print("The airconditioner is deinitialized")
        }
    }

    var airConditioner:SmartAirConditioner? = SmartAirConditioner()
    airConditioner?.temperatureChange(10)
    airConditioner = nil



