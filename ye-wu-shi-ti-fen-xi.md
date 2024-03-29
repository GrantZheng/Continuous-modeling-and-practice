# 从生活中来，到生活中去，谈业务实体的抽象

实体说白了就是实实在在存在的物体，我们也可以成为事物，现实生活中桌子，电视，电脑，钱，汽车等我们都可以称为实体。它在软件建模里它们也都是逻辑上存在的。它代表参与者执行一个或多个用例时所使用的“事物”。而这个“事物”才正是我们在业务建模中所需要分析的核心概念。如果这一步分析的有问题，后面基本都会出现偏差，所以实体分析是非常重要的。

人在生活中的的欲望有千千万，但生活中满足我们欲望所用到的事物却是屈指可数的，同类型的事物在不同的业务场景下进行排列组合，可以帮助人们实现不同的愿望。可见，我们对事物的合理抽象显得尤为重要！

我们如何找出我们所需要的“事物”呢？

在现实生活中，我们要做一件事情，凭我们的生活经验和书上学到的知识，我们都知道需要哪些工具。但是回到虚拟世界中，尤其是面对互联网快速变化的业务场景，演化出来各种新鲜玩儿法的APP，里面的东西都是看得见摸不着，甚至有的东西看也看不见，那么在这样的背景下，我们去抽象一个实体可能就会犯迷糊。

实体的抽象也是顶层设计思路中必不可少的一部分，之前在面试的时候我经常会问如果你作为一个后台技术负责人，你应该如何设计微信朋友圈，直播平台等这类业务平台。大部分的候选人都会在一开始陷入一些细节，比如考虑朋友圈列表页如何设计，使用读扩散还是写扩散，直播的cdn推拉流该怎么做。其实考虑到这些细节都很好，但是作为一个技术负责人缺乏顶层设计能力，这个系统有哪些模块组成，模块之间的逻辑关系是怎样的，这才是作为技术负责人在设计初期该重点考虑的问题。

我们还是以礼物系统为例，来说这个问题。礼物系统的用例在上一节已经介绍过了，我们就以送礼物这个核心用例入手，试着找出其背后的业务实体。大家可以先自行思考下，再看图下面的结论。

![图1](<.gitbook/assets/image (12).png>)

如果想不明白可以试着想下现实生活中送礼物的场景是怎样的，如下图所示，相信大家在学生时期对此场景都比较熟悉。

![图2](<.gitbook/assets/image (13).png>)

我们可以试想一下，在生活中，倘若你想去给一个女孩子送礼物，你会怎么做？常见的步骤如下：

1. 去商场选礼物（商品）— 花，然后付钱
2. 挑选贺卡，然后付钱
3. 找送礼物的渠道（快递送，自己送），然后付钱

然后，找出用到的”关键事物”—对目标有直接贡献的事物：商品，送货渠道，钱，贺卡，最后再分析事物之间的联系，并映射到我们的虚拟世界中，从而得出我们的实体模型，如下图所示：

![图 3](<.gitbook/assets/image (14).png>)

在此过程中，我们容易犯如下错误：

1 分析间接事物。比如，我开着宝马去给妹子送礼物，宝马车这类交通工具我们不应该拿来进行分析，因为他的存在与否不会影响到我们达成目标。当然，你如果说硬要分析，到最后也会把系统设计出来，只不过会增加系统本身的复杂度，且随着这些间接事物的增加会分散你的精力，抓不住关键点。

2 过度的依赖现实场景向虚拟场景的转化，且将现实中的场景原封不动的搬到虚拟场景中。我们只有理不清的时候才会去考虑在现实中进行类比，但并不意味着要把现实中的所有的物件都原封不动的搬到虚拟世界中，如果这样可能在后期会造成过度设计，我们还是要以虚拟世界中的需求场景为主，对现实中的物件进行裁剪来满足我们在虚拟世界中的需求！比如说，我们在送礼物中会有商品的概念，但是我们在做的时候需不需要把电商的那一套给搬过来呢，显然是不用的，我们需要结合直播业务中商品的特性，对商品的概览进行裁剪。
