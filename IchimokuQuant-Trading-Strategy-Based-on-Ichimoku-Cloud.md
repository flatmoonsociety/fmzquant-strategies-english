
> Name

Quant-Trading-Strategy-Based-on-Ichimoku-Cloud
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1bcace6903f7706a3e8.png)
[trans]

## Overview
This strategy designs a quantitative trading system based on the Ichimoku cloud indicator, which is mainly used for assets with good trends. This strategy integrates stop loss, stop loss, trailing stop and other functions, aiming to achieve stable profits.
## Strategy Principle
The Ichimoku cloud chart consists of the conversion line, baseline, frontier line 1, frontier line 2 and cloud chart. The trading signals for this strategy come from the relationship between price and cloud. Specifically, when the price crosses the front line 1, a buy signal is generated; when the price crosses the front line 1, a sell signal is generated. In addition, Frontier 2 will also serve as an auxiliary judgment indicator.
This strategy also sets stop loss and take profit levels based on the ATR indicator. The ATR indicator can effectively capture the degree of market volatility. The stop loss level is 2 times ATR, and the take profit level is 4 times ATR. This can effectively control single losses and lock in part of the profits.
Finally, this strategy uses a trailing stop loss mechanism. Specifically, for long orders, 2 times ATR will be used as the fallback position, and the stop loss line will be adjusted in real time to lock in profits; for short orders, 2 times ATR will be used as the fallback position, and the stop loss line will be adjusted in real time to lock in profits.
## Strategic advantage analysis
1. Based on the Ichimoku cloud chart indicator, it can effectively capture trends
2. Combined with the ATR indicator for stop loss and profit, you can control risks
3. Using the trailing stop loss mechanism can lock in profits well
4. The strategy logic is simple and clear, easy to understand and verify
5. Parametrization can be used to adjust parameters according to different markets.
## Risk Analysis
1. Ichimoku cloud chart is sensitive to Paramer settings. Improper settings may miss trading opportunities or generate wrong signals.
2. If the trailing stop loss is set too large, the loss may be stopped prematurely.
3. Strong stocks may break through the stop loss line or trailing stop loss line given by the ATR indicator
4. Transaction costs will also have a certain impact on profitability
Solutions corresponding to risks:
1. Optimize the parameters of Ichimoku cloud chart and find the most suitable settings
2. Evaluate a reasonable trailing stop loss range, which should not be too large or too small.
3. For strong stocks, the stop loss range can be appropriately relaxed
4. Choose a brokerage with low handling fees
## Strategy optimization direction
1. Combine with other technical indicators for signal filtering to reduce erroneous transactions
2. Optimize parameters based on historical data/backtesting
3. Parameter settings for different varieties can be optimized separately
4. You can consider dynamically adjusting the stop loss range
5. Combine algorithms for feature engineering to establish more reliable trading signals
## Summarize
This strategy is generally a stable trend following strategy. Determine the trend direction based on the Ichimoku cloud indicator; use the ATR indicator to set stop loss and profit; use trailing stop loss to lock in profits. The advantages are that the logic is simple and easy to understand; it can control single losses; and it can effectively track trends. However, there are also risks of sensitive parameter settings and stop loss being breached. By continuously optimizing the parameters as well as the strategy itself, better performance can be achieved.
||

## Overview

This strategy designs a quantitative trading system based on the Ichimoku Cloud indicator, mainly for assets with good trends. The strategy integrates functions such as stop loss, take profit, and trailing stop loss to achieve stable profits.

## Strategy Principle 

The Ichimoku Cloud consists of conversion line, base line, leading span 1, leading span 2 and cloud charts. The trading signals of this strategy come from the relationship between price and cloud charts. Specifically, a buy signal is generated when the price crosses above the leading span 1; A sell signal is generated when the price crosses below the leading span 1. In addition, the leading span 2 also serves as an auxiliary judgment indicator.

This strategy also sets stop loss and take profit based on the ATR indicator. The ATR indicator can effectively capture the degree of market fluctuation. The stop loss is set to 2 times the ATR, and the take profit is set to 4 times the ATR. This can effectively control single loss and lock in some profits.

Finally, the strategy adopts a trailing stop loss mechanism. Specifically, for long positions, it will use 2 times the ATR as the callback amplitude to adjust the stop loss line in real time to lock in profits; for short positions, it will use 2 times the ATR as the callback amplitude to adjust the stop loss line in real time to lock in profits.

## Advantage Analysis

