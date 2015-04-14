## Java8高阶Stream方法 (Java8 stream higher functions)

Java8提供了Stream的高阶方法。所谓高阶方法，就是接受参数为lambda表达式的方法。
譬如，有个整型的集合`Collection<Integer>` col，这个col可能是个`List`，也可能是个`Set`，或是其它的类型。假设这个col里面有5个元素{2, 3, 4, 5, -1}：
```java
Collection<Integer> col = ... //2, 3, 4, 5, -1
Stream<Integer> stream  = col.stream();         //串行单线程stream
Stream<Integer> pStream = col.parallelStream(); //并行多线程stream
```

- anyMatch
```java
stream.anyMatch(i -> i > 4); //返回true，因为有个5。
```

- allMatch
```java
stream.allMatch(i -> i < 6); //返回true，因为所有元素小于6。
```

- forEach
```java
stream.forEach(i -> System.out.println(i)); //打印2, 3, 4, 5, -1
```

- forEachOrdered
```java
//即使使用多线程，仍保证打印顺序2, 3, 4, 5, -1
pStream.forEachOrdered(i -> System.out.println(i)); 

//对比forEach，对比forEach在使用多线程下，不能保证打印顺序：2, 3, 4, 5, -1
pStream.forEach(i -> System.out.println(i)); 
```
- map
```java
stream.map(e -> e * 2).collect(Collectors.toList())); //返回4, 6, 8, 10, -2
```

- reduce
reduce是把元素做迭代运算，最后返回**一个**值的计算。
```java
int r = Stream.of(1, 3, 6).reduce((left, right) -> left + right).get();  //1+3+6=10
```
这个操作可以看作：
```java
BinaryOperator<Integer> accumulator = (left, right) -> left + right;
int r = accumulator.apply(accumulator.apply(1, 3),6);
```

reduce还有其他两个重载的版本：
一个是：`T reduce(T identity, BinaryOperator<T> accumulator)`
举个例子：譬如有一个元素为1，3，6的stream，要以100为初始值做累加，最后结果是110。
```java
int r = Stream.of(1, 3, 6).reduce(100, (left, right) -> left + right);  
```
这个操作可以看作：
```java
BinaryOperator<Integer> op = (left, right) -> left + right; 
int r = op.apply(op.apply(op.apply(100, 1), 3), 6);
```

另外一个是和多线程有关的：`<U> U reduce(U identity, BiFunction<U, ? super T, U> accumulator, BinaryOperator<U> combiner)`。
它被用在并行stream上面，如果用在串行stream上，那么那个combiner是不会被用到的。举个例子，我们要把每个stream里面的元素乘以2，然后求和：
```java
BiFunction<Integer, Integer, Integer> accumulator = (init, e) -> init * e;
BinaryOperator<Integer> combiner = (left, right) -> left + right;
int r = Stream.of(1, 3, 6)
  .parallel()
  .reduce(2, accumulator, combiner); //2*1 + 2*3 + 2*6 = 20
```
accumulator的作用是在多线程上做累计计算，在这个例子里面就是做`2*元素`的计算。
combiner的作用是把多个accumulator的结果做合并，在这个例子里面就是做加法。
