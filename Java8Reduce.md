## Java8 Stream.reduce方法详解 (Java8 Stream.reduce)
reduce是把元素做迭代运算，最后返回**一个**值的计算。它又3个重载版本：

###  `Optional reduce(BinaryOperator accumulator)`
举个例子，我们对1, 3, 6做合计操作：
```java
int sum = Stream.of(1, 3, 6).reduce((left, right) -> left + right).get();  //1+3+6=10
```
这个操作可以看作：
```java
BinaryOperator<Integer> accumulator = (left, right) -> left + right;
int sum = accumulator.apply(accumulator.apply(1, 3),6);
```
注意这个方法返回的是一个`Optional`的类型。如果是个空stream，那么reduce出来是个`Optional.empty()`。

### `T reduce(T identity, BinaryOperator<T> accumulator)`
还是累加的例子，这次要以100为初始值做累加，最后结果是110。
```java
int sum = Stream.of(1, 3, 6).reduce(100, (left, right) -> left + right);  
```
这个操作可以看作：
```java
BinaryOperator<Integer> op = (left, right) -> left + right; 
int sum= op.apply(op.apply(op.apply(100, 1), 3), 6);
```

### `<U> U reduce(U identity, BiFunction<U, ? super T, U> accumulator, BinaryOperator<U> combiner)`
它被用在**并行stream**上面，如果用在串行stream上，那么那个combiner是不会被用到的。举个例子，我们要把每个stream里面的元素乘以2，然后求和：
```java
BiFunction<Integer, Integer, Integer> accumulator = (identity, e) -> identity * e;
BinaryOperator<Integer> combiner = (left, right) -> left + right;
int r = Stream.of(1, 3, 6)
  .parallel()
  .reduce(2, accumulator, combiner); //2*1 + 2*3 + 2*6 = 20
```
accumulator的作用是在多线程上做累计计算，在这个例子里面就是做`2*元素`的计算。
combiner的作用是把多个accumulator的结果做合并，在这个例子里面就是做加法。
上面的那段代码就可以被看作，有多个线程并行计算：

Thread1: `accumulator.apply(2, 1) = 2`

Thread2: `accumulator.apply(2, 3) = 6`

Thread3: `accumulator.apply(2, 6) = 12`

假设Thread1，Thread2先做完乘法，这个时候不等Thread3做`accumulator.apply(2, 6)`，可以先做Thread1，Thread2结果的合并加法：`combiner.apply(2, 6) = 8`。
此时Thread3做完2*6的计算，就可以做最后的合并：把刚才combiner得到的8加上accumulator得到的12，即8+12=20。
因此在整个计算过程中，accumulator和combiner是犬牙交错，没有一定顺序的。

算法的核心在于，accumulator和combiner的解耦合。两者互相不依赖，所以能做并行处理。
