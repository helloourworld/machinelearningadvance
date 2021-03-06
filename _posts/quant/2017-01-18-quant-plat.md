---
layout: post
title: 量化平台ABC
category: Quant
catalog: yes
description: 量化平台ABC
tags:
    - quant
    - python
---
zipline + pyfolio 搭建的量化策略研究平台，解决了策略回测和评价的大部分问题，为quantopian的开源点赞！

# 国内量化平台

作者：匿名用户
链接：https://www.zhihu.com/question/35097533/answer/91017820
来源：知乎
著作权归作者所有，转载请联系作者获得授权。

这个话题我喜欢，摆事实讲道理是我强项。待我放下了手中的狗粮，为大家静静的撸一发。

本人程序猿一枚，去年股灾2.0，本金腰斩时（每念及此，悲从中来不可断绝）开始接触量化/平台。
半年多以来，市面上比较活跃的python量化平台主要有：优矿，米筐，聚宽。本猿都有接触一丢丢，反正不用花钱，其中米筐和聚宽跟国外quantopian非常相似。

分享一下在使用过程中的感受：

优矿：
1. 数据种类丰富，收费数据可以免费试用
2. 有活跃的社区（日报我很喜欢哦，如果有动态大图就更破费了）
3. 前几天推出的快速版和一个简化信号功能，体验了两天，回测速度非常快，爽。
4. @楼上匿名用户，我觉得自动补全很好用啊，文档都可以看到，使用DataAPI方便的不行。
5. 优矿每月都有500万实盘大赛，听说赚了都归我。之前没参赛，打算用简化信号功能开发一个策略参赛玩玩
6. history拿历史数据的api太多了。界面体验上没另外两家好，熟悉平台时间也要长一些。


米筐：
1. 米筐的founder们是一群具有交易系统气质的大牛，开发实力强劲。
2. 平台同时支持python和java两种语言的回测。
3. 米筐的视觉设计和文档做的非常棒，特别是回测结果页面，看着很舒服。
4. 米筐举办的大赛，已经有两期了，奖品还可以，可惜也没拿到。
5. 推出功能速度有些慢，后台稳定性有待加强（最近实时模拟交易也关闭了）。


聚宽：
1. 开发速度很快，比如撤单，非复权成交等等功能，新功能上线很迅速；
2. 社区也比较活跃，很多不错的ETF策略
3. 聚宽没有举办大赛，而是推出了销售策略活动，打算提交一个试试。
4. 微信推送调仓很好用，期待政府早日放开实盘限制
5. 回测速度比上面两家慢，有时候会卡死。


总结：
个人目前主要在优矿上玩。在ipython notebook进行完策略研究，直接编写策略，这种一体化的感觉很好，适合我们这种追求完美与极致体验的星座。也经常去聚宽社区，挖掘靠谱思路。米筐体验上很好，但是现在越用越少，希望他们能在功能上努力加油。

关于回测速度，本猿特意在三个平台分别运行了一个4年HS300按日调仓的日线双均线策略（颤抖吧，人类）回测时间如下：

    |UQER |RQ |JQ
hs300双均线 |60s |264s |150s

# 什么是量化策略？

**什么是量化策略？**

* 量化策略是指使用计算机作为工具，通过一套固定的逻辑来分析、判断和决策。
* 量化策略既可以自动执行，也可以人工执行。

**一个完整的量化策略包含哪些内容？**

*一个完整的策略需要包含输入、策略处理逻辑、输出；策略处理逻辑需要考虑选股、择时、仓位管理和止盈止损等因素。

![](/images/quant/what_is_algo.jpg)

**选股**

量化选股就是用量化的方法选择确定的投资组合，期望这样的投资组合可以获得超越大盘的投资收益。常用的选股方法有多因子选股、行业轮动选股、趋势跟踪选股等。

1 多因子选股

多因子选股是最经典的选股方法，该方法采用一系列的因子（比如市盈率、市净率、市销率等）作为选股标准，满足这些因子的股票被买入，不满足的被卖出。比如巴菲特这样的价值投资者就会买入低PE的股票，在PE回归时卖出股票。

