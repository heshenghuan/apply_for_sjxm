# 面向微博语料的中文词法分析技术

## 一、立项依据

### 1、项目来源

本项目来源于对“大数据”时代互联网海量文本语料资源进行有效利用的需求，研究海量语料资源条件下的微博语料的中文词法分析问题。中文词法分析主要包括中文分词、词性标注和命名实体识别任务，而微博语料的中文分词和词性标注问题是近年来的研究热点，也是当前工业界亟待解决和应用的热点问题。面向微博语料的中文词法分析技术，是工业界很多基于微博的项目（如突发事件检测，事件追踪，舆情分析）的基础，因为中文语料的特殊性，大多是中文自然语言处理任务都必须建立在已分词（词性标注）文本的基础上才能完成。因此，项目的完成将有助于推动互联网相关自然语言处理任务的研究，具有重要的理论意义和应用价值。

### 2、项目研究意义

随着计算机与网络技术的发展，网络社交媒体（social media）不断壮大，并且用户数目不断增多，每时每刻都有数量庞大的信息在网络上产生、传播。微博（Weibo, MicroBlog）是一个基于用户关系的信息平台，用户通过建立关注、被关注、相互关注，可以轻松获取、分享和转发微博平台上海量的微信息。这一切通过操作手机或使用浏览器就可以简单实现。

然而微博上包含的海量语料，是无法直接用于计算机处理的。而且，与新闻报纸等语料相比，微博语料具有以下显著特点：第一，文本长度短小但数量众多；第二，具有不规范性，文法通常是非正式的，语言偏口语化和生活化，带有缩写、拼写错误、不规范用语、噪音及表情符，增加了用户对有价值信息发现的难度；第三，微博短文中通常包含显著的个人意图和明显的个人主义情感色彩；第四，具有半结构化的特点，除了文本内容还包含一些元数据，如发布时间、收藏数量、转发量等等；第五，微博文本通常是某对话线索（conversation thread）中的一个发言或回复，因此每个线索包含多个微博文本，形成充足的上下文；第六，微博文本中因对话线索而形成丰富的上下文，常常有大量的省略和指代【1】。

此外，微博不同于传统媒体，它的发布者和接受者之间无显著区别，拥有完全平等的发言权。微博内容不受题材限制，对用户表达能力要求极低，用户能用只言片语，反映自己的心情即可。可以说，微博上语料的质量参次不齐，但是基于微博用户的庞大数目，微博每时每刻都在产生着海量的语料资源。然而这些未标注的语料资源是无法直接应用的，因此需要一个高效准确的中文词法分析技术对这些语料进行处理、分析和标注。但目前，还没有较为成熟、完善的现有的中文分词（Chinese word segmentation）算法能比较高效准确的处理微博语料。因此，我们现在面对的局面是空有海量的微博语料却没有有效的手段去利用这些资源。故开发一个面向微博语料的中文词法分析技术（包括中文分词，词性标注和命名实体识别等）不仅有重大的理论意义，而且具有使用价值。

// 研究意义在ref_1中有很多

### 3、国内外研究现状、水平和发展趋势

#### 3.1 国内外学术研究现状

（1）国外学术研究现状

早期与微博文本相关的工作集中在语言分析方面。(Java et al., 2007)对微博的概念和作用进行了总结和探讨，介绍了微博的即时性、共享性、快速传播等特点，并从各个角度统计了微博在近年来的使用增长情况【9】。他们根据用户间的关系，阐述了哪一类的用户会分享相同的微博信息。(Kwak et al., 2010)讨论了微博的出现，作为一种社交网络或是一种新闻媒介对世界的影响【10】。并全面统计和剖析了从Twitter出现的到文章发表的三年来，Twitter的所有相关数据，包括Twitter的日发布量、发布总量、使用人数等。(Ellen, 2011)则对微文本(mircotext)进行了特征分析，认为微文本具有“短”、“文法不规范”和“半结构化”等特点【11】。这些工作，为研究者了解并把握微博文本的特征提供了重要依据。(Locke, 2009)将命名实体识别引入到微博文本的研究中，采用分类的方法将命名实体分为三个不同的类别（人名，地名，机构名）【12】。他指出，微博文本由于具有与普通文本许多不同的特征，所以在进行特征选择时，应该选择微博文本所特有的特征，再进行分类。实验证明，该方法取得了一定程度的提高。

在初步了解了微博文本的语言特点后，研究者们开始尝试对其进行处理。由于微博文本字数少，区别于普通文本的特点很多，所以在大多数使用机器学习的方法对其进行处理时，尝尝会发生严重的数据稀疏问题，对性能产生影响。于是,研究者们对解决数据稀疏问题进行了一 些尝试。(Sriram et al., 2010)等考虑到微博文本区别于普通文 本的特征,共选取了八类特征(即作者信息,发布时 间,标志符号等)【13】。加入这些特征之后，算法的性能得到了显著提高，改善了数据稀疏的问题。

可以发现，大多数研究者都对微博文本采用了特殊的特征工程(special feature engineering)，希望可以实现更好的特征表示和处理效果。这说明国外的学者对于微博文本的处理，普遍认为应该是用特殊的方法，而不是使用同普通文本一样的处理方法、工具等。但大多数国外研究者研究的主要方向是面向微博语料的文本分类和聚类、信息抽取、话题检验和情感分析等。这主要是由于国外研究者的微博语料来自于Twitter(一家美国社交网络及微博客服务的网站，是全球互联网上访问量最大的十个网站之一)，其用户大多数为国外人员，且大部分语料资源是英文等不需要进行分词的语料，因此对于微博文本的词法层面的研究几乎没有。但他们的研究思路和成果对于中文微博语料的研究有很好的借鉴意义。

