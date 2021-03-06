我个人对二战时期围绕Enigma展开的密码攻防那段历史和相关的原理很感兴趣，曾花时间研究过Enigma的加解密原理及从波兰数学家到英国数学家针对Enigma的破解方案。

一直以来就想写一写这块的东西，但是作为拖延症重度患者迟迟没有动笔。前段时间去电影院刷了两遍<a href="http://www.imdb.com/title/tt2084970/" target="_blank">《模仿游戏》</a>，重新激起了我写这篇文章的欲望。

作为技术博客，这篇文章会将重点放在Enigma加解密及破解的数学原理，而相关的历史仅会提及但不会展开（对这段历史感兴趣的同学推荐看一本书<a href="http://book.douban.com/subject/3024665/" target="_blank">《密码传奇》</a>）。我将本文的标题设定为『图灵是如何破解Enigma的』，一方面是因为我个人对图灵的崇拜，另一方面图灵的工作确实在整个Enigma破解中是标志性的巅峰之作，但是本文不会直接进入图灵的工作，而是会从古典密码学中的置换密码开始，逐步分析整个故事中涉及的加解密及破解原理。

整个文章会分为四个部分：第一部分讲述Enigma出现前的古典密码学特别是置换密码的发展，第二部分讲解Enigma的加解密原理，第三部分讲解以雷耶夫斯基为标志人物的波兰数学家对Enigma的破解原理，第四部分讲解图灵对Enigma的分析及破解。

<!-- toc -->

# 1 现代密码学视角下的置换密码机制
二战时期包括Enigma密码机从密码学分类来说，仍属于古典密码的置换密码体系。很多文章在讲述古典密码时会直接从朴素的角度进行描述。而随着二战后科技的发展及信息理论的数学化，现代密码学更多是从数学和信息论角度进行表述。

这里我将会先给出现代密码学理论的基础知识，然后从现代密码学角度分析置换密码的特点，这样其实更有助于从本质上理解密码的本质。

## 1.1 加密及解密的数学表示

### 1.1.1 字符集

任何一种语言，首先要有一个字符集，字符集是一个集合，其中的每一个元素叫做一个字符，字符是构成这种语言的不可再分的原子成分。

理论上字符集可以是有限集合或无限可数集合，一般情况下，我们在密码学中仅考虑有限集合。

下面举几个字符集的例子：

+ 二进制整数的字符集是$\\{0,1\\}$
+ 十进制整数的字符集是$\\{0,1,2,3,4,5,6,7,8,9\\}$
+ 英文的字符集是英文字母以及所有在英文中可能出现的标点符号及空格等分隔符（自然语言在没有严格定义的情况下比较复杂，如果考虑外来语等还要包括外来语中的字符，但是密码学中一般考虑形式语言，即语言实例中出现的字符严格来自字符集）

### 1.1.2 语言

非形式化的说，给定字符集$\\Sigma$。由$\\Sigma$生成的语言是所有由$\\Sigma$字符组成的字符串（包括空串）的集合。