2 风格轮动选股

风格轮动选股是利用市场风格特征进行投资，市场在某个时刻偏好大盘股，某个时刻偏好小盘股，如果发现市场切换偏好的规律，并在风格转换的初期介入，就可能获得较大的收益。

3 行业轮动选股

行业轮动选股是由于经济周期的的原因，有些行业启动后会有其他行业跟随启动，通过发现这些跟随规律，我们可以在前者启动后买入后者获得更高的收益，不同的宏观经济阶段和货币政策下，都可能产生不同特征的行业轮动特点。

4 资金流选股

资金流选股是利用资金的流向来判断股票走势。巴菲特说过，股市短期是投票机，长期看一定是称重机。短期投资者的交易，就是一种投票行为，而所谓的票，就是资金。如果资金流入，股票应该会上涨，如果资金流出，股票应该下跌。所以根据资金流向就可以构建相应的投资策略。

5 动量反转选股

动量反转选股方法是利用投资者投资行为特点而构建的投资组合。索罗斯所谓的反身性理论强调了价格上涨的正反馈作用会导致投资者继续买入，这就是动量选股的基本根据。动量效应就是前一段强势的股票在未来一段时间继续保持强势。在正反馈到达无法持续的阶段，价格就会崩溃回归，在这样的环境下就会出现反转特征，就是前一段时间弱势的股票，未来一段时间会变强。

6 趋势跟踪策略

当股价在出现上涨趋势的时候进行买入，而在出现下降趋势的时候进行卖出，本质上是一种追涨杀跌的策略，很多市场由于羊群效用存在较多的趋势，如果可以控制好亏损时的额度，坚持住对趋势的捕捉，长期下来是可以获得额外收益的。

**择时**

量化择时是指采用量化的方式判断买入卖出点。如果判断是上涨，则买入持有；如果判断是下跌，则卖出清仓；如果判断是震荡，则进行高抛低吸。
常用的择时方法有：趋势量化择时、市场情绪量化择时、有效资金量化择时、SVM量化择时等。

**仓位管理**

仓位管理就是在你决定投资某个股票组合时，决定如何分批入场，又如何止盈止损离场的技术。
常用的仓位管理方法有：漏斗型仓位管理法、矩形仓位管理法、金字塔形仓位管理法等

**止盈止损**

止盈，顾名思义，在获得收益的时候及时卖出，获得盈利；止损，在股票亏损的时候及时卖出股票，避免更大的损失。
及时的止盈止损是获取稳定收益的有效方式。

**策略的生命周期**

一个策略往往会经历产生想法、实现策略、检验策略、运行策略、策略失效几个阶段。

产生想法

任何人任何时间都可能产生一个策略想法，可以根据自己的投资经验，也可以根据他人的成功经验。

实现策略

产生想法到实现策略是最大的跨越，实现策略可以参照上文提到的“一个完整的量化策略包含哪些内容？”

检验策略

策略实现之后，需要通过历史数据的回测和模拟交易的检验，这也是实盘前的关键环节，筛选优质的策略，淘汰劣质的策略。

实盘交易

投入资金，通过市场检验策略的有效性，承担风险，赚取收益。

策略失效

市场是千变万化的，需要实时监控策略的有效性，一旦策略失效，需要及时停止策略或进一步优化策略。

