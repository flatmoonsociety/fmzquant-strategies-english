
> Name

Dual-Moving-Average-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/10960ebad05e95e1f81.png)
 [trans]

## Overview
Dual Moving Average Trend Tracking Strategy is a quantitative trading strategy based on moving averages of two different periods to determine the direction of market trends. This strategy uses the long and short status of the fast moving average and the slow moving average to determine the trend direction and trade in the trend direction.
## Strategy Principle
This strategy uses two moving averages, including a fast moving average (e.g. 10-period) and a slow moving average (e.g. 30-period). If both moving averages are upward, it is judged to be a bullish trend; if both moving averages are downward, it is judged to be a bearish trend.
Specifically, the strategy first calculates a fast moving average and a slow moving average. Then compare the size relationship between the current fast moving average and the previous period. If the current fast moving average is larger than the previous period, the value is assigned to 1, which means upward; otherwise, the value is -1, which means downward. The slow moving average makes the same judgment.
Finally, judge the judgment values ​​of the fast and slow moving averages. If both judgment values ​​are 1, the final judgment is 1, indicating a bullish trend; if both judgment values ​​are -1, the final judgment is -1, indicating a short trend. If the judgment values ​​are inconsistent, the trend judgment of the previous period will be maintained.
After determining the direction of the trend, this strategy opens a long position under the bullish trend and a short position under the bearish trend.
## Advantage Analysis
This strategy has the following advantages:
1. The strategic ideas are clear and simple, easy to understand and implement.
2. Using the combination of double moving averages can effectively filter out the noise that shocks the market and lock in the trend direction.
3. Moving average parameters can be flexibly adjusted to adapt to different varieties and time periods.
4. There is no need to set stop loss and take profit points, which reduces the frequency of transactions and is conducive to tracking trends.
5. You can flexibly set only long or short positions to adapt to different trading preferences.
## Risk Analysis
This strategy also has certain risks:
1. When the price changes sharply, the moving average will lag behind, which may lead to missing the best opportunity to open a position.
2. The double moving average may have false breakthroughs and false crossovers, resulting in erroneous trading signals.
3. The strategy itself does not set stop loss and stop profit, and cannot effectively control a single loss.
4. The strategy defaults to full position trading, which is risky and requires caution.
In order to reduce the above risks, you can set the moving average cycle parameters to be more reasonable, introduce other technical indicators as auxiliary judgments, set stop-loss and stop-profit rules, or adjust positions appropriately.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Increase the selection of moving average types, such as SMA, EMA, etc., and use the diversity of chart indicators. 
2. Add other auxiliary technical indicators, such as MACD, BOLL, etc., to improve the accuracy of judgment.
3. Add trend lines and support and resistance level judgments to make trading signals more accurate.  
4. Set stop-loss and stop-profit conditions to effectively control single losses.
5. Optimize position management and adjust positions according to fund utilization rate, profit rate, etc.
## Summarize
The overall idea of ​​the double moving average trend following strategy is clear and easy to understand. It uses the double moving average to filter shocks, judge the trend direction, and conduct transactions according to the judgment results. It is a typical trend following strategy. This strategy allows you to choose only long or short positions based on personal preference. It is flexible, simple, and easy to operate. At the same time, the strategy also has certain profit risks, and it is necessary to add auxiliary technical indicators, stop loss and take profit, etc. to control risks, so as to obtain long-term stable returns.
||


## Overview  

The Dual Moving Average Trend Tracking Strategy is a quantitative trading strategy that uses two moving averages with different periods to determine the trend direction of the market. It uses the long/short status of fast and slow moving averages to identify the trend and make trades along the trend direction.

## Principles  

The strategy employs two moving averages, including a fast moving average (e.g. 10-period) and a slow moving average (e.g. 30-period). If both moving averages are pointing up, it indicates an uptrend. If both moving averages are pointing down, it indicates a downtrend.   

Specifically, the strategy first calculates the fast and slow moving averages. Then it compares the current fast moving average with previous period to see if the current one is larger than the previous one. If yes, assign value 1 indicating up trend. Otherwise assign -1 for down trend. Do the same for the slow moving average.

