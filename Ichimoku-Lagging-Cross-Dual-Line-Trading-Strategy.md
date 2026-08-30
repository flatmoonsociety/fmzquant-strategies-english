
> Name

Lagging Cross Dual Line Trading StrategyIchimoku-Lagging-Cross-Dual-Line-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/89207d15da3c930a41.png)

[trans]


## Overview
Yiyun delayed cross double-line trading strategy is a common Yiyun K-line technical analysis trading strategy. This strategy uses the K-line cloud band and the intersection of the two baselines to determine the turning point of the market. The Yiyun Delayed Cross Trading Strategy has proven to be a profitable trading strategy.
## Strategy Principle
This strategy mainly uses the 5 baselines of Yiyun K-line. You need to first understand the meaning of these lines:
The antenna, also called the conversion line, represents the midpoint of the last 9 K lines. The calculation formula is:
The baseline, also called the standard line, represents the midpoint of the last 26 K lines. The calculation formula is:
Confirming lines, also known as late moving lines, lag behind the price (as the name suggests). The delay line is drawn 26 periods ago.
Leading 1, also called Leading 1, represents a boundary of the cloud band and is the midpoint between the conversion line and the baseline:. This value is plotted after 26 cycles and is the faster cloud band boundary.
Leading 2, also known as Leading 2, represents another boundary of the cloud band and is the midpoint of the recent 52 K lines:. This value is plotted after 52 cycles and is the slower cloud band boundary.
The rules for using Yiyun K-line trading are very simple:
When the conversion line crosses the baseline, take a buy signal.
When the conversion line crosses below the baseline, a sell signal is taken.
## Advantage Analysis
Yiyun delayed cross dual-line trading strategy has the following advantages:
1. Use the intersection of the conversion line and the baseline to determine the timing of buying and selling. The strategy rules are simple and clear.
2. Using cloud bands and their boundaries to determine the trend direction can reduce false signals.
3. The delay line lags behind the price and can verify the trend.
4. Use a variety of lines in combination to comprehensively judge the market and improve decision-making accuracy.
5. Can be used for trading analysis in various time periods.
## Risk Analysis
Yiyun delayed cross dual-line trading strategy also has the following risks:
1. Improper setting of line parameters may result in excessive false signals.
2. When the bull-bear transition occurs, the line crossover signal may be delayed and the turning point cannot be grasped in time.
3. When the market fluctuates violently, Yiyun K-line may fail.
4. More indicators need to be combined to verify the signal, and the effect may be limited when used alone.
5. Frequent monitoring is required and full automatic trading is not possible.
## Optimization direction
Yiyun delayed cross dual-line trading strategy can be optimized from the following aspects:
1. Optimize line parameters and improve delay line settings to make signals more accurate.
2. Combine with indicators such as trend index to judge trend reversal in advance.
3. Add FILTER to filter out false signals.
4. Optimize the strategy to automatically limit profits and losses, and strictly control risks.
5. Test the parameter effects of different varieties and time periods.
6. Carry out backtest optimization and select the best parameter combination.
## Summarize
Yiyun Delayed Crossover Dual Line Trading Strategy utilizes simple conversion line and baseline crossovers to generate trading signals. This strategy effectively uses cloud bands to determine the trend direction and can filter out some noise. However, improper parameter settings can also produce false signals and require further optimization. This strategy is easy to implement, but the best results require combination with other indicators. Through continuous testing and optimization, the strategy can respond promptly to market changes, reducing risks while improving profitability.
||


## Overview

The Ichimoku Lagging Cross Dual Line trading strategy is a common Ichimoku candlestick chart analysis trading strategy. This strategy uses the Ichimoku cloud bands and crossovers of two baseline lines to identify reversal points in the market. The Ichimoku lagging cross trading strategy has proven to be a profitable trading strategy.

## Strategy Principles 

This strategy mainly uses 5 baseline lines of the Ichimoku candlesticks. It is necessary to first understand the meaning of these lines:

Tenkan-Sen line, also called the Conversion Line, represents the midpoint of the last 9 candlesticks, and is calculated with the formula:

Kijun-Sen line, also called the Base Line, represents the midpoint of the last 26 candlesticks, and is calculated with the formula: 

