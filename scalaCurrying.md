# Scala之柯里化(currying)

Scala的柯里化就是能定义和使用*多个参数*的函数。
好比用Java来写：
```java
String concat(String a)(String b) {
  return a + b;  
}
```
当然Java是不支持这种语法的。那么我们来看看Scala怎么做的，同样是用`concat`函数来连接两个String：
```scala
def concat(a: String)(b: String):String = {
  a + b
}
val s = concat("A")("B") //s等于"AB"
```
Scala是把这个`concat`拆成两个函数，传入第一个参数a后，返回一个新函数。这个新函数的参数是b。看起来是这样：
```scala
def concat1(a: String) = {
  (b: String) => a + b
}
  
val concat2 = concat1("A")
val s = concat2("B")
```
