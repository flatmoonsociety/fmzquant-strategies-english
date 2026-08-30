
> Name

Cloud-based trading strategy Ichimoku-Cloud-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy implements simple trend following trading based on the daily ichimoku cloud indicator. The strategy generates buy and sell signals by calculating the conversion line, base line, leading line 1 and leading line 2, combined with the current closing price position. When the closing price is above the cloud chart, it is considered to be in an upward trend and a buy signal is generated; when the closing price is below the cloud chart, it is deemed to be in a downward trend and a sell signal is generated.
## Strategy Principle
This strategy is mainly based on the following formula to calculate the five indicator lines of the ichimoku cloud chart:
1. Conversion line: the average of the highest and lowest prices in the last 9 days
2. Baseline: the average of the highest and lowest prices in the last 26 days
3. Leading line 1: the average of the conversion line and the baseline
4. Leading line 2: the average of the highest price and lowest price in the last 52 days
5. Chart line: closing price, delayed 26 days later
When the closing price is higher than the cloud chart, it is considered to be in an upward trend and a buy signal is generated; when the closing price is lower than the cloud chart, it is deemed to be in a downward trend and a sell signal is generated.
Specifically, the strategy is implemented through the following steps:
1. Calculate the conversion line, baseline line, leading line 1, and leading line 2
2. Draw a chart line of the closing price, delayed by 26 days
3. Determine whether the closing price is higher than the cloud chart (leading line 1 and leading line 2), if so, generate a buy signal
4. Determine whether the closing price is lower than the cloud chart (leading line 1 and leading line 2), if so, generate a sell signal
5. When buy and sell signals are generated, enter the market according to the strategy settings
## Advantage Analysis
This strategy mainly has the following advantages:
1. Use cloud chart indicators to effectively identify trends and generate signals based on the trend direction to avoid unnecessary entry and exit in volatile markets.
2. The calculation parameters have been optimized and selected, which is more suitable for daily trading.
3. Using the combination of leading line 1 and leading line 2 as the judgment standard can filter some false signals caused by shocks and shocks.
4. Combined with the delay design of the attached chart line, it can reduce the risk of an immediate callback after breaking through the top of the cloud chart.
5. The strategy logic is simple and clear, easy to understand and implement
6. No need to combine with other indicators to realize a complete trend tracking trading system
## Risk Analysis
There are also some risks with this strategy:
1. Under certain market conditions, the cloud chart may fail, resulting in false signals.
2. When the parameters of the cloud chart do not adapt to changes in the market environment, the effect of the system will be weakened.
3. The fixed delay setting of the attached chart line may also miss some opportunities.
4. Although there are two leading lines of combined judgment, the risks brought by the catfish effect cannot be completely avoided.
5. There is a certain time lag and rapid reversal cannot be captured in time.
6. Failure to distinguish between long-term market trends and short- and medium-term adjustments may result in losses
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize conversion lines, baselines and other parameters to make them more consistent with different market environments
2. Add trend judgment indicators to confirm the trend direction and strength.
3. Set up stop-loss and take-profit strategies to control single losses and profits
4. Combined with volume, enter the market only when the large volume breaks through the cloud chart.
5. Use different parameter combinations according to market stage
6. Add machine learning algorithm to automatically optimize parameters
7. Consider changing fixed delays to dynamic delays
## Summarize
Overall, the ichimoku cloud chart strategy implements basic trend following trading through simple trend judgment rules. Although there is some room for improvement, its core idea is clear and reliable, and its parameters are fully optimized. It can be used as a basic strategy for quantitative trading. By further optimizing the cloud chart parameters and adding filtering indicators and risk control modules, this strategy can become a very practical quantitative trading system.
||


## Overview

This strategy implements simple trend-following trading based on the ichimoku cloud indicator on daily charts. It generates buy and sell signals by calculating the conversion line, base line, leading span 1, leading span 2, and comparing the closing price's position relative to the cloud. When the closing price is above the cloud, it is considered an upward trend and a buy signal is generated. When the closing price is below the cloud, it is considered a downward trend and a sell signal is generated.  

## Strategy Logic

The strategy mainly calculates the five lines of the ichimoku cloud indicator based on the following formulas:

