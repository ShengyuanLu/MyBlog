# Scala日记

## 强悍的类型推断 (Type Inference)
看下面这个最简单的赋值语句：
```scala
var x = "foo" // x是String类型
```
看似好像动态语言，编译的时候没有类型。但其实编译器已从等号的右边的"foo"，推断出x是`String`类型。所以，当你再试图给`x`赋其他类型的值的时候，编译就是失败了。
```scala
x = 12 //编译失败，x不能赋值Integer
```
再看下面这个数组遍历的例子。如果要用for循环遍历一个Integer型的List，你不需要像Java那样写成：
```java
List<Integer> list = ...
for (Integer e : list) //你必须再次声明e是个Integer，尽管在定义list的时候已经声明过了
```
而是忽略声明Integer，直接写成：
```scala
val list : List[Integer] = ...
for (e <- list) //无需再次声明e的类型，它已经被推测出来是Integer了
```
## 表达式优先与语句
在Scala里面，if语句是有返回值的，所以你可以这样写：
```scala
val x = if (1 < 2) "yes" else "no"
```
看起来很像Java里的三元表达式：
```java
String x = (1 < 2) ? "yes" : "no";
```
但是Scala在if语句里面还能夹其它的操作：
```scala
val x = if ({println("hi")  //判断之前还能加其他的操作
             1 < 2 }) "yes" 
        else "no"
```
其实尽量把各种语言控制做成有返回值也是functional programming的做法。
