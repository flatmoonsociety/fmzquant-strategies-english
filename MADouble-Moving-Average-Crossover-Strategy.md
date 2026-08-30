
> Name

Double-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/6930d91716e4ea0611.png)
[trans]

## Overview
This strategy is a trading strategy based on double moving averages. It will perform golden cross and dead cross operations based on the long and short moving averages set by the user, that is, it will send out trading signals when the fast moving average crosses or falls below the slow moving average. When the fast MA crosses above the slow MA, go long; when the fast MA crosses below the slow MA, go short.
## Strategy Principle
The core logic of this strategy is based on the crossover principle of double moving averages. What is a moving average? It is the average price obtained by taking the arithmetic average of the closing prices within a certain period of time. Moving averages can effectively filter out random noise and reflect clearer price trends.
In this strategy, the short-term MA represents the short-term trend of prices, and the long-term MA represents the long-term trend of prices. The short-term MA is more sensitive to price changes than the long-term MA and can capture price reversals faster. When the short-term MA crosses above the long-term MA, it means that the short-term trend has turned to upwards, and you are going long; when the short-term MA crosses below the long-term MA, it means that the short-term trend has turned to short, and you are going short.
Specifically, the strategy uses ta.sma to calculate the simple moving average of the specified period as a trading signal. Users can customize two MA parameters, namely long_period and short_period. The strategy uses ta.crossover and ta.crossunder to determine the golden cross and dead cross of the MA. When the short MA crosses above the long MA, that is, when the golden cross appears, go long; when the short MA crosses below the long MA, that is, when the dead cross appears, go short.
## Strategic Advantages
This strategy has the following advantages:
1. Simple operation and easy to master.
2. Customizable parameters to adapt to various market environments.
3. Use the double MA crossover principle to effectively filter noise and capture trend reversals.
4. High sensitivity and able to capture price turning points in time.
## Strategy Risk
There are also some risks with this strategy:
1. If the distance between the two MAs is too small, it will easily produce false signals.
2. Improperly cutting off the MA cycle and missing the main trend.
3. A reversal does not necessarily mean a trend turning point, and false signals may appear.
4. Parameters need to be adjusted appropriately to avoid over-optimization.
In view of the above risks, optimization can be carried out by adjusting MA parameters, setting stop loss and take profit, or combining with other indicators.
## Optimize space
This strategy can be optimized from the following aspects:
1. Optimize MA cycle parameters and adopt adaptive MA cycle.
2. Increase trading volume filtering to avoid false breakthroughs. 
3. Combine with other technical indicators, such as MACD, KDJ, etc.
4. Add stop-loss and take-profit logic to control single losses.
5. Optimize the code structure and increase the space for later expansion of modularization.
## Summarize
Overall, this strategy is very suitable as an introductory strategy for quantitative trading. It only requires simple double MA parameters to run, is simple to operate, easy to understand, and can intuitively reflect market reversal opportunities. At the same time, the strategy leaves a large space for optimization, and parameters can be adjusted or other logic added according to actual needs for improvement.
||

## Overview

This is a trading strategy based on double moving averages crossover. It generates buy and sell signals when two moving averages of different lengths cross over. Specifically, it goes long when the faster MA crosses above the slower MA, and goes short when the faster MA crosses below the slower MA.  

## Strategy Logic

The core logic of this strategy lies in the crossover principles between two moving averages. A moving average is the arithmetic average price over a specified time period. It helps filter out market noise and reveal clearer price trends.

In this strategy, the shorter-term MA captures short-term trends while the longer-term MA captures long-term trends. As the short-term MA is more sensitive in responding to the latest price changes, crossing over the long-term MA signals a trend reversal ahead. 

Specifically, the strategy calculates the MAs using ta.sma over the long_period and short_period defined by users. It then uses ta.crossover and ta.crossunder to detect the golden crossover and death crossover between the two MAs. When the short MA crosses above the long MA, go long. When the short MA crosses below, go short.

## Advantages  

The main advantages of this strategy include:

1. Simple logic, easy to follow.  
2. Customizable parameters adaptable to various markets.
3. MA crossover filters out noise, capturing trend reversal.  
4. High sensitivity in capturing price inflection points.

## Risks

There are also several risks:   

1. Too small gap between MAs causes false signals.
2. Wrong MA periods miss major trends. 
3. Reversals do not always imply trend changes.
4. Parameters need adjustment to avoid overfitting.  

To mitigate the risks, parameters can be tuned, stop loss and take profit can be incorporated, or other technical indicators can be added.

## Optimization

There is room for further optimization:

1. Optimize adaptive MA periods.  
2. Add volume filter to avoid false breakout.
3. Incorporate other indicators like MACD, KDJ. 
4. Add stop loss/take profit to limit loss.
5. Improve code structure for better scalability.

## Conclusion

In conclusion, this is an ideal starter strategy for algorithmic trading, thanks to its simplicity in logic and parameters while still able to effectively capture market reversals. At the same time, it has great potential for optimizations to fit various trading needs.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Long Period|
|v_input_2|5|Short Period|
|v_input_string_1|0|MA type: SMA|EMA|
|v_input_3|true|Stop Loss (%)|
|v_input_4|2|Take Profit (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Cross 2 Moving Average Strategy", shorttitle="2MA Cross", overlay=true)

// User-defined input for moving averages
long_period = input(20, title="Long Period")
short_period = input(5, title="Short Period")
type_ma = input.string("SMA", title = "MA type", options = ["SMA", "EMA"])

// Calculating moving averages
long_ma = ta.sma(close, long_period)
short_ma = ta.sma(close, short_period)

// Plot moving averages
plot(long_ma, title="Long Moving Average", color=color.red)
plot(short_ma, title="Short Moving Average", color=color.green)

// Strategy logic for crossing of moving averages
longCondition = ta.crossover(short_ma, long_ma)
shortCondition = ta.crossunder(short_ma, long_ma)

// Entry orders
if (longCondition)
    strategy.entry("Long", strategy.long)

if (shortCondition)
    strategy.entry("Short", strategy.short)

// Optional: Add stop loss and take profit
stop_loss_perc = input(1, title="Stop Loss (%)") / 100
take_profit_perc = input(2, title="Take Profit (%)") / 100

strategy.exit("Exit Long", from_entry="Long", stop=close*(1-stop_loss_perc), limit=close*(1+take_profit_perc))
strategy.exit("Exit Short", from_entry="Short", stop=close*(1+stop_loss_perc), limit=close*(1-take_profit_perc))

```

> Detail

https://www.fmz.com/strategy/440517

> Last Modified

2024-01-31 11:29:45
