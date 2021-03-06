### 函数内部、外部参数

```
import UIKit
//内部参数名
func showMessage(username:String,msg:NSString)->(){
    print("\(msg),\(username)")
}
showMessage(username: "lbp", msg: "Good evening")
//外部参数名
func showMessage1(Username username:String,Message msg:NSString)->(){
 print("\(msg),\(username)")
}
showMessage1(Username: "昔年", Message: "晚上好")

//#修饰的参数，既是内部参数名也是外部参数名
func showMessage3(#username:String,#message:String)->(){
 print("\(msg),\(username)")
}
showMessage3(username: "lbp", msg: "Good evening")/
```

### 默认

```objective-c
//内部参数名
//swift给带有默认值的参数必须要用外部参数名，为了给调用者知道这个默认参数是什么意思
func showMessage(username:String,msg:NSString = "hello", other:String = "How are you?")->(){
 print("\(msg),\(username),\(other)")
}
showMessage(username: "lbp", msg: "Good evening")
showMessage(username: "昔年")
showMessage(username: "刘斌鹏", other:"学习swift加油")
```

### 可变参数

```ojective-c
//可变参数
//一个函数只可以有一个可变参数且必须放在最后一个参数的位置。
func add(a:Int,b:Int, others:Int ...)->Int{
 var sum = a + b
 for element in others{
 sum += element
 }
 return sum
}
add(a: 1, b: 2)
add(a: 2, b: 3, others: 2,3,4)
```

### inout修饰函数参数

```objectiive-c
//inout类型的参数,在函数内部对其改变在外部也会改变其值。
//swift中默认函数传入的参数是对其值复制一个，所以函数内部对值改变在外部不影响结果
//有时需要对参数改变，需要在参数钱加inout修饰，并且在调用的时候参数要加地址引用符号“&”

func swapTwoInts( a:inout Int, b:inout Int)->(Int,Int){
 let t = a
 a = b
 b = t
 return (a , b)
}

var a = 100, b = 10
a
b
swapTwoInts(a: &a, b: &b)
a
b
```

### 函数的闭包

```objective-c
//函数闭包写法
var aray:[Int] = [1,3,5,65,2,34543,334,24,67]
aray.sorted(by: {(a:Int,b:Int)->Bool in
 return a>b
})
aray

aray.sort(by:{(a,b)->Bool in return a > b })
aray
aray.sorted(by: >)
aray
//函数闭包写法
var aray:[Int] = [1,3,5,65,2,34543,334,24,67]
aray.sorted(by: {(a:Int,b:Int)->Bool in
 return a>b
})
aray

aray.sort(by:{(a,b)->Bool in return a > b })
aray

aray.sorted(by: >)
aray
```

### 结尾闭包

```
//结尾闭包(trailling closure)---使得调用者看闭包看起来很明了
var array:[String] = ["d","cd","abcd","a","b"]
sorted(array, {($1,$2) in
 if countElements($1) != countElements($2){
 return countElements($1)<countElements($2)
 }
 return $1<$2
})
//trailling closure
array = sorted(array) {($1,$2) in
 if countElements($1) != countElements($2){
 return countElements($1)<countElements($2)
 }
 return $1<$2
}
array
```

### capturing value

```
闭包会智能地去查找函数的变量，如果内部找不到就去外部查找变量的值
```

```
//结尾闭包(trailling closure)
var array:[Int] = [1,2334,3543,31,45,2,0]
array.sort(){
 //计算整形数据到5的距离
 return fabs(Float($0-5))<fabs(Float($1-5))
}
array

//新的需求：需要由用户决定计算到几的距离--->capturing value
var num = 3
array.sort(){
 return fabs(Float($0-num))<fabs(Float($1-num))
}
array
```