Finally, determine the trend by the values of the two moving averages. If both values are 1, final decision is 1, indicating uptrend. If both are -1, final decision is -1, indicating downtrend. If the values are different, maintain previous trend decision.  

Upon the identification of trend direction, the strategy will long at uptrend and short at downtrend.  

## Advantages

The strategy has the following edges:

1. The logic is simple and easy to understand and implement.  
2. The dual moving averages help filter market noise and identify the trend.
3. Parameters of moving averages can be adjusted for different products and timeframes.  
4. No need to set stop loss or take profit, which lowers trade frequency and helps follow the trend.  
5. Can flexibly go long only or short only based on preference.

## Risks  

There are also some risks of the strategy:  

1. Moving averages may lag during sharp price change, causing missing best entry timing.
2. Fake breakout and incorrect crossover may happen, resulting in wrong trading signals.
3. No stop loss is set, unable to effectively limit single trade loss. 
4. Full position by default brings larger risk, needs cautious operation.

To reduce the risks, parameters of moving averages can be set more reasonably, other indicators can be introduced, stop loss and take profit can be set, and position size can be adjusted accordingly.

## Optimization  

The strategy can be further optimized in the following aspects:

1. Add more types of moving averages like SMA and EMA to utilize more charting tools.  
2. Introduce other assisting indicators like MACD and BOLL to improve accuracy.
3. Add trend line and support/resistance analysis for more precise trading signals.   
4. Set stop loss and take profit to control single trade loss.
5. Optimize position sizing based on fund usage, profit ratio etc.  

## Conclusion    

The Dual Moving Average Trend Tracking Strategy has a clear logic of using dual moving averages to filter noise and identify trend, and trade along the trend direction. It's a typical trend following strategy. Traders can choose long only or short only based on preference. There are still some risks of the strategy. Additional indicators, stop loss/take profit should be added to control risks. By doing so, long term steady profit can be achieved.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|10|MA Fast (red)|
|v_input_4|30|MA Slow (blue)|
|v_input_5|0|MA Type: SMA|EMA|
|v_input_6_ohlc4|0|MA Source: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|
|v_input_7|true|Show MAs|
|v_input_8|false|Show Background|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-12 00:00:00
end: 2023-12-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © noro
// 2020

//@version=4
strategy(title = "Noro's TrendMA Strategy", shorttitle = "TrendMA str", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0, commission_value = 0.1)

//Settings
needlong = input(true, title = "Long")
needshort = input(true, title = "Short")
fast = input(10, minval = 1, title = "MA Fast (red)")
slow = input(30, minval = 2, title = "MA Slow (blue)")
type = input(defval = "SMA", options = ["SMA", "EMA"], title = "MA Type")
src = input(ohlc4, title = "MA Source")
showma = input(true, title = "Show MAs")
showbg = input(false, title = "Show Background")

//MAs
fastma = type == "EMA" ? ema(src, fast) : sma(src, fast)
slowma = type == "EMA" ? ema(src, slow) : sma(src, slow)

//Lines
colorfast = showma ? color.red : na
colorslow = showma ? color.blue : na
plot(fastma, color = colorfast, title = "MA Fast")
plot(slowma, color = colorslow, title = "MA Slow")

//Trend
trend1 = fastma > fastma[1] ? 1 : -1
trend2 = slowma > slowma[1] ? 1 : -1
trend = 0
trend := trend1 == 1 and trend2 == 1 ? 1 : trend1 == -1 and trend2 == -1 ? -1 : trend[1]

//Backgrouns
colbg = showbg == false ? na : trend == 1 ? color.lime : trend == -1 ? color.red : na
bgcolor(colbg, transp = 80)

//Trading
if trend == 1
    if needlong
        strategy.entry("Long", strategy.long)
    if needlong == false
        strategy.close_all()

if trend == -1
    if needshort
        strategy.entry("Short", strategy.short)
    if needshort == false
        strategy.close_all()
    
```

> Detail

https://www.fmz.com/strategy/435881

> Last Modified

2023-12-19 14:49:52