<body>
  <p class="tex">&nbsp; &nbsp; 量化交易，指的是利用数学模型，在金融市场中寻找稳定超额收益的投资手段。量化交易有着挖掘信息能力强，不易受主观情绪影响，下单及时、准确，风险控制严格等特点，能够获得稳健的收益。而其相对于传统主观投资，上手难度也比较大，门槛较高。入门量化交易，主要需要了解如下几方面的知识。<br></p>
  <p class="tex"><br></p>
  <p class="tex"><span style="text-decoration: underline;color: rgb(255,0,0);">1.数学/统计学知识</span></p>
  <p class="tex"><br></p>
  <p class="tex">&nbsp; &nbsp; 既然说到用数学模型，那数学和统计学的知识是必不可少的。由于国内金融市场尚不完备，一些衍生品交易受到限制，所以相较国外市场，能用到的数学/统计学知识也要少一些。对于非理工背景的投资者，需要补充基础的高等数学，线性代数，概率论，统计学，最优化理论等等学科的知识，这些内容可以在高校教科书中找到。对于一些新兴的利用机器学习的交易策略，还需要了解一些数据挖掘的知识。但既然是入门，这部分自然不是必要的。</p>
  <p class="tex">&nbsp; &nbsp; 另外，计量经济学的应用尤其广泛。进行策略研究时经常要面对大量的时间序列、面板数据。虽然在实践过程中更加注重策略结果，只要能赚钱的策略就是好策略，但在严谨的计量理论的支持下，回归结果更准确，能更好的刻画数据背后的关系，故往往更容易得到与预期相近的结果。其中，时间序列回归与截面、面板回归的逻辑与假设均有较大区别，且广泛用于刻画及预测金融资产的收益，波动。</p>
  <p class="tex">&nbsp; 计量经济学的书籍推荐伍德里奇的<span style="color: rgb(192,0,0);">《计量经济学导论：现代观点》</span>；时间序列推荐布鲁克斯的<span style="color: rgb(192,0,0);">《金融计量经济学导论》</span>。</p>
  <p class="tex"><br></p>
  <p class="tex"><span style="text-decoration: underline;color: rgb(255,0,0);">2.编程能力</span></p>
  <p class="tex"><br></p>
  <p class="tex">&nbsp; &nbsp; 由于量化策略要处理大规模的数据，并采用复杂的数学算法，故需要利用程序来完成这一过程。大部分面向对象的编程语言，如Python，Java，R等都可以胜任这一工作。</p>
  <p class="tex">&nbsp; &nbsp; 我在这里推荐Python，在业界比较主流，其特点主要是包括大量第三方开发的包，如处理数据的Numpy，Pandas，和金融包Talib，和各个平台及其他语言兼容性良好。其中Pandas是美国知名对冲基金AQR开发的数据处理包，非常适合用于金融数据。Python的学习可以通过<span style="color: rgb(192,0,0);">《利用Python进行数据分析》</span>等书籍进行学习，也可以通过一些网上教程快速入门。在实际应用的过程中，应该多参考各个工具包的API文档。</p>
  <p class="tex">回测程序主要包括导入数据及初始化账户，每个交易时间点择时条件、调仓逻辑，及回测结果计算，绘制净值曲线等等。京东量化平台封装的回测环境简化了这一过程，能够方便的对策略进行测试。（<a href="http://quant.jd.com">http://quant.jd.com</a>）</p>
  <p class="tex"><br></p>
  <p class="tex"><span style="text-decoration: underline;color: rgb(255,0,0);">3.金融基础知识</span></p>
  <p class="tex"><br></p>
  <p class="tex">&nbsp; &nbsp; 量化交易，根本上是金融市场中的行为。虽然该岗位对数学、编程知识有要求，但脱离了其金融本质，就无法设计出优秀的策略。量化投资者需要了解各种金融资产的性质，以及影响其价格的因素。对于股票而言，公司的基本面及财务情况，其所处行业的形势能够从某种程度上反映在其股票价格中，因此投资者应对此有基本了解。这部分可以参考博迪，凯恩，马库斯的<span style="color: rgb(192,0,0);">《投资学》</span>，以及财务会计，报表相关书籍。此外，中国市场受到人为操控的因素影响较为显著，在实盘操作中，量化投资者在依赖量化策略进行投资决策的同时，一般也会加入一些主观判断，以更及时捕捉市场走势，获得更高的收益。因此，宏观经济，政策形势对金融市场的影响，也是投资者不能忽视的问题。每天看看华尔街见闻，长久以来可以培养金融直觉。</p>
  <p class="tex"><br></p>
  <p class="tex"><span style="text-decoration: underline;color: rgb(255,0,0);">4.策略研究能力</span></p>
  <p class="tex"><br></p>
  <p class="tex">&nbsp; &nbsp; 即是将以上内容综合运用，将投资思想程序化，开发成为有投资价值的策略的能力。起步时，应多参照已有的较为成熟的策略，进行完善复制。策略本身的逻辑可能三言两语就能概括，但在实际执行的过程中的细节不可忽略。众所周知，在回测中表现突出的策略在实盘中不一定有效，但在回测中效果都不好的策略，难以在实盘重有良好的表现。过度拟合，幸存者偏差和使用未来函数都是新手经常会出现的错误，避免这些错误，才能让回测结果更好的接近真实情况。同时，在得到回测结果后，如何对收益进行归因分析，研究持仓股票，风险暴露，并对参数进行优化，也是量化投资者需要解决的问题。</p>
  <p class="tex">&nbsp; &nbsp; 一些经典的投资策略包括多因子策略（Fama-French三因子模型），技术指标择时（MACD，布林带等），动量反转策略，事件驱动策略，统计套利策略等。其中很多策略源于外国学术论文，高质量学术期刊包括<span style="color: rgb(192,0,0);">Journal of Finance，Journal of Financial Economics</span>等等。同时有一些系统的教学书籍，包括<span style="color: rgb(192,0,0);">《Barra Handbook》</span>（多因子圣经），<span style="color: rgb(192,0,0);">《Quantitative Equity Portfolio Management》</span>（主要讲解投资组合管理），<span style="color: rgb(192,0,0);">《Quantitative Trading Strategies》</span>（主要讲如何构造量化策略）。</p>
  <p class="tex"><br></p>
  <p class="tex"><span style="text-decoration: underline;color: rgb(255,0,0);">5.在实践中学习</span></p>
  <p class="tex"><br></p>
  <p class="tex">&nbsp; &nbsp; 策略回测终究是回测。基于过去行情设计的策略，一定能在过去的时间区间内有良好的表现。但同样的历史不一定会重演，随着市场趋势和微观结构的改变，策略在未来的时间可能不会按照预期的方向发展。实盘中还存在报表信息公布延迟，交易摩擦，下单对市场价格影响等问题。故一个交易策略，在经过严谨全面的回测检验后，要在实盘上检验其真正效果。</p>
  <p class="tex">&nbsp; &nbsp; 在接触量化交易初期，了解数学编程，模型搭建中的细节处理都是绕不开的问题。而如今各种技术手段都较为成熟，可供大家使用，一个成功的投资者与众不同的地方一定在于其设计策略的思想，和对市场的把握。设计交易策略应以背后的金融直觉为基础，是我一直坚信的理念。希望各位投资者能够在量化投资领域中找到自己独特的视角，成为下一个西蒙斯！</p>
  <p class="tex"><br></p>
  <p class="tex">更多资料请访问：<a href="https://www.zhihu.com/question/22211032">https://www.zhihu.com/question/22211032</a> </p>


现在有非常多的关于Quant的书。基础书籍包括：

Hull著《Options Future and Other Derivatives》。这本书被称为Bible。缺点是这本书的内容主要面向MBA而不是Quantitative专家
《Baxter and Rennie》。主要介绍一些手法和诀窍，但主要面向原理而不是实际操作。
Wilmott著《Derivatives》。对PDE介绍的非常不错，但其他方面一般
《The Concepts and Practice of Mathematical Finance》。这本书的目标在于覆盖一个优秀quant应该知道的知识领域。其中包括强列推荐你在应聘工作之前看的一些编程项目。
《C++ Design Patterns and Derivatives Pricing》。这本书是为了告诉大家如何使用C++来做Quant的工作。

随机微积分虽然在第一眼看上去不是很重要，但的确非常有用的。我建议大家先看一些基本理论的书,类似Chung’s books。一些这方面我推荐的书:

Williams著《Probability with Martingales》。一本很容易让人了解Account of discrete time martingale theory的书
Rogers and Williams著《Particularly Volume 1》