（2）国内学术研究现状

不同于英语、葡萄牙语等语言，中文的词与词之间没有明显的分隔符号。而词又是理解句子的最小单位，这就导致分词成为中文信息处理非常重要的第一步。面向传统语料的分词系统已经十分成熟，并提供了词性标注和命名实体识别等功能的整合。然而，面向微博语料的分词、词性标注和命名实体识别却刚刚起步。这一方面是由于微博语料的特殊特点，另一方面，最主要的原因还是由于训练数据的匮乏。由于微博上拥有海量的语料资源，而人工标注数据费时费力，但经过人工标注、校对过的数据又是训练一个机器学习算法必不可少的，这就导致了矛盾的产生--我们需要数据却没有足够的数据。

为了解决这样的矛盾，(Zhang et al., 2012)提出了一个基于线性时间复杂度的增量模型的分词算法【4】。他们采用的是基于词的分词算法，同时使用了丰富的特征，包括：字特征(character-based features)，词特征(word-based features)和其他容易使用的可能特征。他们首先使用人民日报语料训练了一个通用目的的分词、词性标注联合模型，之后使用这个模型产生的结果作为最终微博分词模型的特征。并且，各种词汇表特征，例如词典和熟语、成语表也被用于对微博数据的分词。有关URL和特殊字符的处理也被引进。(Wang et al., 2012)首次将条件随机场（Conditional Random Fields）模型用于解决中文微博语料的分词问题【3】。他们也同样遇到了训练语料匮乏的问题，但考虑到文本语言的独特性，他们提出了一些方法让CRFs模型更适用于微博领域的分词。具体来说，他们不仅设计了最好的特征模板，而且使用了新的6-tag标注集，外部一元词典信息和其他领域语料来提升系统在中文微博语料上的分词性能。(Jing et al., 2012)提出了一些有关微博语料上中文分词的优化规则，并从实验结果中得出结论：这些优化规则十分有用【8】。优化规则包括：（1）计算新词的出现频次，添加高频新词进入词典；（2）添加常用的标点符号组合使用例子进入词典；（3）原始系统不能很好的处理有关时间的字符串，因此建立了一套时间模板（Time Templates）用于匹配时间字符串；（4）对于包含“http”这类关键字的URl字符串进行处理。

目前国内研究者们对于微博语料的词法层面的工作，大多数都使用了添加外部语料、新型特征模板和规则化处理等方案。实验结果表明，这些方向对于提升算法的性能有一定的帮助，但还有很大的提升空间。

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
13. Sriram B, Fuhry D, Demir E, et al. Short text classification in twitter to improve information filtering[C]//Proceedings of the 33rd international ACM SIGIR conference on Research and development in information retrieval. ACM, 2010: 841-842.
14. Jiang W, Huang L, Liu Q. Automatic adaptation of annotation standards: Chinese word segmentation and POS tagging: a case study[C]//Proceedings of the Joint Conference of the 47th Annual Meeting of the ACL and the 4th International Joint Conference on Natural Language Processing of the AFNLP: Volume 1-Volume 1. Association for Computational Linguistics, 2009: 522-530.

## 二、实践目标、实践内容和拟解决的主要问题

### 2.1 实践目标

### 2.2 实践内容

### 2.3 拟解决的主要问题

## 三、可以的实践思路与方法、技术路线、实践方案（含创新性）及其可行性分析

### 1、实践思路与方法

### 2、技术路线

### 3、实践方案

### 4、可行性分析

### 5、本项目的特色与创新之处

## 四、实践工作的总体安排及进度

## 五、实践工作的预期成果及成果提交形式

### 1、预期成果

## 六、实践基础和工作条件

### 1）实践基础

项目申请人的导师夏睿一直从事自然语言处理、人工智能、机器学习和数据挖掘等方 面的研究工作。在自然语言处理和人工智能领域的顶级国际学术期刊和学术会议(IEEE IS、 Information Sciences、IJCAI、AAAI、ACL、COLING 和 IJCNLP 等)上发表高质量学术论 文 10 余篇。他曾担任国际会议 IJCAI (2013)、COLING (2014)、WWW Workshop on MABSDA (2013)、ACM KDD Workshop on WISDOM (2012, 2013)、IEEE ICDM Workshop on SENTIRE (2011, 2012, 2013) 的程序委员会委员,并担任国际期刊 Data Mining and Knowledge Discovery (2014)、IEEE IS (2012)、IEEE CIM (2013)、ACM TALIP (2010)、JCST (2011)、 计算机学报 (2014)、自动化学报 (2012, 2013) 和国际会议 IJCAI (2013), COLING (2010, 2014), IEEE NLPKE (2008, 2009) 的审稿人。### 2）工作条件

项目申请人所在的研究单位为南京理工大学计算机科学与技术学院,拥有“模式识别与智能系统”国家重点学科,依托于“高维信息智能感知与系统”教育部重点实验室,拥有良好的硬件设备和研究环境,具备若干台计算机和高性能服务器,网络环境良好,图书资料齐全,为本项目的研究工作提供了很好的支持和保障。
## 七、经费概算（单位：万元）
|支出科目|金额|计算根据及理由|
|:----:|:----:|:-----:|
|交通支出|0.5 |差旅费|
|参加会议|0.5 |根据学术需要参加会议支持|
|人员补贴|0.5 |4个人1年的项目研究经费|
|合计   |1.5 |项目申请经费|