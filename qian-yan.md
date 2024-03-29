# 前言

### 建模重要吗？

对于建模概念我不想赘述，但对其重要性，我觉得值得多次强调。虽说计算机技术飞快发展，涌现了各种架构名词，比如：Monolithic，SOA，Micro-Service，Serverless 等，也出现了各种新技术，比如：区块链，大数据，AI等。但最后的落地都需要依赖优秀的架构和工程能力，而对建模知识的掌握正是这些能力形成的基础。

当然也会听到不少反面的声音，比如：有些人不爱建模，觉得没啥用，照着自己的方法弄照样能够稳定的运行。我想说要么你的业务复杂度和规模太小，暴露不了问题，或者你的角色还没达到要用到建模的地方。

当然还会有些想法，比如：先上，让业务跑起来，先顶住再优化，但最后的结果是迟迟未优化，总有高邮优的事情插在前面。或者用人海战术，堆人，从而导致研发成本的上升。但是作为一名架构师来说，能一次做对的事情，为什么要以信任为代价，要反复做多次呢。有时候机会真的只有一次，一不留意稍纵即逝！

### 建模必要吗？

是否有必要主要还是看人和看事，如果遇到个小需求，你只需要在某个系统中加个字段就能满足，而且能确保后续的扩展性，那么此时建模可能不是必要的。也有些人水平非常高，经验也很丰富，可能有些东西在脑子过一遍就能想明白，那么对于这类高手来讲，只能说建模早已印在了心中，已经达到了无招胜有招的地步。但对于大多数人，包括我自己来说，面对一个稍微复杂点的需求，我还是会老实画图，并找同事来一起来反复推演和验证。

### 为什么要写《持续建模与实践》？

本来最初只想以《持续建模》为主题来写的，但最后想到平时看到了太多的ppt架构，看ppt觉得设计的不错，一看代码，真是一地鸡毛，所以最后还是加上了一点“实践的内容“。

笔者长期在互联网一线从事系统设计和开发工作，在日常面试和工作中发现，大家在系统设计和建模方面的能力积累的比较少。每次在讨论和review系统设计方案的时候，不同的人身上总会出现相似的现象：

现象1：需求沟通完，就开始设计数据表结构，想到的是数据库设计三范式：第一范式，第二范式和第三范式。然后，要建哪些索引，有哪些唯一键，如何保证事务等，陷入一个种面向数据编程的思路。

现象2：接到需求，就写代码，想到哪儿写到哪儿，既不关心为何要做这样的需求，也不考虑需求变化后，如何保证系统的弹性。到最后可能才发现，好复杂，代码越写越多，当时想简单了，或者随着需求的迭代，现有的系统已经满足不了越来越复杂的需求了，萌生了重构的想法。

现象3：经验驱动设计，我以前XX公司做过类似的，是这样设计的，但是要他讲为什么这样设计，却又说不上来，总会有一种“似是而非”的感觉，自己阐述的东西，缺乏理论支撑。另外，随着时代的发展，技术是革新的，经验随着时代和场景的变化，可能不再受用，而唯一能支撑我们却是逐渐形成的知识体系。

现象4：按照业务方提供的业务流程图来设计系统，容易在一开始陷入功能细节，以致分不清主次，理不清系统之间的关系，导致无法按期完成交付，或者设计出来的系统扩展性极差。

现象5：做一个需求的时候，同一个字段加到A系统中可以实现需求，加到B系统中同样也可以实现需求，那么我们到底该放哪儿呢？这时我们不应该从实现功能的角度来考虑这个问题，应该从系统层面来看，维护这个字段的职责放在哪个系统更为合理！

现象6：懂点系统设计，但是画出来的图一团糟，旁人要么看不懂，要么会产生歧义。

现象7：多个同学在一起讨论需求和方案的时候，经常会出现大家思考的点不在一个层次上的现象，比如A同学在讲如何实现需求，B同学站在行性能的角度上，可能会说你这个有性能问题，应该如何如何设计，然后C同学又跑过来说，你这样弄扩展性不好，可维护性也不好。大家站在各自的角度上，各执其词，说的都有道理，那么该如何抉择呢？

