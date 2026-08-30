
> Name

Moving-Average-Pullback-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1213ad75ab8adb96cbf.png)

[trans]

## Overview
Moving Average Pullback Trading Strategy is a strategy for trading in the direction of the trend. It uses the relationship between long-term and short-term moving averages to determine the overall trend direction, and buys on dips during short-term retracements, closing positions with stop-loss and take-profit targets.
## Strategy Principle
The main judgment rules of this strategy are:
1. When the closing price is above the long-term moving average, it is confirmed that the current market is in a long position and the conditions for opening a position are met.
2. A short-term retracement occurs when the closing price drags from above the short-term moving average to below the short-term moving average.
3. If the RSI indicator is less than 30 at this time, it is considered to be oversold, forming a buy signal.
4. Establish a long position, set the stop loss to less than 5% of the entry price, and set the take profit to more than 10% of the entry price
Through such combined judgment, we can take advantage of short-term adjustment opportunities to establish positions on the premise that the trend direction is in line with expectations.
## Strategic Advantages
The biggest advantage of this strategy is that it only conducts long transactions in anticipation of an upward general trend, which can effectively avoid the risk of market shock. At the same time, it uses the opportunity of the short-term average pullback to pursue purchases, which can enter the market at a better price.
In addition, this strategy has a stop-loss and take-profit mechanism. This allows even if the judgment is wrong and a reverse market occurs, the loss can be controlled by stop loss; and after making a profit, part of the profit can be locked in by stop loss.
## Strategy Risk
Although this strategy takes into account the general trend judgment and stop-loss and take-profit settings, there are still certain risks:
1. Risk of incorrect judgment of long-term trends. When it is judged that the market has entered a long market and a long position is opened, but in fact the market has turned from long to volatile or short, this will cause greater losses.
2. The risk of the stop loss being exceeded. Especially when major negative events occur, the market may gap down and exceed the pre-set stop loss line, resulting in uncontrollable losses.
Correspondingly, we can consider the following methods to reduce risks:
1. Do a good job in market analysis and avoid misjudging trends in the volatile range. Or set a longer period moving average to confirm the general trend.
2. Use conditional orders to trigger liquidation when the market jumps and falls, instead of a simple stop loss order. This can prevent the stop loss order from being chased through to a certain extent.
## Strategy optimization
Considering that the characteristics of this strategy are long-term judgment and short-term entry, we can further optimize from the following aspects:
1. Optimize the period parameters of the moving average and find the best parameter combination
2. Add other indicator judgments. For example, add trading volume analysis, or combine other overbought and oversold indicators based on the RSI indicator.
3. Adjust the stop loss and take profit range in real time. We can make adaptive adjustments according to the degree of market fluctuations and appropriately relax the stop loss range when there are large fluctuations.
4. Test the adaptability of different target varieties. This type of strategy may be more suitable for index products. If used for individual stocks, other screening rules need to be added.
## Summarize
The moving average pullback trading strategy is generally a relatively mature and stable strategy idea. It mainly considers the general trend and short-term correction opportunities, and obtains better entry opportunities without chasing higher prices. At the same time, lock in profits and control risks through stop loss and take profit settings. This strategy is particularly suitable for investors with strong comprehensive analysis capabilities and rich trading experience.
||


## Overview

The moving average pullback trading strategy is a trend-following strategy. It utilizes the relationship between long-term and short-term moving averages to determine the overall trend direction and makes long entries during short-term pullbacks when prices are relatively low.  

## Strategy Logic

The key decision rules of this strategy are:

1. When the closing price is above the long-term moving average, it confirms an upward trend that meets the opening position criteria  
2. When the closing price pulls back from above the short-term moving average to below the short-term moving average, there is a short-term pullback
3. At this time, if the RSI indicator is less than 30, it is considered oversold and a buy signal is generated
4. Establish a long position with the stop loss set below 5% of the entry price and take profit set above 10% of the entry price

With such combined criteria, we can establish positions during short-term pullbacks while the trend direction matches expectations.

## Advantages of the Strategy

The biggest advantage of this strategy is that it only carries out long trades in an expected upward trend, which can effectively avoid the risk of a volatile market. At the same time, it chases the buy on the pullback of the short-term moving average, which allows entering the market at a relatively better price.

