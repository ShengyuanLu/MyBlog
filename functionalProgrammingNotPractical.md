
# 函数式编程不实用 Functional Programming Not Practical
虽然函数式编程这几年火热流行，但是我认为**函数式编程只能作为OO的辅助**。

OO才是改变编程理念，极大提高生产率的变革。OO解决的是编程中最普遍的建模的思路，符合人的思维习惯。函数式编程不是。函数式编程是在局部使得代码更紧凑，更有表现力（譬如Java8的lambda表达式）。所以，我认为纯函数式的语言基本不实用。而像**Scala这样OO + FP这样的混合编程模式才在工业界比较实用**。Scala的主页写着：*Object-Oriented Meets Functional*。你可以使用OO，同时也可以使用FP，这就有了自由。

函数式的确有很多好处，immutable，没有side effect，lazy evaluation。以及各种函数编程技法：偏函数，柯里化等等。但是，它们的确需要更多的编程技巧。
我相信，对大多数程序员来说，函数式普遍应用的递归的写法就是比较困难的。举个例子，要实现一个数组反转。如果用命令式的显式循环做法，基本上是毫无难度。但是要用递归来实现，那就费劲了。再者，像递归和immutable对计算机来说也是低效率的。很多Scala库的内部实现，仍旧采用非函数式的实现。

## “Elegance and familiarity are orthogonal” － Rich Hickey
正如函数式语言Clojure的发明者所说的编程哲学：*Elegance and familiarity are orthogonal* 。即优雅和熟悉是正交的。换言之，程序的优雅和简易性是不相关的。它的潜台词就是：我要的就是程序的优雅，容不容易学是另一码事。

拿Java来说，它的一大优势就在于它在工业界的易用性。但是它的优雅性就被万夫所指了。（被大家噴得比较多的就是缺乏表现力。具体说，就是其他语言两三行实现的功能，Java要写上一堆代码才行）

但是现实世界里，到底有多少程序员和老板对编程语言优雅性有要求？出货时间有限，先实现了再说！这就是现实的世界，简单好用为王。
Java8 lambda表达式的出现缓解了一些Java优雅性的问题。当然lambda表达式对Java的简易性来说是变得不那么简单了。但是，我还是认为lambda表达式是巨大的进步！说到底，就算你用不来`stream`和`->`，你还是可以用循环啊，它只是多了一种编程的选择。

## Functional Programming Myth
很多业界名人推崇LISP，包括Paul Graham一直是函数式语言LISP的推崇者。所以啊，这些大牛都推崇备至的语言，普罗大众谁敢轻易否定？问题在于他们的观点是LISP是**最好**的语言，而不是**最实用**的语言。当然，他们推崇LISP不光是因为它是函数式编程语言，LISP还是有像同相性（homoiconicity）这样厉害的特性。

在公司里用纯函数编程语言，有这几个问题需要回答：
 - 人才市场上会纯函数编程语言的人容易招聘吗？
 - 纯函数编程语言的IDE好用吗？也许这些大神们都用记事本写代码。。。呵呵
 - 纯函数编程语言的生态系统如何？工具和第三方包足够吗？

但凡这些纯函数式编程语言，在业界都没有很好的市场。倒不是拉黑这些语言，我只是说它们不实用。但是它们的学习价值相当高，学习它们会使人的编程能力跃上一个新的台阶。

《大教堂与市集》的作者Eric Raymond也表达过类似的观点:
> Lisp is worth learning for the profound enlightenment experience you will have when you finally get it; that experience will make you a better programmer for the rest of your days, even if you never actually use Lisp itself a lot.
