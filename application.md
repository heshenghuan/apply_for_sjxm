# 面向微博语料的中文词法分析技术

## 一、立项依据

### 1、项目来源

本项目来源于对“大数据”时代互联网海量文本语料资源进行有效利用的需求，研究海量语料资源条件下的微博语料的中文词法分析问题。中文词法分析主要包括中文分词、词性标注和命名实体识别任务，而微博语料的中文分词和词性标注问题是近年来的研究热点，也是当前工业界亟待解决和应用的热点问题。面向微博语料的中文词法分析技术，是工业界很多基于微博的项目（如突发事件检测，事件追踪，舆情分析）的基础，因为中文语料的特殊性，大多是中文自然语言处理任务都必须建立在已分词（词性标注）文本的基础上才能完成。因此，项目的完成将有助于推动互联网相关自然语言处理任务的研究，具有重要的理论意义和应用价值。

### 2、项目研究意义

随着计算机与网络技术的发展，网络社交媒体（social media）不断壮大，并且用户数目不断增多，每时每刻都有数量庞大的信息在网络上产生、传播。微博（Weibo, MicroBlog）是一个基于用户关系的信息平台，用户通过建立关注、被关注、相互关注，可以轻松获取、分享和转发微博平台上海量的微信息。这一切通过操作手机或使用浏览器就可以简单实现。

然而微博上包含的海量语料，是无法直接用于计算机处理的。而且，与新闻报纸等语料相比，微博语料具有以下显著特点：第一，文本长度短小但数量众多；第二，具有不规范性，文法通常是非正式的，语言偏口语化和生活化，带有缩写、拼写错误、不规范用语、噪音及表情符，增加了用户对有价值信息发现的难度；第三，微博短文中通常包含显著的个人意图和明显的个人主义情感色彩；第四，具有半结构化的特点，除了文本内容还包含一些元数据，如发布时间、收藏数量、转发量等等；第五，微博文本通常是某对话线索（conversation thread）中的一个发言或回复，因此每个线索包含多个微博文本，形成充足的上下文；第六，微博文本中因对话线索而形成丰富的上下文，常常有大量的省略和指代【1】。

此外，微博不同于传统媒体，它的发布者和接受者之间无显著区别，拥有完全平等的发言权。微博内容不受题材限制，对用户表达能力要求极低，用户能用只言片语，反映自己的心情即可。可以说，微博上语料的质量参次不齐，但是基于微博用户的庞大数目，微博每时每刻都在产生着海量的语料资源。然而这些未标注的语料资源是无法直接应用的，因此需要一个高效准确的中文词法分析技术对这些语料进行处理、分析和标注。但目前，还没有较为成熟、完善的现有的中文分词（Chinese word segmentation）算法能比较高效准确的处理微博语料。因此，我们现在面对的局面是空有海量的微博语料却没有有效的手段去利用这些资源。故开发一个面向微博语料的中文词法分析技术（包括中文分词，词性标注和命名实体识别等）不仅有重大的理论意义，而且具有使用价值。

// 研究意义在ref_1中有很多

### 3、国内外实践研究现状、水平和发展趋势

#### 3.1 国内外学术研究现状

（1）国外学术研究现状

早期与微博文本相关的工作集中在语言分析方面。(Java et al., 2007)对微博的概念和作用进行了总结和探讨，介绍了微博的即时性、共享性、快速传播等特点，并从各个角度统计了微博在近年来的使用增长情况【9】。他们根据用户间的关系，阐述了哪一类的用户会分享相同的微博信息。(Kwak et al., 2010)讨论了微博的出现，作为一种社交网络或是一种新闻媒介对世界的影响【10】。(Ellen, 2011)则对微文本(mircotext)进行了特征分析，认为微文本具有“短”、“文法不规范”和“半结构化”等特点【11】。这些工作，为研究者了解并把握微博文本的特征提供了重要依据。(Locke, 2009)将命名实体识别引入到微博文本的研究中，采用分类的方法将命名实体分为三个不同的类别（人名，地名，机构名）【12】。他指出，微博文本由于具有与普通文本许多不同的特征，所以在进行特征选择时，应该选择微博文本所特有的特征，再进行分类。实验证明，该方法取得了一定程度的提高。

在初步了解了微博文本的语言特点后，研究者们开始尝试对其进行处理。由于微博文本字数少，区别于普通文本的特点很多，所以在大多数使用机器学习的方法对其进行处理时，尝尝会发生严重的数据稀疏问题，对性能产生影响。

（2）国内学术研究现状

// 国内学术研究现状在ref_1中section 3

#### 3.2 国内外实践与应用研究现状



### 参考文献

1. 张剑峰, 夏云庆, 姚建民. 微博文本处理研究综述[J]//中文信息学报, 2012, 26(4):21-27.
2. 石秋慧. 微博热点话题抽取及其情感分类[D]//哈尔滨工业大学, 2014.
3. Wang L, Wong D F, Chao L S, et al. CRFs-based Chinese word segmentation for micro-blog with small-scale data[C]//Second CIPS-SIGHAN Joint Conference on Chinese Language Processing. 2012: 51-57.
4. Zhang K, Sun M, Zhou C. Word segmentation on Chinese mirco-blog data with a linear-time incremental model[C]//Second CIPS-SIGHAN Joint Conference on Chinese Language Processing. 2012: 41-46. 
5. 于清, 阿里甫·库尔班. 微博语料分词及标注方法初探[J]//新疆大学学报:自然科学版, 2013(1).
6. 邱泉清, 苗夺谦, 张志飞. 中文微博命名实体识别[J]//计算机科学, 2013, 40(6).
7. Huiming D, Zhifang S, Ye T, et al. The CIPS-SIGHAN CLP 2012 Chinese Word Segmentation on MicroBlog Corpora Bakeoff[C]//Second CIPS-SIGHAN Joint Conference on Chinese Language Processing. 2012: 35-40.
8. Jing Z, Degen H, Xia H, et al. Rules-based Chinese Word Segmentation on MicroBlog for CIPS- SIGHAN on CLP2012[C]//Second CIPS-SIGHAN Joint Conference on Chinese Language Processing. 2012: 74-78.
9. Java A, Song X, Finin T, et al. Why we twitter: understanding microblogging usage and communities[C]//Proceedings of the 9th WebKDD and 1st SNA-KDD 2007 workshop on Web mining and social network analysis. ACM, 2007: 56-65.
10. Kwak H, Lee C, Park H, et al. What is Twitter, a social network or a news media?[C]//Proceedings of the 19th international conference on World wide web. ACM, 2010: 591-600.
11. Ellen J. All about Microtext-A Working Definition and a Survey of Current Microtext Research within Artificial Intelligence and Natural Language Processing[J]. ICAART (1), 2011, 11: 329-336.
12. Locke B W. Named entity recognition: Adapting to microblogging[J]. 2009.