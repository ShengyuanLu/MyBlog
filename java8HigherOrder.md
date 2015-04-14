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
