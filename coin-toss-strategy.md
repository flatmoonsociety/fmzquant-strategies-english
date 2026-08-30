
> Name

coin toss strategy
> Author

Lentils
> Strategy Description

Complete T-Shen public account, Lv Shen’s special strategy translation.
The following is the reproduced content,
Please pay more attention to "Qianqian's Quantitative World" to get more strategy source codes!!
Also give yourself an advertisement~
Public account "Lengdouzi's Quantitative Log"
Give everyone a daily public execution and online quantified bankruptcy~
There are many more benefits for you~
--------

Make good use of volatility and outperform the BTC market is that simple!
Original Lu Yangyang Qianqian’s Quantitative World 3 days ago
"The research and development of quantitative strategies actually has two sides. It is very difficult for those who are just getting started. It is not only the code at the "technical" level, but also the strategic and logical thinking at the "strategic" level. Both are important and must not be biased. "




Hello, fellow friends of Qianqian Quantification! ! !


This article is the second issue of specially invited articles. Qianqian is honored to invite Master Lu Yangyang (WeChat ID LE_CHIFFRE1) to introduce to you: how to use the volatility factor to easily outperform the BTC market and achieve "dimensionality reduction strike"!
Lu Shen comes from a traditional quantitative investment institution and has been deeply involved in the currency exchange business. He has rich experience and unique insights in the quantitative field. The content of this issue of Lu Shen covers inspiration, coding implementation, personal insights, etc. It is full of useful information. Qianqian herself felt that she benefited a lot from reading it. She really admires and thanks Lu Shen. I strongly recommend everyone to read it carefully!
Now let’s give a round of applause to Lu Shen to introduce the volatility strategy to everyone.

01

—



introduction


