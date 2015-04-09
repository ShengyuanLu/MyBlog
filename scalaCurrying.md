# Scala之柯里化(currying)

Scala的柯里化就是能定义和使用*多个参数*的函数。
好比用Java来写：
```java
String concat(String s1)(String s2) {
  return s1 + s2;  
}
```
当然Java是不支持这种语法的。那么我们来看看Scala怎么做的，同样是用concat函数来连接两个String：
```scala
def concat(s1: String)(s2: String):String = {
  s1 + s2
}
val s3 = concat("A")("B") //s3等于"AB"
```

