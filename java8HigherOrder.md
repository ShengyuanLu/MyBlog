## Java8高阶Stream方法 (Java8 stream higher functions)

Java8提供了Stream的高阶方法。所谓高阶方法，就是接受参数为lambda表达式的方法。
譬如，有个整型的集合`Collection<Integer>` col，这个col可能是个`List`，也可能是个`Set`，或是其它的类型。假设这个col里面有5个元素{2, 3, 4, 5, -1}：
```java
Collection<Integer> col = ... //2, 3, 4, 5, -1
Stream<Integer> stream = col.stream();
```

- anyMatch
```java
stream.anyMatch(i -> i > 4); //返回true，因为有个5。
```
