### 类型属性

```
 Int.max、Int.min像这样，max和min是Int这个结构体的类型属性，它不是int的实例的属性。类型属性用static修饰，在最外层的花括号内。
```

```
class Player{
 var name:String
 var score:UInt32 = 0
 static var historyScore:UInt32 = 0
 init(name:String) {
 self.name = name
 }


 func play() {
 let score = arc4random()%100
 print("\(self.name) played and got \(score)")
 self.score += score
 print("total score of \(name) is \(self.score)")
 if self.score > Player.historyScore {
 Player.historyScore = self.score
 }
 print("the higest score of the game is \(Player.historyScore)")
 }
}

var player1 = Player(name: "liubinpeng")
player1.name
player1.play()
player1.play()
print("\n")
var player2 = Player(name: "zhangyu")
player2.name
player2.play()
player2.play()
```

```
类型方法:和具体某个对象无关，而是和某个类型有关，这样的方法应该被声明为类型方法。距离：一个矩阵的结构体，可以有1个矩阵对象，声明一个方法：作用是传入一个参数，生成一个单位矩阵。想想看，这样的方法跟某个矩阵没关系，而根矩阵这个类型有关，因此可以将这个方法声明为类型方法。
```

```
import UIKit
struct Matrix{
 var m:[[Int]]
 var row:Int
 var col:Int

 init?(_ arr2d:[[Int]]) {
 guard arr2d.count>0 else {
 return nil
 }

 let row = arr2d.count
 let col = arr2d[0].count

 for i in 1..<row{
 if arr2d[i].count != row{
 return nil
 }
 }

 self.m = arr2d
 self.row = row
 self.col = col
 }

 func printMatrix() -> Void{
 for i in 0..<row{
 for j in 0..<col{
 print(m[i][j],terminator:"\t")
 }
 print()
 }
 }

 static func identityMatrix(n:Int) -> Matrix?{
 guard n>0 else {
 return nil
 }

 var arr2d:[[Int]] = []
 for i in 0..<n{
 var row = [Int](repeating:0,count:n)
 row[i] = 1
 arr2d.append(row)
 }
 return Matrix(arr2d)
 }
}


if let m = Matrix([[1,2],[3,4]]) {
 m.printMatrix()
}

if let e = Matrix.identityMatrix(n: 3){
 e.printMatrix()
}
```



