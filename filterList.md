Filter a list
=============
过滤操作是一种工作中常用的集合操作。这种操作实在是太典型了，我要用这个例子来展示各种编程的做法。举个例子，我要在一个整数list里面过滤掉小于0的数。

1. 循环过滤
听上去这种做法很简单，很直观：
```java
List<Integer> filtered = new ArrayList<>();
List<Integer> toFilter = Arrays.asList(1, -3, 9, 0);
for(Integer i : toFilter) {
  if(i > 0)
    filtered.add(i);
}
```
经过这个循环，filtered就成了`[1, 9]`。很简单！

2. Java8 stream
如果你用Java8来做，就多了functional programming的味道：
```java
List<Integer> toFilter = Arrays.asList(1, -3, 9, 0);
List<Integer> filtered = toFilter.stream()
  .filter((i) -> i > 2)
  .collect(Collectors.toList());
```
.filter函数直击问题核心，它的参数是个lambda表达式：
`Predicate<Integer> p = (Integer i) -> i > 2;`
lambda表达式简单明了地表达了逻辑意图。