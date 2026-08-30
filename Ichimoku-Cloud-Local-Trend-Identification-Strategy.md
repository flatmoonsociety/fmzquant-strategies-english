
> Name

Ichimoku-Cloud-Local-Trend-Identification-Strategy in one article
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/112e2be4f18be94e608.png)
[trans]

## Overview
This strategy is a trend identification and trading strategy designed based on the Ichimoku Cloud indicator and the Fibonacci Ratio. The strategy uses the Conversion Line, Base Line, Kumo Cloud and Lagging Span in Yiwen Cloud indicators to determine the current market trend, and combines the two golden ratios of 1.618 and 0.618 to set stop loss levels and identify volatile markets. In addition, the strategy also introduces two additional midlines to filter out false signals.
## Strategy Principle
Yiwen Cloud indicator consists of four parts: conversion line, baseline, cloud and delay line. Among them, the conversion line and the baseline are calculated from the average of the highest price and the lowest price in different periods respectively. The cloud is formed by the baseline moving forward for 26 periods, and the delay line is the closing price moving backward for 26 periods.
The long position opening conditions for this strategy are as follows:
1. The delay line is above the cloud
2. The conversion line is higher than the baseline
3. The closing price is above the 1.618 stop loss level
4. The 0.618 line is higher than the 1.618 stop loss level
5. The closing price is above the cloud
The conditions for opening a short position are opposite to those for a long position.
The stop loss position is set using two golden ratios of 1.618 and 0.618. The long stop loss position is the upper edge of the cloud minus 1.618 times the distance between the upper and lower edges, and the short stop loss position is the opposite. The 0.618 line is used to identify a volatile market. When the cloud is green and the 0.618 line is lower than the 1.618 stop loss level, the market is considered to be in a volatile state.
In addition to the Yiwenyun indicator, this strategy also introduces two midlines to filter out false signals. The midline is calculated from the average of the highest and lowest prices for different periods.
## Advantage Analysis
1. Using price and trend indicators simultaneously can better identify current market trends.
2. Introduce the golden ratio to dynamically set the stop loss level, and the risk is controllable.
3. The 0.618 line can effectively identify volatile markets and avoid frequent opening of positions in volatile markets.
4. Two additional center lines can further filter out false signals and improve signal quality.
5. The parameters are adjustable and suitable for different markets and cycles.
## Risk Analysis
1. In extreme market conditions, such as sharp rises and plummets, trend indicators may fail, resulting in signal distortion.
2. The stop loss position is calculated based on the distance of the cloud. When the cloud is very thin, the stop loss may be too close to the opening price.
3. The golden ratio stop loss and 0.618 line methods for judging market shocks lack theoretical support and may not be applicable to all markets.
4. Parameter optimization may lead to overfitting and poor performance in the actual market.
## Optimization direction
1. You can consider introducing more trend confirmation indicators, such as moving average systems, MACD, etc., to further improve signal quality.
2. The setting of stop loss level can take into account more factors, such as ATR, volatility, etc., making it more dynamic and personalized.
3. For the judgment of the volatile market, you can try other methods, such as the trend strength indicator ADX, etc.
4. Parameter optimization can use machine learning methods such as genetic algorithms, and conduct out-of-sample testing to avoid overfitting.
5. Position management and risk control modules can be added, such as Kelly criteria, fixed risks, etc., to improve the robustness and reliability of the strategy.
## Summarize
This strategy innovatively combines the Yiwenyun indicator and the golden ratio to form a complete trend identification and trading system. At the same time, introducing additional midline filtering can improve signal quality to a certain extent. The advantage of the strategy is that it can better adapt to the two market conditions of trend and shock, and control risks through dynamic stop loss. However, the strategy also has some shortcomings, such as lack of theoretical support, parameter optimization may be over-fitting, etc. In the future, the strategy can be improved by introducing more indicators, optimizing stop loss and position management, and optimizing machine learning parameters. In general, this strategy is novel and has certain reference value, but it requires further testing and optimization in practical applications.
|| 

## Overview

This strategy is a trend identification and trading strategy based on the Ichimoku Cloud indicator combined with Fibonacci Ratios. It uses the Conversion Line, Base Line, Kumo Cloud, and Lagging Span from the Ichimoku Cloud indicator to determine the current market trend, and incorporates the 1.618 and 0.618 Fibonacci Ratios to set stop-loss levels and identify sideways markets. Additionally, the strategy introduces two extra mid-lines to filter out false signals.

## Strategy Principle

The Ichimoku Cloud indicator consists of four components: the Conversion Line, Base Line, Kumo Cloud, and Lagging Span. The Conversion Line and Base Line are calculated using the average of the highest high and lowest low over different time periods. The Kumo Cloud is formed by shifting the Base Line forward by 26 periods, and the Lagging Span is the closing price shifted backwards by 26 periods.

The long entry conditions for this strategy are as follows:

1. The Lagging Span is above the cloud
2. The Conversion Line is greater than the Base Line
3. The closing price is above the 1.618 stop-loss level
4. The 0.618 line is above the 1.618 stop-loss level 
5. The closing price is above the cloud

The short entry conditions are the opposite of the long entry conditions.

The stop-loss levels are set using the 1.618 and 0.618 Fibonacci Ratios. For long positions, the stop-loss is the upper edge of the cloud minus 1.618 times the distance between the upper and lower edges. For short positions, it is the opposite. The 0.618 line is used to identify sideways markets. When the cloud is green and the 0.618 line is below the 1.618 stop-loss level, the market is considered to be in a sideways state.

