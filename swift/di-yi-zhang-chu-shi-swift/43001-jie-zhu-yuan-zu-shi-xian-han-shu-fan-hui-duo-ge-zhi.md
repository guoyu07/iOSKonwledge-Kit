### 借助元组让函数返回多个值

```
import UIKit

func maxMinFun(array:[Int])->(minNum:Int,maxNum:Int){
 var currentMin = array[0]
 var currentMax = array[0]
 for i in array{
 currentMin = min(i,currentMin)
 currentMax = max(i,currentMax)
 }
 return (currentMin,currentMax)
}

let testArray = [1,2,3,92,0,2933,221,73]
let result = maxMinFun(array: testArray)
print("the max is \(result.maxNum)")
print("the min is \(result.minNum)")
```

### 同样不一定要给元组各个参数命名

```
func maxMinFun2(array:[Int])->(Int,Int)?{
 if array.isEmpty {
 return nil
 }

 var currentMin = array[0]
 var currentMax = array[0]
 for i in array{
 currentMin = min(i,currentMin)
 currentMax = max(i,currentMax)
 }
 return (currentMin,currentMax)
}


var testArray1:[Int]? = [1,2,3,92,0,2933,221,73]
testArray1 = testArray1 ?? []
if let result1 = maxMinFun2(array: testArray1!){
 print("the max is \(result1.0)")
 print("the min is \(result1.1)")
}
```



