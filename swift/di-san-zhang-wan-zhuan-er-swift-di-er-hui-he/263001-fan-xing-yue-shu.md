```
import UIKit
```

```

protocol Priziable{
    func isPriziable()->Bool
}

struct Student:CustomStringConvertible,Equatable,Comparable,Priziable{
    var name:String
    var score:Int
    var description: String{
        return name + "Socre:" + String(score)
    }
    func isPriziable() -> Bool {
        return score >= 60
    }
}

func ==(s1:Student,s2:Student)->Bool{
    return s1.score == s2.score
}
func <(s1:Student,s2:Student)->Bool{
    return s1.score < s2.score
}

let a = Student(name: "Alice", score: 80)
let b = Student(name: "Bob", score: 92)
let c = Student(name: "Karl", score: 85)
let geek = Student(name: "geek", score: 100)
let students = [a,b,c,geek]

//Self表示自己所属的类型
func topOne<T:Comparable>(seq:[T])->T{
    assert(seq.count > 0)
    return max(seq[0], seq[1])
}
```



