### 范型

范型:用&lt;&gt;修饰，里面的名称可以自定义。但是标准的是T

```
import UIKit

//Generic-范型

func swapTwoInt( _ a:inout Int, _ b :inout Int){
    (a,b) = (b,a)
}

func swapTwoDouble(a:inout Double, b:inout Double){
    (a,b) = (b,a)
}

//范型:用<>修饰，里面的名称可以自定义。但是标准的是T
func swapTwoThings<Thing>(a:inout Thing,b:inout Thing){
    (a,b) = (b,a)
}
func swapTwoElement<T>(a: inout T,b:inout T){
    (a,b) = (b,a)
}

var a = 11
var b = 22
swapTwoInt(&a, &b)
a
b

var m = 1.2
var n = 3.2
swapTwoDouble(a: &m, b: &n)
m
n


var left = "oc"
var right = "swift"
swapTwoThings(a: &left, b: &right)

left
right

swapTwoElement(a: &left, b: &right)
left
right
```



