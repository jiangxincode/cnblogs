---
title: "R语言书籍的学习路线图"
categories:
  - others
tags:
  - R
  - 书籍
toc: true
---

现在对R感兴趣的人越来越多，很多人都想快速的掌握R语言，然而，由于目前大部分高校都没有开设R语言课程，这就导致很多人不知道如何着手学习R语言。
对于初学R语言的人，最常见的方式是：遇到不会的地方，就跑到论坛上吼一嗓子，然后欣然or悲伤的离去，一直到遇到下一个问题再回来。当然，这不是最好的学习方式，最好的方式是——看书。目前，市面上介绍R语言的书籍很多，中文英文都有。那么，众多书籍中，一个生手应该从哪一本着手呢？入门之后如何才能把自己练就成某个方面的高手呢？相信这是很多人心中的疑问。有这种疑问的人有福了，因为笔者将根据自己的经历总结一下R语言书籍的学习路线图以使Ruser少走些弯路。
本文分为6个部分，分别介绍初级入门，高级入门，绘图与可视化，计量经济学，时间序列分析，金融等。

## 1.初级入门

`An Introduction to R`，这是官方的入门小册子。其有中文版，由丁国徽翻译，译名为`R导论`。`R4Beginners`，这本小册子有中文版应该叫`R入门`。除此之外，还可以去读刘思喆的`153分钟学会R`。这本书收集了R初学者提问频率最高的153个问题。为什么叫153分钟呢？因为最初作者写了153个问题，阅读一个问题花费1分钟时间，全局下来也就是153分钟了。有了这些基础之后，要去读一些经典书籍比较全面的入门书籍，比如`统计建模与R软件`，国外还有`R Cookbook`和`R in action`，本人没有看过，因此不便评论。
最后推荐，`R in a Nutshell`。对，“果壳里面的R”！当然，是开玩笑的，in a Nutshell是俚语，意思大致是“简单的说”。目前，我们正在翻译这本书的中文版，大概明年三月份交稿！这本书很不错，大家可以从现在开始期待，并广而告知一下！

## 2.高级入门

读了上述书籍之后，你就可以去高级入门阶段了。这时候要读的书有两本很经典的。`Statistics with R`和`The R book`。之所以说这两本书高级，是因为这两本书已经不再限于R基础了，而是结合了数据分析的各种常见方法来写就的，比较系统的介绍了R在线性回归、方差分析、多元统计、R绘图、时间序列分析、数据挖掘等各方面的内容，看完之后你会发现，哇，原来R能做的事情这么多，而且做起来是那么简洁。读到这里已经差不多了，剩下的估计就是你要专门攻读的某个方面内容了。下面大致说一说。

## 3.绘图与可视化

亚里斯多德说，“较其他感觉而言，人类更喜欢观看”。因此，绘图和可视化得到很多人的关注和重视。那么，如何学习R画图和数据可视化呢？再简单些，如何画直方图？如何往直方图上添加密度曲线呢？我想读完下面这几本书你就大致会明白了。
首先，画图入门可以读`R Graphics`，个人认为这本是比较经典的，全面介绍了R中绘图系统。该书对应的有一个网站，google之就可以了。更深入的可以读`Lattice：Multivariate Data Visualization with R`。上面这些都是比较普通的。当然，有比较文艺和优雅的——ggplot2系统，看`ggplot2：Elegant Graphics for Data Analysis`。还有数据挖掘方面的书：`Data Mining with Rattle and R`，主要是用Rattle软件，个人比较喜欢Rattle!当然，Rattle不是最好的，Rweka也很棒！再有就是交互图形的书了，著名的交互系统是ggobi，这个我已经喜欢两年多了，关于ggobi的书有`Interactive and Dynamic Graphics for Data Analysis With R and GGobi`，不过，也只是适宜入门，更多更全面的还是去ggobi的主页吧，上面有各种资料以及包的更新信息！
特别推荐一下，中文版绘图书籍有谢益辉的`现代统计图形`。

## 4.计量经济学

关于计量经济学，首先推荐一本很薄的小册子:`Econometrics In R`，做入门用。然后，是`Applied Econometrics with R`，该书对应的R包是AER，可以安装之后配合使用，效果甚佳。计量经济学中很大一部分是关于时间序列分析的，这一块内容在下面的地方说。

## 5.时间序列分析

时间序列书籍的书籍分两类，一种是比较普适的书籍，典型的代表是：`Time Series Analysis and Its Applications：with R examples`。该书介绍了各种时间序列分析的经典方法及实现各种经典方法的R代码，该书有中文版。如果不想买的话，建议去作者主页直接下载，英文版其实读起来很简单。时间序列分析中有一大块儿是关于金融时间序列分析的。这方面比较流行的书有两本`Analysis of financial time series`，这本书的最初是用的S-plus代码，不过新版已经以R代码为主了。这本书适合有时间序列分析基础和金融基础的人来看，因为书中关于时间序列分析的理论以及各种金融知识讲解的不是特别清楚，将极值理论计算VaR的部分就比较难看懂。另外一个比较有意思的是Rmetrics推出的`TimeSeriesFAQ`，这本书是金融时间序列入门的东西，讲的很基础，但是很难懂。对应的中文版有`金融时间序列分析常见问题集`，当然，目前还没有发出来。经济领域的时间序列有一种特殊的情况叫协整，很多人很关注这方面的理论，关心这个的可以看`Analysis of Integrated and Cointegrated Time Series with R`。最后，比较高级的一本书是关于小波分析的，看`Wavelet Methods in Statistics with R`。附加一点，关于时间序列聚类的书籍目前比较少见，是一个处女地，有志之士可以开垦之！

## 6.金融

金融的领域很广泛，如果是大金融的话，保险也要被纳入此间。用R做金融更多地需要掌握的是金融知识，只会数据分析技术意义寥寥。我觉得这些书对于懂金融、不同数据分析技术的人比较有用，只懂数据分析技术而不动金融知识的人看起来肯定如雾里看花，甚至有人会觉得金融分析比较低级。这方面比较经典的书籍有：`Advanced Topics in Analysis of Economic and Financial Data Using R`以及`Modelling Financial Time Series With S-plus`。金融产品定价之类的常常要用到随机微分方程，有一本叫`Simulation Inference Stochastic Differential Equations：with R examples`的书是关于这方面的内容的，有实例，内容还算详实!此外，是风险度量与管理类。比较经典的有`Simulation Techniques in Financial Risk Management`、`Modern Actuarial Risk Theory Using R`和`Quantitative Risk Management：Concepts, Techniques and Tools`。投资组合分析类和期权定价类可以分别看`Portfolio Optimization with R`和`Option Pricing and Estimation of Financial Models with R`。

## 7.数据挖掘

这方面的书不多，只有`Data Mining with R:learing with case studies`。不过，R中数据挖掘方面的包已经足够多了，参考包中的帮助文档就足够了。

## 8.附注

出于版权等事宜的考虑，我无法告知你说在“新浪爱问”等地方可以直接免费下载到上面提到的这些书，但是，我想你可以发挥自己的聪明才智去体悟！

原始出处: <http://yishuo.org/r/2012/01/19/how-to-learn-r-by-reading-books.html>