In addition to the Ichimoku Cloud indicator, the strategy introduces two mid-lines to further filter out false signals. The mid-lines are calculated using the average of the highest high and lowest low over different time periods.

## Advantage Analysis

1. By using both price and trend indicators, the strategy can better identify the current market trend.
2. Introducing Fibonacci Ratios to dynamically set stop-loss levels makes risk controllable.
3. The 0.618 line can effectively identify sideways markets and avoid frequent entries in ranging markets.
4. The two extra mid-lines can further filter out false signals and improve signal quality.
5. Parameters are adjustable, making the strategy suitable for different markets and timeframes.

## Risk Analysis

1. In extreme market conditions, such as strong uptrends or downtrends, trend indicators may fail, leading to distorted signals.
2. The stop-loss level is based on the distance of the cloud. When the cloud is very thin, it may result in the stop-loss being too close to the entry price.
3. The method of using Fibonacci Ratios for stop-loss and the 0.618 line to judge sideways markets lacks theoretical support and may not be applicable to all markets.
4. Parameter optimization may lead to overfitting and poor performance in real markets.

## Optimization Directions

1. Consider introducing more trend confirmation indicators, such as moving averages, MACD, etc., to further improve signal quality.
2. The setting of stop-loss levels can take into account more factors, such as ATR and volatility, to make them more dynamic and personalized.
3. For identifying sideways markets, other methods such as the ADX trend strength indicator can be tried.
4. Machine learning methods such as genetic algorithms can be used for parameter optimization, and out-of-sample testing should be conducted to avoid overfitting.
5. Position sizing and risk control modules can be added, such as the Kelly Criterion and fixed risk, to improve the robustness and reliability of the strategy.

## Conclusion

This strategy innovatively combines the Ichimoku Cloud indicator with Fibonacci Ratios to form a complete trend identification and trading system. The introduction of extra mid-lines for filtering can improve signal quality to a certain extent. The strategy's advantage lies in its ability to adapt well to both trending and ranging market conditions, and to control risk through dynamic stop-losses. However, the strategy also has some shortcomings, such as lack of theoretical support and potential overfitting in parameter optimization. In the future, the strategy can be improved by introducing more indicators, optimizing stop-losses and position sizing, and using machine learning for parameter optimization. Overall, this strategy has an innovative approach and is worth referencing, but further testing and optimization are needed for practical application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|9|Conversion Line Length|
|v_input_int_2|26|Base Line Length|
|v_input_int_3|52|Leading Span B Length|
|v_input_int_4|17|PPL1|
|v_input_int_5|39|PPL2|
|v_input_int_6|26|Lagging Span|
|v_input_float_1|1.618|Mult1|
|v_input_float_2|0.618|Mult2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-03-13 00:00:00
end: 2024-03-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © manoharbauskar

//@version=5
// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © manoharbauskar

//@version=5
strategy("Advanced_Ichimoku_Cloud_Strategy", overlay=true, margin_long=100, margin_short=100)
conversionPeriods = input.int(9, minval=1, title="Conversion Line Length")
basePeriods = input.int(26, minval=1, title="Base Line Length")
laggingSpanPeriods = input.int(52, minval=1, title="Leading Span B Length")
pivotPeriods1 = input.int(17,minval = 1,title = "PPL1")
pivotPeriods2 = input.int(39,minval = 1,title = "PPL2")
displacement = input.int(26, minval=1, title="Lagging Span")
donchian(len) => math.avg(ta.lowest(len), ta.highest(len))
conversionLine = donchian(conversionPeriods)
baseLine = donchian(basePeriods)
midLine1 = donchian(pivotPeriods1)
midLine2 = donchian(pivotPeriods2)
midLine3 = donchian(laggingSpanPeriods)
leadLine1 = math.avg(conversionLine, baseLine, midLine1)
leadLine2 = math.avg(midLine2 , midLine3)


plot(conversionLine, color=#2962FF, title="Conversion Line")
plot(baseLine, color=#B71C1C, title="Base Line")

plot(close, offset = -displacement + 1, color=color.yellow, title="Lagging Span")
p1 = plot(leadLine1, offset = displacement - 1, color=#A5D6A7,
	 title="Leading Span A")
p2 = plot(leadLine2, offset = displacement - 1, color=#EF9A9A,
	 title="Leading Span B")
   
plot(leadLine1 > leadLine2 ? leadLine1 : leadLine2, offset = displacement - 1, title = "Kumo Cloud Upper Line", display = display.none) 
plot(leadLine1 < leadLine2 ? leadLine1 : leadLine2, offset = displacement - 1, title = "Kumo Cloud Lower Line", display = display.none) 
fill(p1, p2, color = leadLine1 > leadLine2 ? color.rgb(67, 160, 71, 90) : color.rgb(244, 67, 54, 90))

//stoploss calculating
mult1 = input.float(1.618, "Mult1")
mult2 = input.float(0.618, "Mult2")
stoploss1 = leadLine1 - (leadLine1 - leadLine2)*mult1
stoploss2 = leadLine1 - (leadLine1 - leadLine2)*mult2
plot(stoploss1,"Sl", color = color.fuchsia, linewidth = 2, style = plot.style_line, offset = displacement - 1)
plot(stoploss2,"S2", color = color.lime, linewidth = 2, style = plot.style_line, offset = displacement - 1)

longCondition = leadLine1 > leadLine2 
if (longCondition)
    strategy.entry("Buy", strategy.long)

shortCondition = leadLine1 < leadLine2
if (shortCondition)
    strategy.entry("Sell", strategy.short)

```

> Detail

https://www.fmz.com/strategy/445451

> Last Modified

2024-03-19 15:10:59