Hello everyone, today I am honored to publish an article on the "Qianqian's Quantification" public account, and I would also like to thank Boss T (one of Qianqian's nicknames) for the invitation. This is my first time writing an article for Boss T. I am completely free to use my spare time after work. Please correct the quality and errors and include them in the article. Thank you all. 

Boss T said to write something quantitative, but he didn’t give any scope. He really didn’t know where to start. Then start with the topics you most enjoy discussing with others. Quantitative indicators and strategies (which can be assisted or automated). Of course, in the end we have to add a cliché: "Investment is risky, so you need to be cautious when entering the market." Strategies only provide ideas and reference for everyone, and you are responsible for your profits and losses. All profits and losses from using this strategy have nothing to do with myself or the main body of the "Qianqian Quantitative World" public account.

Now that the disclaimer is out of the way, let’s get down to business.



02

—



A simple volatility strategy




People who know me well know that personally, I don’t really like Alpha’s gameplay. Relatively speaking, I believe in Beta more and study Beta more. As for why, e.........mmmmm, I don't know how to answer~~, please make up your own mind. If you are interested, you can send a private message or leave a message to the author of the public account. If the logic is clear and distinctive, the author himself will send a small red envelope to everyone.
The research and development of quantitative strategies actually has two sides. It is very difficult for those who are just getting started. It is not only the code at the "technical" level, but also the strategic and logical thinking at the "strategic" level. Both are important and must not be taken in either direction. The strategy I will introduce to you today is actually inspired by a research report from Huatai many years ago. Please read it carefully and it is just an inspiration. The reason why I say this is because the logic of this strategy is completely different from what was mentioned in the research report. Let’s chat with Mr. T privately about the specific research report.
This strategy algorithm adopts the rolling yield fluctuation principle of the logarithmic price rise and fall in a certain period. Based on the fluctuation interval, it calculates the rolling highest value and the minimum value in a certain period. The highest value is used as the upper channel, and the minimum value is used as the lower channel. If it breaks through the upper channel, a position is opened. The rolling average of the upper and lower pipelines is used as the closing line. (Knock on the blackboard here!)
For the specific graphic visualization interface, please refer to the PPT below. This graphic was drawn by me using Pyecharts. Please contact Mr. T privately for the specific code.
 ![IMG](https://www.fmz.com/upload/asset/95f6e8b8196998728de6.png) 



In fact, this strategy was the one I used to build broad-based ETFs before. Of course, it was also used for index timing for stock trading. Later, I moved it directly to the currency circle. I was shocked to find that the parameters did not need to be changed in a real dimensionality reduction attack.


 ![IMG](https://www.fmz.com/upload/asset/95c0d34f79df83ec85c5.png) 





The figure below shows the performance of the backtest that year. The specific code logic screenshots are as follows:

 ![IMG](https://www.fmz.com/upload/asset/951f56f73aeb0da6ffa1.png) 




The above is actually to calculate the indicator data through pandas after reading the data.

 ![IMG](https://www.fmz.com/upload/asset/951a76802f3a22a6da7c.png) 




After the calculation is completed, the data can be output through the pd.to_csv() function and the pyecharts used in the screenshot above can be used for visual output (note: I am using an old version of pyecharts).


All the specific strategies, visualizations, and performance indicator codes are still privately chatted with Mr. T.



03

—

Random talk about quantification


Next I will mainly talk about two points. First: Some people have many questions or say why you people can publish the real strategy. Are you fake liars? Or is it really about saving all sentient beings? Haha~~. First of all, a good strategy is not afraid of disclosure. This is not a weapon development for war-level confrontation, which will determine life and death. Therefore, I and other organizations or individuals are not afraid of so-called strategic secrets, because in my opinion, CTA has no secrets. It’s just ideas that everyone thinks of and doesn’t think of. Secondly, this version is my oldest version. On this basis, I have made several upgrades, such as adding other conditional judgments, stop-profit and stop-loss, etc., and of course, it also includes parameter adjustments for other types of cycles, etc.


Second: Many people, whether they are newbies, already started, or even experienced players, need sources of inspiration, including stock factor mining, timing strategy ideas, etc. These often come from subjective experience, research reports, communication in the circle, etc. It is not ruled out that some purchased strategies on the market can be read and understood, and modified according to their own risk tolerance and specific needs.


Finally, to summarize, quantification is originally an imported product, and programmatic trading is a subset of quantification. As early as when I was in college (around 2009), people have been involved in TB, pyramid and other programs. If we continue to do it today, it can be said that these people who were the first to foresee and foresight have been there for 10 years, and this does not include those who "brought back" high-frequency strategies and systems from Wall Street. Therefore, quantitative strategies or programmatic strategies have been going on in China for some time, but in terms of current market share, participants, and policy support, quantification is still a very small part of the market, even though research reports on multi-factor analysis and strategy modeling are flying everywhere. Some people like to use brainless logic to compare this with the United States, believing that China's quantitative future development trends will be the same as those of the United States, with explosive growth and so on. However, this is not Ruixing’s “coffee and small pot of tea” business logic. China has Chinese characteristics, and the road ahead is still thorny and bumpy. Therefore, we have also gathered a large circle of institutional and individual investors, hoping that everyone can get to know, communicate and grow together, and make a small contribution to this industry.


Finally, I would like to thank the "Qianqian Quantification" public account for its trust in my profession and the invitation to write articles. If you have any specific code and strategy questions, please send a private message to me or Mr. T. I am also in Mr. T’s group.




Finally, thank you again Shen Lu for your wonderful explanation!
Friends who have not joined the quantitative discussion group, please join the group to receive learning materials! ! !
Thousands of deities guard the building!

 ![IMG](https://www.fmz.com/upload/asset/9576f0337a4b9144925e.png) 



Scan on WeChat
Follow this public account
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|tp_first|0.03|tp_first|
|trailing_tp|0.01|trailing_tp|
|st|0.05|st|


> Source (javascript)

``` javascript
/*backtest
start: 2020-01-20 00:00:00
end: 2021-01-19 23:59:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_BitMEX","currency":"XBT_USD","fee":[0.008,0.1]}]
args: [["st",0.1]]
*/

// 初始化
exchange.SetContractType('XBTUSD')
_CDelay(100)
// 止盈止损
var TP_status = false // 是否触发追踪止盈 
var TP_HH = 0
var TP_LL = 0
var B = 1

// 获取交易所信息
function UpdateInfo() {
    account = exchange.GetAccount()
    pos = exchange.GetPosition()
    records = exchange.GetRecords()
    ticker = exchange.GetTicker()
}

// 定制本次盈亏
function Onept() {
    // 更新用户信息
    UpdateInfo()
    // 如果现在余额 大于 之前的余额, 那么 盈利次数+1, 且pt_1设为现在余额
    if (account.Stocks - pt_1 > 0) {
        pt_times = pt_times + 1
        Log('这回赚钱啦~~~~ (＾Ｕ＾)ノ~ＹＯ', account.Stocks - pt_1)
        B = 1
        pt_1 = account.Stocks
    }
    // 如果现在余额 小于 之前的余额, 那么 亏损次数+1, 且pt_1设为现在余额
    if (account.Stocks - pt_1 < 0) {
        st_times = st_times + 1
        Log('这回亏掉了.... /(ㄒoㄒ)/~~', account.Stocks - pt_1)
        B = B * 1.618
        pt_1 = account.Stocks
    }
}

// 画线
function PlotMA_Kline(records) {
    $.PlotRecords(records, "K")
}

// 追踪止盈 初始%, 追踪U
function TP() {
    var TP_first_long = pos[0].Price + tp_first * ticker.Last
    var TP_trailing_long = TP_HH - trailing_tp * ticker.Last
    var TP_first_short = pos[0].Price - tp_first * ticker.Last
    var TP_trailing_short = TP_LL + trailing_tp * ticker.Last
    // 当多仓时, 现价大于开仓+初始止赢价 -> 触发追踪止盈 
    if ((pos[0].Type == 0) && (ticker.Last > TP_first_long)) {
        // Log('当多仓时, 现价大于开仓+初始止赢价 -> 触发追踪止盈', TP_HH)
        TP_status = true
        // 触发追踪止盈, 未初始化开仓最大价格 -> 开仓后最大价格更新为现价
        if (TP_status === true && TP_HH == 0) {
            Log('触发追踪止盈, 未初始化开仓最大价格 -> 开仓后最大价格更新为现价', TP_HH)
            TP_HH = ticker.Last
        }
        // 触发追踪止盈, 已有开仓后最大价格, 现价大于开仓后最大价格 -> 开仓后最大价格更新为现价
        else if (TP_status === true && TP_HH != 0 && ticker.Last > TP_HH) {
            Log('触发追踪止盈, 已有开仓后最大价格, 现价大于开仓后最大价格 -> 开仓后最大价格更新为现价', TP_HH)
            TP_HH = ticker.Last
        }
        // 触发追踪止盈, 已有开仓后最大价格, 现价小于 (开仓后最大价格减 - 回撤USD) -> 开空平仓止盈
        else if (TP_status === true && TP_HH != 0 && ticker.Last < TP_trailing_long) {
            Log('触发追踪止盈, 已有开仓后最大价格, 现价小于 (开仓后最大价格减 - 回撤USD) -> 开空平仓止盈', TP_HH)
            exchange.SetDirection("closebuy")
            exchange.Sell(ticker.Buy, pos[0].Amount, "在" + ticker.Last + "止赢平多仓!! 开仓价格: " + pos[0].Price + "数量: " + pos[0].Amount)
            $.PlotFlag(new Date().getTime(), 'Sell', 'PT_BK' + ticker.Sell)
            Onept()
            TP_status = false
            TP_HH = 0
        }
    }
    // 当空仓时, 现价小于开仓-初始止赢价 -> 触发追踪止盈
    else if ((pos[0].Type == 1) && (ticker.Last < TP_first_short)) {
        // Log('当空仓时, 现价小于开仓-初始止赢价 -> 触发追踪止盈', TP_LL)
        TP_status = true
        // 触发追踪止盈, 未初始化开仓最大价格 -> 开仓后最小价格更新为现价
        if (TP_status === true && TP_LL == 0) {
            Log('触发追踪止盈, 未初始化开仓最大价格 -> 开仓后最小价格更新为现价', TP_LL)
            TP_LL = ticker.Last
        }
        // 触发追踪止盈, 已有开仓后最小价格, 现价小于开仓后最小价格 -> 开仓后最小价格更新为现价
        else if (TP_status === true && TP_LL != 0 && ticker.Last < TP_LL) {
            Log('触发追踪止盈, 已有开仓后最小价格, 现价小于开仓后最小价格 -> 开仓后最小价格更新为现价', TP_LL)
            TP_LL = ticker.Last
        }
        // 触发追踪止盈, 已有开仓后最小价格, 现价大于 (开仓后最小价格减 + 回撤USD) -> 开多平仓止盈
        else if (TP_status === true && TP_LL != 0 && ticker.Last > TP_trailing_short) {
            Log('触发追踪止盈, 已有开仓后最小价格, 现价大于 (开仓后最小价格减 + 回撤USD) -> 开多平仓止盈', TP_LL)
            exchange.SetDirection("closesell")
            exchange.Buy(ticker.Sell, pos[0].Amount, "在" + ticker.Last + "止赢平空仓!! 开仓价格: " + pos[0].Price + "数量: " + pos[0].Amount)
            $.PlotFlag(new Date().getTime(), 'Buy', 'PT_SK' + ticker.Sell)
            Onept()
            TP_status = false
            TP_LL = 0
        }
    }
}

// 止损 %
function Stoploss() {
    // 当多仓时, 现价小于开仓-止损价, 做空平多
    if ((pos[0].Type == 0) && (ticker.Last < pos[0].Price - st * ticker.Last)) {
        Log('当多仓时, 现价小于开仓-止损价, 做空平多')
        exchange.SetDirection("closebuy")
        exchange.Sell(ticker.Buy, pos[0].Amount, "在" + ticker.Last + "止损平多仓!! 开仓价格: " + pos[0].Price + "数量: " + pos[0].Amount)
        $.PlotFlag(new Date().getTime(), 'Sell', 'ST_BK' + ticker.Buy)
        Onept()
    }
    // 当空仓时, 现价大于开仓+止损价, 做多平空
    else if ((pos[0].Type == 1) && (ticker.Last > pos[0].Price + st * ticker.Last)) {
        Log('当空仓时, 现价大于开仓+止损价, 做多平空')
        exchange.SetDirection("closesell")
        exchange.Buy(ticker.Sell, pos[0].Amount, "在" + ticker.Last + "止损平空仓!! 开仓价格: " + pos[0].Price + "数量: " + pos[0].Amount)
        $.PlotFlag(new Date().getTime(), 'Buy', 'ST_SK' + ticker.Sell)
        Onept()
    }
}

// 计算凯利公式 仓位
function PriceAmount() {
    // 赢可以赢多少 
    y = tp_first
    // 输会输多少 
    s = st
    //赔率
    b = y / s
    // 赢的概率
    if (total_times < 10) {
        p = 0.382
    } else {
        p = pt_times / total_times
    }
    // 输的概率
    q = 1 - p
    // 凯莉公式
    f = (b * p - q) / b
    // 限制B最大值
    if (B > 16.18) {
        B = 16.18
    }
    //Amount = _N(Math.abs(f) * account.Stocks * ticker.Last * B, 0)
    Amount = _N(0.618 * account.Stocks * ticker.Last, 0)
    //Log(Amount)
}

// 交易逻辑
function onTick() {
    // 获取均匀分布 0-9 随机数
    ToTheMoon = Math.floor(Math.random() * 10)
    // 无仓位时
    if (pos.length == 0) {
        // Long 
        if (ToTheMoon > 5) {
            exchange.SetDirection("buy")
            exchange.Buy(ticker.Sell, Amount)
            $.PlotFlag(new Date().getTime(), 'Buy', 'BK' + ticker.Sell)
            total_times = total_times + 1
        }
        // Short 
        if (ToTheMoon < 4) {
            exchange.SetDirection("sell")
            exchange.Sell(ticker.Buy, Amount)
            $.PlotFlag(new Date().getTime(), 'Sell', 'SK' + ticker.Buy)
            total_times = total_times + 1
        }
    }
        // 多仓时
    if (pos.length > 0 && pos[0].Type == 0) {
        // 平多 
        if (ToTheMoon < 1) {
            exchange.SetDirection("closebuy")
            exchange.Sell(ticker.Buy, pos[0].Amount)
            $.PlotFlag(new Date().getTime(), 'Sell', 'PBK')
            Onept()
        }
    }
    // 空仓时
    if (pos.length > 0 && pos[0].Type == 1) {
        // 平空 
        if (ToTheMoon > 8) {
            exchange.SetDirection("closesell")
            exchange.Buy(ticker.Sell, pos[0].Amount)
            $.PlotFlag(new Date().getTime(), 'Buy', 'PSK')
            Onept()
        }
    }
}


function main() {
    UpdateInfo()
    // 统计
    pt_1 = account.Stocks
    total_times = 0
    pt_times = 0
    st_times = 0
    while (1) {
        UpdateInfo()
        PriceAmount()
        onTick()
        PlotMA_Kline(records)
        if (pos.length > 0) {
            TP()
        }
        if (pos.length > 0) {
            Stoploss()
        }
        LogStatus("总余额: " + _N(ticker.Last * account.Stocks, 2), " 下单量: " + Amount, " 下单倍数: " + B, " ToTheMoon: " + ToTheMoon, " 下单量比: " + _N(Amount * 100 / _N(ticker.Last * account.Stocks, 2), 2), "% 胜率: " + _N(p * 100, 2), "%", total_times, pos)
    }
}
```

> Detail

https://www.fmz.com/strategy/201007

> Last Modified

2021-01-21 18:16:19