Chikou Span, also called the Lagging Span, lags behind the price (as the name suggests). The Lagging Span is plotted 26 periods back.

Senkou Span A, also called the Leading Span A, represents one of the Cloud boundaries and it is the midpoint between the Conversion Line and the Base Line: . This value is plotted 26 periods into the future and it is the faster Cloud boundary.

Senkou Span B, or the Leading Span B, represents the second Cloud boundary and it is the midpoint of the last 52 price bars: . This value is plotted 52 periods into the future and it is the slower Cloud boundary.

The trading rules with Ichimoku are very simple:

When the Conversion Line crosses above the Base Line, it triggers a buy signal.

When the Conversion Line crosses below the Base Line, it triggers a sell signal.

## Advantage Analysis

The Ichimoku Lagging Cross Dual Line trading strategy has the following advantages:

1. Using crossover of Conversion and Base Lines to determine entries and exits, the strategy rules are simple and clear.

2. Using the cloud bands and boundaries to determine trend direction, it reduces false signals.

3. The lagging line lags behind the price and can confirm the trend. 

4. The combination of multiple lines provides comprehensive market assessment and improves decision accuracy.

5. Can be used for trading analysis across various timeframes.

## Risk Analysis

The Ichimoku Lagging Cross Dual Line trading strategy also has the following risks:

1. Improper parameter settings may generate excessive false signals.

2. Crossover signals may lag around trend reversals, unable to capture turning points timely.

3. Ichimoku may fail with violent price fluctuations.

4. Needs more indicators to confirm signals, limited effects when used alone. 

5. Requires frequent monitoring, cannot be fully automated.

## Optimization Directions

The Ichimoku Lagging Cross Dual Line trading strategy can be optimized in the following aspects:

1. Optimize line parameters, improve lagging line settings for more accurate signals.

2. Incorporate trend indices to anticipate trend reversals early. 

3. Add FILTERS to filter out false signals.

4. Optimize stop loss and take profit points to control risks.

5. Test parameters across different products and timeframes.  

6. Conduct backtesting for best parameter combinations.

## Conclusion

The Ichimoku Lagging Cross Dual Line trading strategy uses simple conversion and base line crossovers to generate trade signals. It effectively uses the cloud bands to determine trend direction and filter out some noise. However, improper parameter settings can also produce false signals, requiring further optimizations. This strategy is easy to implement but best effects would need incorporating other indicators. With continuous testing and optimizations, this strategy can adapt to market changes timely, improving profitability while reducing risks.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Conversion Line Periods|
|v_input_2|26|Base Line Periods|
|v_input_3|52|Lagging Span 2 Periods|
|v_input_4|26|Displacement|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-19 00:00:00
end: 2023-10-19 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © iamskrv

//@version=4
strategy("Ichimoku Cloud Strategy v2.0", overlay=true)

//@version=4
// study(title="Ichimoku Cloud", shorttitle="Ichimoku", overlay=true)

conversionPeriods = input(9, minval=1, title="Conversion Line Periods"),
basePeriods = input(26, minval=1, title="Base Line Periods")
laggingSpan2Periods = input(52, minval=1, title="Lagging Span 2 Periods"),
displacement = input(26, minval=1, title="Displacement")

donchian(len) => avg(lowest(len), highest(len))

conversionLine = donchian(conversionPeriods)
baseLine = donchian(basePeriods)
leadLine1 = avg(conversionLine, baseLine)
leadLine2 = donchian(laggingSpan2Periods)

plot(conversionLine, color=#0496ff, title="Conversion Line")
plot(baseLine, color=#991515, title="Base Line")
plot(close, offset = -displacement + 1, color=#459915, title="Lagging Span")

p1 = plot(leadLine1, offset = displacement - 1, color=color.green,
 title="Lead 1")
p2 = plot(leadLine2, offset = displacement - 1, color=color.red, 
 title="Lead 2")
fill(p1, p2, color = leadLine1 > leadLine2 ? color.green : color.red)

// Strategy


longCondition = crossover(conversionLine,baseLine)
if (longCondition)
    strategy.entry("Buy", strategy.long)

shortCondition = crossover(baseLine, conversionLine)
if (shortCondition)
    strategy.entry("Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/429786

> Last Modified

2023-10-20 17:17:28
