过滤List的4种做法（Filter a List with 4 ways）
=============
过滤操作是一种工作中常用的集合操作。这种操作实在是太典型了，我用这个例子来展示各种编程的做法。举个例子，我要在一个整数list里面过滤掉小于0的数。

## 做法1: 循环过滤
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

## 做法2: Java8 stream
如果你用Java8来做，就多了functional programming的味道：
```java
List<Integer> toFilter = Arrays.asList(1, -3, 9, 0);
List<Integer> filtered = toFilter.stream()
  .filter((i) -> i > 0)
  .collect(Collectors.toList());
```
`filter()`函数直击问题核心，它的参数是个lambda表达式：
`Predicate<Integer> p = (Integer i) -> i > 0;`
lambda表达式简单明了地表达了逻辑意图。 当然，它背后也是利用循环过滤的做法。
顺便说一下，如果用Scala做，会更加精简：
```scala
val filtered = toFilter.filter(_ > 0)
```

##  做法3: 延迟计算（Lazy Evaluation）
假设我拿到这个过滤之后的filtered，然后由于后续代码中的逻辑分支，filtered只被用了其中的一部分元素。那么之前对**所有元素的循环过滤操作就是浪费的**！
这个场景下，延迟计算就派上用场了。延迟计算也是来自于functional programming的一种做法。也就是用到的时候再进行计算。在我们这个例子里面，就是当过滤list真正被用的时候，再进行过滤操作。
```java
Iterable<Integer> filtered = new Iterable<Integer>() {
  @Override
  public Iterator<Integer> iterator() {
  
    return new Iterator<Integer>() {
      Iterator<Integer> it = toFilter.iterator();
      Integer i;
      
      @Override
      public boolean hasNext() {
        while(it.hasNext()) {
          i = it.next();
          if(i > 0) { //Evaluate at lazy
            return true;
          }
        }
        return false;
      }
      
      @Override
      public Integer next() {
        return i;
      }
    };
  }
};
```
是不是有点复杂？那么我们再写一段测试代码：
```java
for(Integer i : filtered)
  System.out.println(i);
```
然后再打些断点。你会发现当返回这个filtered的时候，没有任何过滤的操作。只有当for循环的时候才会产生判断操作。这就是延迟计算。
  
##  做法4: 递归计算（Recursive）
递归也是functional programming的一个经典思路。利用递归做法，代码会非常精简。不过由于递归调用会使得调用栈变深，在数组长度太大的时候，会stack overflow。
用Scala代码作：
```scala
def filter(toFilter: List[Int]): List[Int] = {
  toFilter match {
    case List() => List()
    case first::tail => if(first > 0) first :: filter(tail)
                    else filter(toFilter.tail)
  }
}
```
不是因为Java代码不能作，而是用Java实现这段逻辑会有点麻烦。
下面几乎与Scala等价的代码：
```scala
List<Integer> filter(List<Integer> toFilter) {
  if (toFilter.isEmpty()) {
    return toFilter;
  }
  
  Integer first = toFilter.get(0);
  List<Integer> tail = toFilter.subList(1, toFilter.size());
  if (first > 0) {
    List<Integer> result = new ArrayList<>();
    result.add(first);
    result.addAll(filter(tail)); //Recursive
    return result;
    
  } else {
    return filter(tail); //Recursive
  }
}
```
