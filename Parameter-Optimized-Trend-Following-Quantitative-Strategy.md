
> Name

Parameter-Optimized-Trend-Following-Quantitative-Strategy based on parameter optimization
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/a800a2f343d0bc3580.png)
[trans]

## Overview
The main idea of ​​this strategy is to combine the percentrank indicator and parameter optimization to realize the judgment and tracking of price trends. This strategy generates trading signals by comparing the current price with the price percentage within a certain historical period to capture the intermediate mirror effect, track the trend, and obtain excess returns.
## Strategy Principle
This strategy uses the percentrank indicator to determine price trends. percentrank represents the relative strength of the current price over the viewing period. The parameter len represents the length of the historical period to be viewed.
The value range of percentrank is between 0 and 100. When the percentrank value is close to 0, it means that the current price is close to the lowest price in the viewing period, and it belongs to the undervalued area; when it is close to 100, it means that the current price is close to the highest price in the viewing period, and it belongs to the overvalued area.
This strategy also introduces the scale parameter as an offset. Move the interval from 0 to 100 to the interval from scale to 100+scale. Set two signal lines level_1 and level_2 at the same time. Among them, level_1 represents the bullish level, and level_2 represents the bearish level.
A bullish signal is generated when the price percentrank indicator crosses level_1 from bottom to top; a bearish signal is generated when the price crosses level_2 from top to bottom. The closing conditions are opposite to the entry signals.
## Strategic Advantages
1. Use the percentrank indicator to determine the strength of the price trend to avoid being trapped and chasing highs.
2. Apply the parameter optimization method, adjust the offset scale and signal line threshold, and adjust parameters for different varieties and cycles to improve stability.
3. Combine trend following and reversal trading ideas, and follow the trend in time after breaking through the signal line
## Risk Analysis
1. Misjudgment of trends leads to unnecessary losses
2. When the price fluctuation trend is not obvious, it is easy to generate wrong signals
3. Improper parameter settings may lead to frequent transactions or insufficient transaction volume.
For the above risks, you can optimize by adjusting the parameters len, scale, and level settings; at the same time, you can combine other indicators as confirmation to avoid wrong transactions.
## Optimization direction
There is room for further optimization of this strategy:
1. Stop loss points can be introduced to reduce single losses
2. It can be confirmed by combining indicators such as moving averages to filter out some false signals.
3. Can be combined with machine learning methods to automatically optimize parameters
4. Can run in parallel in multiple time periods
## Summarize
The overall idea of ​​this strategy is clear, and it uses quantitative methods of parameter optimization to judge and track price trends. It has certain practical value, but it still needs further testing and optimization to reduce practical risks and improve stable profitability.
||

## Overview

The main idea of this strategy is to judge and track price trends by combining the percentrank indicator and parameter optimization. The strategy generates trading signals by comparing the current price with the percentage of prices over a certain historical period to capture the mirror effect and track trends for excess returns.

## Strategy Principle    

The strategy uses the percentrank indicator to determine price trends. Percentrank represents the relative strength of the current price over the viewed period. The parameter len indicates the length of the historical period to view.

The range of percentrank values is from 0 to 100. When the percentrank value is close to 0, it means the current price is near the lowest price in the viewed period and is in an undervalued area. When it is close to 100, it means the current price is near the highest price in the viewed period and is in an overvalued area.

The strategy also introduces a scale parameter as an offset to move the 0 to 100 range to the scale to 100+scale range. Two signal lines level_1 and level_2 are also set, where level_1 indicates the long level and level_2 indicates the short level. 

When the price percentrank indicator crosses level_1 upwards, a long signal is generated. When it crosses level_2 downwards, a short signal is generated. The exit conditions are opposite of the entry signals.

## Advantages of the Strategy  

1. Use percentrank indicator to determine the strength of price trends, avoiding being trapped or chasing highs
2. Apply parameter optimization methods to adjust offset scale and signal line threshold for different products and cycles to improve stability 
3. Combine trend following and mean reversion trading ideas to track trends in a timely manner after breaking through the signal line

## Risk Analysis   

1. Incorrect judgment of trends resulting in unnecessary losses
2. Prone to generating wrong signals when price volatility and trend are unclear
3. Improper parameter settings may lead to too frequent trading or insufficient trading volume

To address the above risks, parameters like len, scale, level can be adjusted for optimization. Other indicators can also be incorporated for confirmation to avoid erroneous trades.

## Optimization Directions

There is room for further optimization of the strategy:

1. Stop loss points can be introduced to reduce single trade loss
2. Indicators like moving average can be incorporated for confirmation to filter out some wrong signals  
3. Machine learning methods can be used to automatically optimize parameters
4. Can run in parallel across multiple time frames

## Conclusion  

The overall idea of the strategy is clear, applying quantitative methods of parameter optimization to judge and track price trends. It has some practical value but still needs further testing and optimization to reduce risks and improve stable profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|10|lookback - Период сравнения|
|v_input_3|50|scale offset - смещение шкалы|
|v_input_4|30|sygnal line 1|
|v_input_5|-30|sygnal line 2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-02 00:00:00
end: 2024-01-01 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Alex_Dyuk

//@version=4
strategy(title="percentrank", shorttitle="percentrank")
src = input(close, title="Source")
len = input(title="lookback - Период сравнения", type=input.integer, defval=10, minval=2)
scale = input(title="scale offset - смещение шкалы", type=input.integer, defval=50, minval=0, maxval=100)
level_1 = input(title="sygnal line 1", type=input.integer, defval=30)
level_2 = input(title="sygnal line 2", type=input.integer, defval=-30)

prank = percentrank(src,len)-scale
plot(prank, style = plot.style_columns)
plot(level_2, style = plot.style_line, color = color.red)
plot(level_1, style = plot.style_line, color = color.green)

longCondition = (crossunder(level_1, prank) == true)
if (longCondition)
    strategy.entry("Long", strategy.long)
longExitCondition = (crossover(level_2, prank) == true)
if (longExitCondition)
    strategy.close("Long")
    
shortCondition = (crossover(level_2, prank) == true)
if (shortCondition)
    strategy.entry("Short", strategy.short)
shortexitCondition = (crossunder(level_1, prank) == true)
if (shortexitCondition)
    strategy.close("Short")

    
```

> Detail

https://www.fmz.com/strategy/437383

> Last Modified

2024-01-02 11:01:22
