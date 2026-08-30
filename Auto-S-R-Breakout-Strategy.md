
> Name

Auto-S-R-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/44b60d2c6b8099df30b7e8b3cf4beebccd80d0e6c27abe2289a0c09042520ab1.png)

[trans]

## Overview
The automatic support/resistance strategy is a trend following strategy. It determines key support and resistance levels by calculating the highest and lowest prices within a certain period. When the price breaks through these key levels, buy or sell.
## Strategy Principle
This strategy first calculates the highest and lowest prices within a certain number of periods on the left and right sides to determine the main support and resistance levels. Then calculate the highest and lowest prices in a shorter period to determine quick support and resistance levels. When the price breaks through the fast support level, the buying operation is carried out; when the price breaks through the fast resistance level, the selling operation is carried out.
The key logic of the strategy is that after the prices on the left and right sides form support or resistance, if the price breaks through these levels, it is likely to start a new trend. At this time, operations can capture the direction of the trend. This strategy also combines different cycles to determine trends, thereby avoiding short-term momentum affecting judgment.
## Advantage Analysis
The biggest advantage of this strategy is that it can automatically determine key support and resistance levels. There is no need to manually judge the location of support and resistance. At the same time, judging the trend based on different cycles can effectively filter out false breakthroughs and avoid transaction traps.
In addition, the strategy's buying and selling conditions are simple and clear, and only require the price to break through a quick support or resistance level. Easy to implement and easy to backtest optimization parameters.
## Risk Analysis
The biggest risk of this strategy is that the automatically calculated support and resistance levels are not necessarily reliable, and the price may directly break through these levels to form a new trend. This will cause losses.
In addition, if the period of rapid support and resistance level setting is too short, it may result in too many false breakout signals. This will increase actual trading losses.
In order to reduce risks, you can consider filtering in combination with other indicators, such as trading volume, moving average and other indicators to determine the direction. Or manually check the plausibility of automatically calculated support and resistance levels.
## Optimization direction
This strategy can be optimized mainly from two aspects:
1. Optimize the entered period parameters and find the best parameter combination. You can try different combinations of left and right cycles to find the parameters with the highest breakthrough success rate.
2. Add indicator filtering conditions, such as energy indicators, moving averages, etc., to avoid false breakthroughs. It can also be combined with manual judgment of key positions to improve the strategy effect.
## Summarize
This strategy as a whole is a better strategic framework for automatically determining support and resistance levels. Since support and resistance levels are automatically determined, implementation is not difficult and it is suitable for capturing the direction of the trend. At the same time, combined with parameter optimization and conditional filtering, the strategy benefits can be further improved.
||

## Overview  

The Auto S/R strategy is a trend following strategy. It calculates the highest and lowest prices over certain periods to determine key support and resistance levels. When the price breaks through these key levels, buy or sell orders are executed.  

## Strategy Logic

The strategy first computes the highest high and lowest low prices over a number of bars on left and right sides to identify major support and resistance levels. Then it calculates highest high and lowest low prices over a smaller number of bars to determine near-term support and resistance levels. When the price breaks above the near-term support level, a buy order is triggered. When the price breaks below the near-term resistance level, a sell order is triggered.  

The key logic behind the strategy is that if the price breaks supporter or resistance levels formed on both sides over certain periods, it likely signals the start of a new trend. Entering positions in the direction of the breakout allows capturing the emerging trend. The strategy combines different timeframes to confirm the trend, avoiding being misled by short-term price swings.

## Advantage Analysis 

The biggest advantage of this strategy is it can automatically identify key support and resistance levels, eliminating the need for manual price level identification. By combining different timeframes, it can effectively filter out false breakouts, avoiding being trapped in losing positions. 

In addition, the entry and exit rules are simple and straight-forward - just requiring a break of the near-term S/R levels. This makes the strategy easy to implement and optimize by tuning parameters.  

## Risk Analysis

The biggest risk is that automatically calculated S/R levels may not be reliable, and the price could break through without beginning a trend. This could cause losses.  

Also, if the period for near-term S/R is too short, it may generate excessive false signals, leading to high losses in live trading.

To reduce risks, consider adding filter conditions using other indicators like volume and moving averages to confirm trend directionality before entries. Traders could also manually inspect and confirm the reasonableness of automatically calculated S/R levels.  

## Optimization Directions

There are two main aspects this strategy can be optimized:

1. Optimize the input parameters to find the optimal period combinations for highest breakout success rate. Different left and right period mixes could be tested.  

2. Add additional filters like volume/momentum indicators and moving averages to avoid false breakouts. Combining with manual inspection of S/R levels could also improve performance.  

## Summary

Overall this is a solid framework for automatically identifying support and resistance levels. Implementation is straightforward thanks to automated S/R detection, making it suitable for trend following strategies. Further optimizations on parameters and filters can enhance profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|50|Left Bars|
|v_input_int_2|25|Right Bars|
|v_input_int_3|5|Quick Right Bars|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-12-05 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © lukaRT

//@version=5
strategy("Auto S/R Strategy", shorttitle="Auto S/R", overlay=true)

// Ваши входные параметры
leftBars = input.int(50, title="Left Bars")
rightBars = input.int(25, title="Right Bars")
quickRightBars = input.int(5, title="Quick Right Bars")
src = input(close, title="Source")

pivotHigh = ta.pivothigh(src, leftBars, rightBars)
pivotLow = ta.pivotlow(src, leftBars, rightBars)

quickPivotHigh = ta.pivothigh(src, leftBars, quickRightBars)
quickPivotLow = ta.pivotlow(src, leftBars, quickRightBars)

// Ваши уровни сопротивления и поддержки
resistanceLevel1 = ta.valuewhen(quickPivotHigh, high[quickRightBars], 0)
supportLevel1 = ta.valuewhen(quickPivotLow, low[quickRightBars], 0)

// Пересечение ценой уровней
longCondition = ta.crossover(close, supportLevel1)
shortCondition = ta.crossunder(close, resistanceLevel1)

strategy.entry("Long", strategy.long, when=longCondition)
strategy.entry("Short", strategy.short, when=shortCondition)

// Отображение линий сопротивления и поддержки на графике
plot(resistanceLevel1, color=color.red, title="Resistance Level 1")
plot(supportLevel1, color=color.green, title="Support Level 1")

```

> Detail

https://www.fmz.com/strategy/434470

> Last Modified

2023-12-06 16:51:30