In addition, the strategy has set up mechanisms for stop loss and take profit. This allows us to control losses through stop loss even if the judgment is wrong and the market moves in the opposite direction; for profits, take profit allows locking in some gains.

## Risks of the Strategy  

Although this strategy considers the major trend judgment and sets up stop loss and take profit, there are still certain risks:

1. Risk of incorrect judgment of the major trend. When judging that the market has entered a bull market after opening long positions, the actual market has turned from bullish to sideways or bearish, which will cause huge losses.

2. The risk of stop loss being penetrated. Especially when major negative events occur, the market may gap down beyond the predetermined stop loss line, resulting in uncontrollable losses.

Accordingly, we can consider the following methods to mitigate risks:

1. Make good analyses of the general market to avoid misjudging the trend in the shock zone. Or set longer cycle moving averages to confirm the major trend. 

2. Adopt conditional orders which get triggered on gap-down moves instead of simple stop loss orders. This can prevent stop loss orders from being penetrated to some extent.   

## Strategy Optimization

Considering the characteristics of this strategy with long-term judgment and short-term entry, we can further optimize it in the following aspects:  

1. Optimize the cycle parameters of moving averages to find the best parameter combination

2. Increase other technical indicator filters. Such as adding volume analysis, or combining other overbought-oversold indicators on the basis of RSI

3. Dynamically adjust the stop loss and take profit range. We can make adaptive adjustments based on market volatility, appropriately widening the stop loss range during high volatility periods  

4. Test adaptiveness across different products. This type of strategy may be more suitable for index products. Additional filters are needed when applied to individual stocks.

## Conclusion

In general, the moving average pullback trading strategy is a relatively mature and steady strategy idea. It mainly considers the major trend and chances for short-term pullbacks, obtaining good entry opportunities without chasing new highs. At the same time, it locks in profits and controls risks through stop loss and take profit settings. This strategy is especially suitable for investors with strong comprehensive analytical capabilities and rich trading experience.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|200|(?パラメータ) long term moving average BASE200/period of long term sma|
|v_input_int_2|10|Long-term moving average BASE10/period of short term sma|
|v_input_int_3|5|stoploss percentages|
|v_input_int_4|20|利食いの合合%/take profit percentages|
|v_input_1|timestamp(01 Jan 2000 13:30 +0000)|(?Period)バックテストを开户める日/start trade day|
|v_input_2|timestamp(1 Jan 2099 19:30 +0000)|Finish date day|

> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-30 00:00:00
end: 2023-12-06 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © tsujimoto0403

//@version=5
strategy("simple pull back", overlay=true,default_qty_type=strategy.percent_of_equity,
     default_qty_value=100)

//input value 
malongperiod=input.int(200,"長期移動平均BASE200/period of long term sma",group = "パラメータ")
mashortperiod=input.int(10,"長期移動平均BASE10/period of short term sma",group = "パラメータ")
stoprate=input.int(5,title = "損切の割合％/stoploss percentages",group = "パラメータ")
profit=input.int(20,title = "利食いの割合％/take profit percentages",group = "パラメータ")
startday=input(title="バックテストを始める日/start trade day", defval=timestamp("01 Jan 2000 13:30 +0000"), group="期間")
endday=input(title="バックテスを終わる日/finish date day", defval=timestamp("1 Jan 2099 19:30 +0000"), group="期間")


//polt indicators that we use 
malong=ta.sma(close,malongperiod)
mashort=ta.sma(close,mashortperiod)

plot(malong,color=color.aqua,linewidth = 2)
plot(mashort,color=color.yellow,linewidth = 2)

//date range 
datefilter = true

//open conditions
if close>malong and close<mashort and strategy.position_size == 0 and datefilter and ta.rsi(close,3)<30 
    strategy.entry(id="long", direction=strategy.long)
    
//sell conditions 
strategy.exit(id="cut",from_entry="long",stop=(1-0.01*stoprate)*strategy.position_avg_price,limit=(1+0.01*profit)*strategy.position_avg_price)


if close>mashort and close<low[1] and strategy.position_size>0
    strategy.close(id ="long")
        



```

> Detail

https://www.fmz.com/strategy/434610

> Last Modified

2023-12-07 18:09:27