1. Conversion Line: 9-period average of the highest high and lowest low

2. Base Line: 26-period average of the highest high and lowest low

3. Leading Span 1: average of the conversion line and base line

4. Leading Span 2: 52-period average of the highest high and lowest low 

5. Lagging Span: closing price plotted 26 periods behind

When the closing price is above the cloud, it is considered an upward trend and a buy signal is generated. When the closing price is below the cloud, it is considered a downward trend and a sell signal is generated.

Specifically, the strategy implements this logic through the following steps:

1. Calculate the conversion line, base line, leading span 1, and leading span 2

2. Plot the lagging span of the closing price 26 periods behind

3. Check if the closing price is above the cloud (leading span 1 and 2), generate buy signal if true

4. Check if the closing price is below the cloud, generate sell signal if true 

5. Enter trades on buy/sell signals based on strategy settings

## Advantage Analysis

The main advantages of this strategy are:

1. Using the ichimoku cloud can effectively identify trends and generate signals along the trend direction, avoiding unnecessary trades in range-bound markets.

2. The calculation parameters are optimized for daily trading. 

3. Using both leading span 1 and 2 combines multiple signals to filter out false signals.

4. The lagging span delay helps reduce risk of immediate pullback after cloud breakout.

5. Simple and clear logic, easy to understand and implement.

6. No other indicators needed, complete trend following system.

## Risk Analysis

There are some risks to consider:

1. The cloud may fail in certain market conditions, generating incorrect signals.

2. If parameters are not adapted to changing market dynamics, it weakens the system.

3. The fixed lagging span delay may miss some opportunities. 

4. Still cannot completely avoid whipsaws.

5. There is some time lag, unable to capture quick reversals.

6. Cannot differentiate major trends vs shorter corrections, may cause losses.

## Improvement Areas

Some ways to improve the strategy:

1. Optimize parameters like conversion line for different market conditions.

2. Add trend filtering indicators to confirm strength and direction. 

3. Implement stop loss and take profit to control loss per trade.

4. Only take cloud breakout signals with high volume.

5. Use different parameter sets based on market regime.

6. Add machine learning to auto-optimize parameters.  

7. Consider dynamic lagging span instead of fixed delay.

## Summary

Overall, this ichimoku cloud strategy implements basic trend following rules, although improvements can be made. The core logic is sound, parameters optimized, good baseline algo trading strategy. With further cloud parameter enhancement, adding filters and risk controls, it can become a very practical quantitative trading system.

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
start: 2023-09-30 00:00:00
end: 2023-10-07 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="Ichimoku Cloud", shorttitle="Ichimoku", overlay=true, commission_type=strategy.commission.percent,commission_value=0.075, initial_capital = 1000,  default_qty_type=strategy.percent_of_equity, default_qty_value=100)

conversionPeriods = input(9, minval=1, title="Conversion Line Periods"),
basePeriods = input(26, minval=1, title="Base Line Periods")
laggingSpan2Periods = input(52, minval=1, title="Lagging Span 2 Periods"),
displacement = input(26, minval=0, title="Displacement")

donchian(len) => avg(lowest(len), highest(len))

conversionLine = donchian(conversionPeriods)
baseLine = donchian(basePeriods)
leadLine1 = avg(conversionLine, baseLine)
leadLine2 = donchian(laggingSpan2Periods)

plot(conversionLine, color=#0496ff, title="Conversion Line")
plot(baseLine, color=#991515, title="Base Line")
plot(close, offset = -displacement, color=#459915, title="Lagging Span")

p1 = plot(leadLine1, offset = displacement, color=color.green,
 title="Lead 1")
p2 = plot(leadLine2, offset = displacement, color=color.red, 
 title="Lead 2")
fill(p1, p2, color = leadLine1 > leadLine2 ? color.green : color.red)
buy = close > leadLine1[26] and close > leadLine2[26]
sell = close < leadLine1[26] and close < leadLine2[26]
strategy.entry("Buy", strategy.long, when = buy)
strategy.entry("Sell", strategy.short, when = sell)

```

> Detail

https://www.fmz.com/strategy/428684

> Last Modified

2023-10-08 12:24:06