1. Based on the Ichimoku cloud chart indicator, it can effectively capture trends
2. With ATR-based stop loss and take profit, it can control risks
3. Adopt trailing stop loss mechanism to lock in profits well  
4. The strategy logic is simple and clear, easy to understand and verify
5. parametrization is available, parameters can be adjusted according to different markets

## Risk Analysis

1. Ichimoku cloud maps are very sensitive to parameter settings, improper settings may miss trading opportunities or generate wrong signals
2. If the trailing stop loss amplitude is set too large, stop loss may occur prematurely
3. Strong stocks may break through the stop loss line or trailing stop loss line given by the ATR indicator
4. Transaction costs will also have some impact on profitability

Solutions to corresponding risks:
1. Optimize the parameters of Ichimoku cloud maps to find the most appropriate settings
2. Evaluate reasonable trailing stop loss amplitude, neither too large nor too small
3. For strong stocks, appropriately relax the stop loss range 
4. Choose brokers with low commissions

## Optimization Directions

1. Combine other technical indicators for signal filtering to reduce wrong trades
2. Optimize parameters based on historical data/backtesting  
3. Parameters for different varieties can be optimized separately
4. Consider dynamically adjusting the stop loss amplitude
5. Combine algorithms to do feature engineering to build more reliable trading signals  

## Summary  

In general, this strategy is a stable trend tracking strategy. Judge the trend direction based on the Ichimoku cloud indicator; set stop loss and take profit using the ATR indicator; use trailing stop loss to lock in profits. The advantages are simple logic, easy to understand; single loss can be controlled; trend can be tracked effectively. But there are also some risks of parameter sensitivity and stop loss being broken through. By continuously optimizing parameters and the strategy itself, better performance can be obtained.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Conversion Line Length|
|v_input_2|26|Base Line Length|
|v_input_3|52|Leading Span B Length|
|v_input_4|26|Lagging Span|
|v_input_5|14|ATR Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-05 00:00:00
end: 2024-01-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Ichimoku Cloud Strategy with SL, TP, and Trailing Stop", overlay=true)

conversionPeriods = input(9, "Conversion Line Length")
basePeriods = input(26, "Base Line Length")
laggingSpan2Periods = input(52, "Leading Span B Length")
displacement = input(26, "Lagging Span")
atrLength = input(14, title="ATR Length")

donchian(len) => math.avg(ta.lowest(len), ta.highest(len))
conversionLine = donchian(conversionPeriods)
baseLine = donchian(basePeriods)
leadLine1 = math.avg(conversionLine, baseLine)
leadLine2 = donchian(laggingSpan2Periods)

// Plot the Ichimoku Cloud components
plot(conversionLine, color=color.blue, title="Conversion Line")
plot(baseLine, color=color.red, title="Base Line")
plot(leadLine1, color=color.green, title="Leading Span A")
plot(leadLine2, color=color.orange, title="Leading Span B")
plot(leadLine1 > leadLine2 ? leadLine1 : leadLine2, color=color.green, title="Kumo Cloud Upper Line")
plot(leadLine1 < leadLine2 ? leadLine1 : leadLine2, color=color.red, title="Kumo Cloud Lower Line")

// ATR for stop loss and take profit
atrValue = ta.atr(atrLength)
stopLoss = atrValue * 2
takeProfit = atrValue * 4

// Strategy entry and exit conditions
longCondition = ta.crossover(close, leadLine1) and close > leadLine2
shortCondition = ta.crossunder(close, leadLine1) and close < leadLine2

// Plot buy and sell signals
plotshape(series=longCondition ? leadLine1 : na, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(series=shortCondition ? leadLine1 : na, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)

// Execute strategy orders with stop loss and take profit
strategy.entry("Buy", strategy.long, when=longCondition)
strategy.close("Buy", when=shortCondition) // Close buy position when sell condition is met
strategy.entry("Sell", strategy.short, when=shortCondition)
strategy.close("Sell", when=longCondition) // Close sell position when buy condition is met

// Trailing stop
strategy.cancel("Trailing Stop")
var float trailingStopPrice = na
if (longCondition)
    trailingStopPrice := math.max(trailingStopPrice, close - atrValue * 2)
    strategy.exit("Trailing Stop", from_entry="Buy", trail_offset=atrValue * 2, trail_price=trailingStopPrice)
else if (shortCondition)
    trailingStopPrice := math.min(trailingStopPrice, close + atrValue * 2)
    strategy.exit("Trailing Stop", from_entry="Sell", trail_offset=atrValue * 2, trail_price=trailingStopPrice)

```

> Detail

https://www.fmz.com/strategy/438492

> Last Modified

2024-01-12 14:20:43
