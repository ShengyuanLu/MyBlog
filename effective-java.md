## Effective Java书评

Effective Java是本价值极高的书。如果有人要我推荐一本Java书，我会毫不犹豫推荐它。

它不是一本普通的Java语言的书，虽然全篇都在说Java。但它道出了涉及了很多跨语言的**普遍编程的理念**。我认为每个职业Java工程师都应该读一读这本书。即使你以后用其他编程语言的时候，它仍旧极具参考价值。

### Joshua Bloch
先说作者Joshua Bloch，他是JDK collection API的作者。也就是说，你每天用的`ArrayList`，`HashMap`都是他写的。Effective Java中的那些条目都应用在了这些Java JDK类库的编写上了。说得通俗一点，他是“干活”的。所以，这样出自一线编码大师的书中都是相当实用的建议。

### 更好地写代码
Effective Java不是教你怎么写Java，而是让你怎么**更好地写Java**（以及其他编程语言）。我知道大家都看过Think in Java，这是本好书。就是我说的，它是教你怎么写Java。而读Effective Java的前提是你已经比较了解Java语言了，你希望能写得更好。

举几个例子：

- Item 16: Favor composition over inheritance

组合优先于继承，是不是很耳熟？这不就是"设计模式"的思路么。

- Item 13: Minimize the accessibility of classes and members 

这适用于所有面向对象编程的原则。

- Item 38: Check parameters for validity

防御性编程。

- Item 40: Design method signatures carefull

API设计。

- Item 45: Minimize the scope of local variables

重构实践。


### 悲惨的现实
以我在这个行业的经验来看，大部分的商业产品Java代码并没有遵循Effective Java的建议。这真是行业的**重大损失**啊。


我后来看到Google的一些Java开源项目，我认为那些代码非常遵循Effective Java的建议。这是不是和Joshua Bloch加如Google成为高级架构师有关，我不敢说。但是我敢说，那些Java的顶尖高手都是读过这本书，而且在他们的代码里实践了这些东西。

