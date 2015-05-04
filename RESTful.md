## 我理解的RESTful
最近几年RESTful的架构成为主流。但是，感觉每个人对RESTful的理解都有所不同。自己也看了不少文章，听了些讲座。RESTful是一种*风格*，不是一种*标准*，这给了大众自由把握的空间。我从自己的行业经验和对技术的理解，来写自己对RESTful的理解。

### RESTful和HTTP
首先来说RESTful的发明者Roy Fielding，他同时也是HTTP规范的制订者之一。在我看来，RESTful风格和HTTP有极其相似的理念。从理论上说，RESTful可以是非HTTP的，但实际运用上几乎都是HTTP的。我还没见过不在HTTP上的RESTful运用。我认为，Roy Fielding是把HTTP的理念单独抽出来形成RESTful风格。或者说，Roy Fielding**认为大家在滥用HTTP协议的初衷，所以要强化原来的理念，单独剥离出来。**

最典型的就是动词的使用：CRUD对应的PUT，POST，DELETE和GET。这些HTTP头里的标志本来就是设计的原意。很多场合，或许是为了图方便，一个应用全都使用一个GET或者POST。当然程序不会错，但是当你用GET的头去做一个更新操作的时候，这肯定不是制订HTTP规范的人的意图。


