
> Name

Dual-Moving-Average-Breakout-Strategy Dual-Moving-Average-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c67bdc37d01cc6b423.png)
[trans]
## Overview
The double moving average breakthrough strategy is a typical quantitative trading strategy that follows trends. This strategy determines positions by calculating simple moving averages of different periods and setting trading signals when the price breaks through the moving average. This strategy uses the 20-day line and the 60-day line as trading signals.
## Strategy Principle
The core logic of the double moving average breakthrough strategy is to use moving averages of different periods to capture price trends and send trading signals when the price breaks through the moving averages.
Specifically, the 20-day simple moving average and the 60-day simple moving average are used in this strategy. These two moving averages can be regarded as tools for capturing short-term trends and medium- and long-term trends respectively. When the short-term price breaks through the medium- and long-term price, it means that it is currently in an upward trend, and you should go long; when the short-term price falls below the medium- and long-term price, it means that it is currently in a downward trend, and you should reduce your position.
The code uses `ta.crossover` and `ta.crossunder` to determine whether the price breaks or falls below a moving average. When a breakthrough occurs, a long or lighten order is issued.
## Strategic Advantages
The double moving average breakthrough strategy has the following advantages:
1. The concept is simple, easy to understand and implement.
2. Can effectively track market trends and avoid being affected by noise.
3. The strategy has few parameters and is easy to optimize.
4. The moving average cycle can be flexibly selected to adjust the sensitivity to the market.
## Strategy Risk
The double moving average breakout strategy also has some risks:
1. When the market is in a volatile trend, many false signals will be generated. This can be alleviated by increasing the holding period.
2. Unable to effectively capture rapidly reversing markets. Can be combined with other indicators as filters.  
3. Moving averages are inherently lagging and cannot respond to price changes in advance. The improvement cycle can be appropriately shortened.
## Strategy optimization direction
The double moving average breakthrough strategy can be optimized from the following dimensions:
1. Optimize the period parameters of the moving average and find the best parameter combination.
2. Add other indicator judgments to avoid false signals. For example, MACD, KD, etc. 
3. Add stop loss logic.
4. Combine with more time period analysis to achieve multiple time frames.
## Summarize
The double moving average breakout strategy is a simple and practical trend following strategy. It can effectively capture medium and long-term trends while avoiding the interference of short-term market noise. At the same time, the strategy is easy to understand and implement, with only a few parameters, which is very suitable for the requirements of quantitative trading. Of course, there is also some room for improvement in the strategy, which can be improved by optimizing parameters, adding signal filtering and stop-loss logic, etc., to make the strategy more stable and profitable.
||

## Overview

The dual moving average breakout strategy is a typical trend following quantitative trading strategy. It generates trading signals by calculating simple moving averages of different periods and checking if the price breaks through them to determine positions. This strategy uses 20-day and 60-day moving averages as trading signals.  

## Strategy Logic

The core logic of the dual MA strategy is to **use moving averages of different periods to capture price trends and generate trading signals when the price breaks through the moving averages**.  

Specifically, this strategy employs 20-day and 60-day simple moving averages. These two moving averages can be seen as tools to capture short-term and medium-long term trends respectively. When the short term price breaks through the medium-long term price, it signals that the market is in an upward trend and thus should go long. When the short term price drops below the medium-long term price, it signals that the market is in a downward trend and thus positions should be reduced.

The code uses `ta.crossover` and `ta.crossunder` to determine if the price has broken through or dropped below a moving average. Trading signals of going long or reducing position are emitted accordingly when a breakout happens.  

## Advantages

The dual moving average breakout strategy has the following advantages:

1. The concept is simple and easy to understand and implement.  
2. It can effectively track market trends and avoid noise interference.
3. Few strategy parameters and easy to optimize.  
4. Flexible in choosing moving average periods to adjust market sensitivity.

## Risks

There are also some risks with the strategy:

1. Prone to whipsaws when market is ranging. Can be alleviated by increasing holding period.
2. Ineffective in catching quick market reversals. Other indicators can be added as filters.
3. Moving averages inherently lagging, unable to early signal price changes. Shortening period may help.

## Enhancement Areas

The strategy can be enhanced from the following dimensions:  

1. Optimize moving average periods to find best parameter sets.
2. Add other indicators to filter out false signals, e.g. MACD, KD etc.  
3. Add stop loss logic.  
4. Incorporate multi-timeframe analysis for robustness.

## Summary

The dual moving average breakout strategy is a simple and practical trend following strategy. It can effectively capture medium-long term trends while avoiding short-term market noise. Also, the easy-to-understand logic and limited parameters make it very suitable for quantitative trading. Of course there are rooms for improvements, such as parameter tuning, signal filtering and stop loss to make it more stable and profitable.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2018|backtest_year|
|v_input_int_1|true|backtest_month|
|v_input_int_2|true|backtest_day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-04 00:00:00
end: 2024-02-03 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Astorhsu

//@version=5
strategy("Astor SMA20/60", overlay=true)
backtest_year = input(2018, title='backtest_year') //回測開始年分
backtest_month = input.int(01, title='backtest_month', minval=1, maxval=12) //回測開始月份
backtest_day = input.int(01, title='backtest_day', minval=1, maxval=31)  //回測開始日期
start_time = timestamp(backtest_year, backtest_month, backtest_day, 00, 00)  //回測開始的時間函數

//Indicators
sma10 = ta.sma(close,10)
sma20 = ta.sma(close,20)
sma60 = ta.sma(close,60)
plot(sma20, color=color.green, title="sma(20)")
plot(sma60, color=color.red, title="sma(60)")

//進場條件
// trend1 = sma60 > sma20 //假設目前趨勢為60>20
longCondition = ta.crossover(close, ta.sma(close, 20))
if (longCondition) 
    strategy.entry("open long20", strategy.long, qty=1, comment="站上m20做多")


shortCondition = ta.crossunder(close, ta.sma(close, 20))
if (shortCondition) 
    strategy.close("open long20",comment="跌破m20平倉", qty=1)     
    
longCondition1 = ta.crossover(close, ta.sma(close, 60))
if (longCondition1) 
    strategy.entry("open long60", strategy.long, qty=1, comment="站上m60做多")


shortCondition1 = ta.crossunder(close, ta.sma(close, 60))
if (shortCondition1) 
    strategy.close("open long60",comment="跌破m60平倉", qty=1)     
    
// longCondition2 = ta.crossover(close, ta.sma(close, 10))
// if (longCondition2) 
//     strategy.entry("open long10", strategy.long, qty=1, comment="站上m10做多")


// shortCondition2 = ta.crossunder(close, ta.sma(close, 10))
// if (shortCondition2)
//     strategy.close("open long10",comment="跌破m10平倉", qty=1)   

```

> Detail

https://www.fmz.com/strategy/441003

> Last Modified

2024-02-04 16:06:46