当然现实中暴露的问题远不止以上几条，渐渐发现这是一个很普遍的现象。正式由于此类现象的出现，从而导致后期的系统维护难，沟通成本高，投入人力大，生产效率低等问题。而在工作中，每次都要把同样的设计理论反反复复传授给不同的人，之前也在网上写过几篇相关的文章，也有在公司内部讲过类似的课程，但总有种一篇难尽，一言难尽的感觉，事后有不少朋友和同事问我有没有相关的书可以参考，能不能说的再详细点和系统点。故想以《持续建模与实践》为主题，总结一些建模相关的思路，分享下笔者在工作中的一点经验，帮助后来者少走弯路。

笔者写这本书的目的，就是帮助大家绕开那些误区。另外，关于一些建模的基本概念，市面上有不少的书籍已经对其进行了很好的解释，我在这里不会对其进行详细的讲解，我尽量用最精炼的语言来阐述建模过程中的一些关键点。

### 是否存在重复造轮子的嫌疑？

目前市面上将这方面知识的书籍也很多，光介绍《领取驱动设计》的就有好几本，还有一些讲软件工程，UML建模相关的等。可能大家不喜欢轮子漫天飞的环境，尤其是造出来的轮子还没别人的好，就显的更尴尬了。我个人也不喜欢造轮子，也不喜欢在书里面提出新概念，然后为了说明这个概念去使用更多的概念。本书中提到的都是早已存在的方法和理论，只是我对这些方法和理论有一些新的认知视角，结合多年的项目实践，总结出了一套简化的建模方法，分享出来，供大家批评和指正，或许对大家理解现有的现有的建模理念有些助益吧。

《持续建模与实践》同市面上已有的经典建模书籍有何不同？

1 晦涩难懂的概念，如：领域模型/限界上下文/值对象/聚合根/实体/用例等，有些概念一看是那么回事儿，但是实际落地又无从下手；

2 案例太陈旧，常见的案例大部分都是那些传统的软件案例，如图书管理系统，银行系统，电力系统等，离我们经常遇到的互联网类的业务场景有一定的距离，所以当我们拿到需求的时候，不知道如何的去运用书上所阐述的理论来解决我们的实际问题；

3 所阐述的方法大而全，很难满足我们快速变化和迭代的互联网需求。举个例子，就拿《领域驱动设计》这本书来说，书中强调要有“领域专家”，可是当我们面对日新月异的互联网产品时，对所有人而言，一切事物都是新的，大家都是在摸着石头过河和探索，此时又哪来的领域专家呢！

《持续建模与实践》的内容是笔者基于传统的建模理论，在工作中通过大量的互联网业务系统的实践而总结出来的，里面提到的建模思想和方法都是笔者亲自实践且验证过的，偏向于”实用主义”。其主要由以下几个章节组成：

第一章 关于建模的是是非非

1.1 DDD并非唯一的建模方法

1.2 并不是微服务才需要建模

1.3 也许刚开始单体架构才是最优选择

1.4 浅谈建模学习的三重境界

第二章 我的方法论

2.1 统一认识：建模的本质是映射

2.2 通过用例描述现实需求

2.3 从生活中来，到生活中去，谈业务实体的抽象

2.4 从业务实体道动态视图的构建

2.5 从物质的客观实在性看实体属性

2.6 系统架构图

第三章 架构方案选型和验证

3.1 常见的架构模型——单体，SOA，微服务

3.2 如何抉择

3.3 如何证明架构模型的有效性

3.4 如何有效的落地

第四章 实战

4.1 基于gokit，快速构建易于拆分的单体应用

为了便于大家理解，我选取目前市面上两款常见的产品——“微信朋友圈”、“直播平台”作为案例来讲解上述理论。随着需求的迭代，这些产品所包含的功能也越来越多，我们在讲解时只需要关注产品最基本的形态即可，目的是为了帮助大家理解建模理论。当然，由于笔者的工作经历有限，所阐述的内容如有不对还请指正。另外，如果大家有其它的产品case想讨论，也可以留言，我们一起来分析。
