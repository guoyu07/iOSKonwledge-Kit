### typealias类型别名

通过为已经存在的类型重新定义新的名字，通过命名使得代码变得更清晰，使用的语法像普通的赋值语句一样。还可以用来声明Block。

```
typealias sendBlock = (_ par:String)->Void
var call:sendBlock
call = {_ in 
    print("world")
}
call("hello")
```

```
typealias Length = Double
extension Double{
    // 转换成米
    var km:Length{ return self*1000.0 }
    var m:Length{ return self  }
    var cm:Length { return self/100 }
    var ft:Length{ return self/3.28084 }
}

let runningDistance:Length = 3.74.km
runningDistance


//可称重接口。单位可变
protocol WeightCalculabe{
    associatedtype WeightType
    var weight:WeightType{ get }
}

class iPhone7:WeightCalculabe{
    typealias WeightType = Double
    var weight: Double{
        return 0.114
    }
}


class Ship:WeightCalculabe{
   typealias WeightType = Int
    let weight: WeightType
    init(weight:Int) {
        self.weight = weight
    }
}


extension Int{
    typealias Weight = Int
    var t:Weight{
        return 1_000 * self
    }

}
let titanic = Ship(weight: 46_328.t)
```



