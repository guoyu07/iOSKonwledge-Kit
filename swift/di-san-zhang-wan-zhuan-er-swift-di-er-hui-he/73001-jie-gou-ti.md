### 结构体

```
1、结构体的构造函数（默认构造函数和自定义构造函数）
```

```
 import UIKit 
//结构体
struct Location{
 let longitude:Double
 let latitude:Double
 var placeName:String?

 //默认构造函数
 //Failable-Initalizer
 //默认使用构造函数时，参数是不可省略的。如果想省略此参数名，则在参数名前加_
 //对于结构体和类来说，建议给出一个带有全参数的构造函数。
 init(_ coordinateString:String) {
 let commaIndex = coordinateString.range(of: ",")!.lowerBound
 let firstElement = coordinateString.substring(to: commaIndex)
 var secondElement = coordinateString.substring(from: commaIndex)
 secondElement = secondElement.substring(from: coordinateString.index(coordinateString.startIndex, offsetBy: 1))
 longitude = Double(firstElement)!
 latitude = Double(secondElement)!
 }

 init(longitude:Double,latitude:Double) {
 self.longitude = longitude
 self.latitude = latitude
 }
}

//let location:Location = Location(coordinateString: "12,22")
var location2:Location = Location(longitude:22,latitude:22)
location2.placeName = "杭州"
location2
let location3:Location = Location("23.2,34.2")

//var HZLocation:Location = Location(longitude: 12,latitude: 22)
```

```
2、可失败的构造函数
```

```
import UIKit

struct Location{
 let longitude:Double

 //默认构造函数
 //Failable-Initalizer
 //默认使用构造函数时，参数是不可省略的。如果想省略此参数名，则在参数名前加_：---> init(_ coordinateString:String) {
 //对于结构体和类来说，建议给出一个带有全参数的构造函数。
 init?(coordinateString:String) {
 //解包：？尝试解包，！强制解包：可能奔溃

     if let commaIndex = coordinateString.range(of: ",")?.lowerBound{
         if let firstElement = Double(coordinateString.substring(to: commaIndex)){
             self.longitude = firstElement
         }else{
             return nil
         }
     }else{
         return nil
     }
 }
 init(longitude:Double) {
     self.longitude = longitude
 }
}

//let location:Location = Location(coordinateString: "12,22")
var location2:Location = Location(longitude:22)

let location3 = Location(coordinateString:"12,22")
let location4 = Location(coordinateString: "12122")
let location5:Location? = Location(coordinateString: "12122")
```

```
     ->改进（if let x = expression）,if太多可读性太差
```

```
import UIKit


struct Location{
 let longitude:Double

 //默认构造函数
 //Failable-Initalizer
 //默认使用构造函数时，参数是不可省略的。如果想省略此参数名，则在参数名前加_：---> init(_ coordinateString:String) {
 //对于结构体和类来说，建议给出一个带有全参数的构造函数。
 init?(coordinateString:String) {
 //解包：？尝试解包，！强制解包：可能奔溃

 guard let commaIndex = coordinateString.range(of: ",")?.lowerBound else{
     return nil
 }

 guard let firstElement = Double(coordinateString.substring(to: commaIndex)) else {
    return nil
 }

 self.longitude = firstElement

 }

 init(longitude:Double) {
     self.longitude = longitude
 }
}

let location:Location? = Location(coordinateString: "12,22")
var location2:Location = Location(longitude:22)
let location3 = Location(coordinateString:"12,22")
let location4 = Location(coordinateString: "12122")
```



