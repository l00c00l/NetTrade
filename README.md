# NetTrade
网格交易策略脚本
本脚本只是针对 ETF拯救世界 在以下地方提到过的闲钱网格的探索测试以及记录，不构成任何建议

策略来源:
* [闲散资金的策略-微博问答 2017-03-22](https://weibo.com/ttwenda/p/show?id=2310684088171439759396)
* [网格说明-雪球 2015年9月2日](https://xueqiu.com/4776750571/55799950)
* [有没有博友愿意为大家做道题？ 2013年8月23日](https://www.chinaetfs.net/?p=895)
* [网格操作记录 2012年6月25日](https://www.chinaetfs.net/?p=757)

数据来源:
* [集思录分享](https://www.jisilu.cn/question/55996)
* [螺丝钉分享](https://xueqiu.com/1997857856/62838103)

计算方法:
* [估值计算方法](http://fund.eastmoney.com/news/1594,20170322722385868.html)

### 策略概述

* 条件A: 低于历史估值均值 20% (每个人计算估值的方法应该是不太一样的，作为小韭菜也没有获取数据的来源，你可以对接自己的数据来源, 这里作为测试先写死一个净值开始)
* 条件B: 还没想好

#### 策略A
1. 假设每网 1000 元
2. 第一网: 达到条件(A或B或者其他，自己定)， 入 1 网
3. 幅度
   * a: 3%
   * b: 5%
4. 下跌: 每达到最近次交易价格的幅度, 每网金额增加 20%，入一网
5. 上涨: 每达到最近次交易价格的幅度, 每网金额减小 20%,  出网
   * 5a: 将低于当前价格买入的份额全部出掉
   * 5b: 买入份额/买入次数 得到一个平均每次买入份数，出掉低于当前价格的买入次数 * 平均每次买入份数

#### 策略B
n = 入网次数-出网次数 (n = 0)
1. 假设每网 1000 元
2. 第一网:  达到条件, 入 1 网 (n = 1)
3. 幅度
   * a: 3%
   * b: 5%
4. 下跌: 每达到最近次交易价格的幅度, 买入 money 金额，money = max((floor(n / 3) + 1) * 每网钱数, 你能接受的一网的最大买入的钱数), 总买入次数 += floor(money / 每网初始价格)
5. 上涨: 每达到最近次交易价格的幅度, 出网
   * 5a: 将低于当前价格买入的份额全部出掉
   * 5b: 买入份额/买入次数 得到一个平均每次买入份数，出掉低于当前价格的买入次数 * 平均每次买入份数
