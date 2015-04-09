
## 强悍的类型推断 (Type Inference)
看下面这个最简单的赋值语句：
```scala
var x = "foo" // x is type of String
```
看似好像动态语言，编译的时候没有类型。但其实编译器已从等号的右边的"foo"，推断出x是`String`类型。所以，当你再试图给`x`赋其他类型的值的时候，编译就是失败了。
```scala
x = 12 //Fail, type mismatch!
```

## 表达式优先与语句
