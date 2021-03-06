### 拓展

```
swift中的拓展类似oc中的Category
区别：pc类别还需要重命名；而swoft只需要Extension   
+需要拓展的对象 ｛
      func play（）｛

      ｝
//注意class为引用类型因此使用self.就可以改变值
//struct为值类型，要想改变struct中的成员必须在函数前加mutating修饰
｝

注意：Extension可以拓展属性和方法，但是不可以拓展存储属性，只可以拓展计算属性。
```

```
import UIKit

struct Point{
    var x = 0.0
    var y = 0.0
}
struct Size{
    var width = 0.0
    var heigt = 0.0
}
/*
struct Rectangle{
    var origin = Point()
    var size = Size()
    init(origin:Point,size:Size) {
        self.origin = origin
        self.size = size
    }
}

var rect1 = Rectangle(origin: Point(x: 0,y: 0), size: Size(width: 3, heigt: 4))
//拓展
extension Rectangle{
    mutating func translate(x:Double,y:Double){
        self.origin.x += x
        self.origin.y += y
    }
}
 */
class Rectangle{
    var origin = Point()
    var size = Size()
    init(origin:Point,size:Size) {
        self.origin = origin
        self.size = size
    }
}

//拓展
extension Rectangle{
     func translate(x:Double,y:Double){
        self.origin.x += x
        self.origin.y += y
    }
}

var rect1 = Rectangle(origin: Point(x: 0,y: 0), size: Size(width: 3, heigt: 4))
rect1.translate(x: 10, y: 10)

extension Rectangle{
    var center:Point {
        get{
            let x = origin.x + size.width/2
            let y = origin.y + size.heigt/2
            return Point(x: x, y: y)
        }

        set(newCenter){

            //origin.x = newCenter.x - size.width/2
            //origin.y = newCenter.y - size.heigt/2
            size.width = (newCenter.x - origin.x)*2
            size.heigt = (newCenter.y - origin.y)*2
        }
    }

    convenience init(center:Point,size:Size) {
        let originX = center.x - size.width/2
        let originY = center.y - size.heigt/2
        self.init(origin: Point(x: originX,y: originY),size:size)
    }
}
rect1
rect1.center
rect1.center = Point(x: 13, y: 13)
rect1

var rect2 = Rectangle(center: Point(x:15,y:15), size: Size(width: 10, heigt: 10))
rect2
```

```
import UIKit
//Nested Type

//extension

extension Int{
    var square:Int{
        get{
            return self * self
        }
    }

    var cube:Int{
        get{
            return self * self * self
        }
    }


    func inRange(closedLeft left:Int, openedRight :Int)->Bool{
        return self >= left && self < openedRight
    }

    func repetitions(tasks:()->Void) {
        for _ in 0..<self{
            tasks()
        }
    }
}

let num = 8
num * num
num.square

num * num * num
num.cube

let index = 12
index >= 0 && index < 20
index.inRange(closedLeft: 0, openedRight: 20)


var i = 0
for _ in 0..<20{
    i += 1
}
i

var j = 5
j.repetitions {
    print("task")
}

for m in stride(from: 0, through: 10, by: 3){
    print(m)
}

for n in stride(from: 0, through: 10, by: 2) {
    print(n)
}
```



