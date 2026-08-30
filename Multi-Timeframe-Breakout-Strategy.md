
> Name

Multi-Timeframe-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/d612419fa8a63e943aa6ec35ebe75ca70630feaccbec44384f4428dda335b332.png)

[trans]

## Overview
The multi-time frame breakout strategy generates more reliable trading signals by combining price breakout signals on two different time frames. This strategy simultaneously calculates price breakthrough signals on short time frames such as 1 hour, 2 hours, and 3 hours, and longer time frames such as 4 hours and daily. When the signals on the two time frames are in the same direction, a buy or sell signal will be generated to conduct transactions in the corresponding direction.
## Strategy Principle
The core logic of this strategy is to calculate price breakthrough signals on two different time frames, and then perform matching filtering. Specifically, the strategy will calculate whether the price breaks through the specified level on a shorter time frame (such as the 1-hour line), and also calculates whether the price breaks through the specified level on a longer time frame (such as the 4-hour line). The strategy will generate a trading signal only when the breakout signals on both time frames are in the same direction, that is, when the price breaks above a specified level on either time frame, either to the upside or to the downside.
The condition for generating a buy signal is that the closing price or the lowest price on both the short time frame and the long time frame breaks through the corresponding price level. The condition for generating a sell signal is that the closing price or the highest price on both the short and long time frames breaks through the corresponding price levels. Through this multi-time frame matching method, the strategy can filter out some false signals and make the signals more reliable.
## Advantage Analysis
The biggest advantage of this strategy is the high reliability of its trading signals. By requiring prices to break through corresponding levels on both time frames, some noise can be effectively filtered out and wrong trades avoided. In addition, breakout signals on different time frames can verify each other, making trading opportunities more effective. In addition, the strategy provides a certain degree of flexibility, allowing the selection of two combined time frames, as well as data sources, etc., which users can adjust according to their own needs.
## Risk Analysis
The main risk of this strategy is that during the Zeit period when the market is calm, it is easy for the price to not break through on either time frame. At this time, the strategy will not generate any trading signals and trading opportunities may be missed. In addition, there is also a certain time lag between the two time frames, which may cause the signal to be inefficient. In addition, the strategy does not set a stop loss logic, so there is a greater risk.
## Optimization direction
This strategy can be optimized from the following aspects: 1) Add stop-loss logic to control risks; 2) Optimize the combination of time frames to improve trading efficiency; 3) Add more time frames for combinations to make trading signals more stringent; 4) Combine with other indicators for filtering to improve signal quality; 5) Develop an Exiting mechanism to better control profits, etc.
## Summarize
The multi-time frame breakthrough strategy improves signal quality by comparing price breakthroughs on two time frames, and is a more reliable trend following strategy. However, there are also certain flaws, which can be made into a stable and reliable quantitative trading strategy through continuous optimization.
||

## Overview  

The multi timeframe breakout strategy generates more reliable trading signals by combining price breakout signals from two different timeframes. The strategy calculates price breakout signals simultaneously on shorter timeframes such as 1 hour, 2 hours, 3 hours, etc. and longer timeframes such as 4 hours, daily, etc. It will only generate buy or sell signals when the signals from the two timeframes are in the same direction for the execution of corresponding trades.   

## Strategy Logic

The core logic of this strategy is to calculate price breakout signals on two different timeframes respectively and then match them for filtering. Specifically, the strategy will check if prices break certain levels on a shorter timeframe (e.g. 1 hour) and also if prices break corresponding levels on a longer timeframe (e.g. 4 hours). Only when the breakout signals from the two timeframes are in the same direction, that is prices on both timeframes break out upward or downward, will the strategy generate trading signals.   

The condition for a buy signal is that closing prices or low prices on both the shorter and longer timeframes break above their price levels. The condition for a sell signal is that closing prices or high prices on both timeframes break below their levels. By matching signals across timeframes this way, the strategy can filter out some false signals and make the signals more reliable.  

## Advantage Analysis

The biggest advantage of this strategy is the higher reliability of its trading signals. By requiring price breakouts on levels in two timeframes, it can effectively filter out some noise and avoid bad trades. In addition, breakout signals from different timeframes can validate each other, making trading opportunities more efficient. Moreover, the strategy offers some flexibility by allowing users to choose timeframes to combine and data source etc. according to their own needs.  

## Risk Analysis   

The main risk of this strategy is that during calm market Zeitgeists, prices may not break out on either timeframe. In that case, the strategy will not generate any trading signals and may miss opportunities. Also, there is some time lag between the two timeframes which may lead to inefficient signals. Furthermore, the strategy does not include stop loss logic and has larger risks.  

## Optimization Directions

This strategy can be optimized in the following aspects: 1) Add stop loss logic to control risks; 2) Optimize timeframe combinations to improve efficiency; 3) Add more timeframes for combination to make trading signals more strict; 4) Incorporate other indicators for filtration to improve signal quality; 5) Develop exiting mechanisms to better control profits, etc.  

## Conclusion  

The multi timeframe breakout strategy improves signal quality by comparing price breakouts across timeframes and is a relatively reliable trend following strategy. But it also has some flaws. Through constant optimizations, it can become a stable and reliable quantitative trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|Capital, %|
|v_input_4|W|timeframe 1|
|v_input_5|D|timeframe 2|
|v_input_6_ohlc4|0|Source: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|
|v_input_7|true|use saw filter|
|v_input_8|true|гыу color filter|
|v_input_9|true|Show lines|
|v_input_10|1900|From Year|
|v_input_11|2100|To Year|
|v_input_12|true|From Month|
|v_input_13|12|To Month|
|v_input_14|true|From day|
|v_input_15|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-28 00:00:00
end: 2023-12-28 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=3
strategy(title = "Noro's Levels Strategy v1.1", shorttitle = "Levels str 1.1", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Capital, %")
tf1 = input('W', title = "timeframe 1")
tf2 = input('D', title = "timeframe 2")
src = input(ohlc4, "Source")
ap = input(true, defval = true, title = "use saw filter")
cf = input(true, defval = true, title = "гыу color filter")
showlines = input(true, defval = true, title = "Show lines")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Levels
level1 = request.security(syminfo.tickerid, tf1, src)
level2 = request.security(syminfo.tickerid, tf2, src)
col = showlines ? silver : na
p1 = plot(level1, linewidth = 3, color = col, title = "Level 1")
p2 = plot(level2, linewidth = 3, color = col, title = "Level 2")

//Signals
up1 = close > level1 and ap == false ? true : low > level1 ? true : false
dn1 = close < level1 and ap == false ? true : high < level1 ? true : false
up2 = close > level2 and ap == false ? true : low > level2 ? true : false
dn2 = close < level2 and ap == false ? true : high < level2 ? true : false

//Trading
size = strategy.position_size
lot = 0.0
lot := size != size[1] ? strategy.equity / close * capital / 100 : lot[1]

if up1 and up2 and (close < open or cf == false)
    strategy.entry("Long", strategy.long, needlong == false ? 0 : lot, when = (time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
    
if dn1 and dn2 and (close > open or cf == false)
    strategy.entry("Short", strategy.short, needshort == false ? 0 : lot, when = (time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))

if time > timestamp(toyear, tomonth, today, 23, 59)
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/437025

> Last Modified

2023-12-29 16:18:22
