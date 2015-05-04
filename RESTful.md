## 我理解的RESTful
最近几年RESTful的架构成为主流。但是，感觉每个人对RESTful的理解都有所不同。自己也看了不少文章，听了些讲座。RESTful是一种*风格*，不是一种*标准*，这给了大众自由把握的空间。我从自己的行业经验和对技术的理解，来写自己对RESTful的理解。

### RESTful和HTTP
首先来说RESTful的发明者Roy Fielding，他同时也是HTTP规范的制订者之一。在我看来，RESTful风格和HTTP有极其相似的理念。从理论上说，RESTful可以是非HTTP的，但实际运用上几乎都是HTTP的。我还没见过不在HTTP上的RESTful运用。我认为，Roy Fielding是把HTTP的理念单独抽出来形成RESTful风格。或者说，Roy Fielding**认为大家在滥用HTTP协议的初衷，所以要强化原来的理念，单独剥离出来。**

最典型的就是动词的使用：CRUD对应的PUT，POST，DELETE和GET。这些HTTP header里的标志本来就是设计的原意。很多场合，或许是为了图方便，一个应用全都使用一个GET或者POST。当然程序不会错，但是当你用GET的header去做一个更新操作的时候，这肯定不是制订HTTP规范的人的意图。所以，从这个角度来讲，原先的SOAP是滥用了HTTP协议。

RESTful里还有cache的概念，想想HTTP协议里面有一大堆和cache相关的header。和时间相关的cache，还有和内容相关的cache的。这些cache必须和GET动词联合用才有效果。这完全就是HTTP的概念。当然，还有标准的response code。

### HATEOAS (Hypermedia as the Engine of Application State)
这是RESTful最高的最成熟的级别，也是大家感觉比较玄虚的部分。别忘了我之前说的：RESTful和HTTP的关系。我认为，现在一般的网页都基本实现了这个HATEOAS！是不是觉得不太对？！看看HATEOAS的一个重要标准就是：client不需要事先知道server的变更，仍旧能正常工作。想想我们平时用浏览器上网，其实就能达到这个目的。譬如，一个网站改版了，用户仍旧能够完成先前的操作。
